---
title: "💻 Implementation"
description: "How we implemented key aspects of NudgeMe."
layout: single
image: "images/implementation/flutter-go.png"
date: 2021-03-09
draft: false
---

# Mobile/Client-side Features

Below are details of how we implemented key parts of the mobile application.

## PDF Generation

We want to generate a PDF of the user's wellbeing graph, and allow them to
share it.
We use two libraries - pdf and printing - to generate a PDF of a widget.

At first, this _seems_ easy.
These libraries allow us to easily share a PDF that contains some image.
We just have to create the document, add a page that contains an image
and save the document. Here is the relevant method in our sharing class:

``` dart
void _share() async {
    final doc = pw.Document(); // create new document

    // Get image source, we implement _fromWidgetKey() ourselves:
    final ImageProvider flutterImg = await _fromWidgetKey(); 

    // convert the image source into a format recognised by the pdf library:
    final pw.ImageProvider img = await flutterImageProvider(flutterImg); 

    // adds an a4 page containing the image at the center
    doc.addPage(pw.Page(
        pageFormat: PdfPageFormat.a4,
        build: (pw.Context ctx) => pw.Center(child: pw.Image.provider(img))));

    // opens the share panel, allowing the user to share the newly
    // created document
    await Printing.sharePdf(bytes: doc.save(), filename: _filename);
}
```

The problem (and interesting part) is how we get an image (i.e. how to implement 
the `_fromWidgetKey()` method). Firstly, the 
'image' that we wish to share is the image of the user's wellbeing graph. However, 
this is *not* actually an 'image' (yet), it is a visual component of the UI 
built and drawn by Flutter.

To convert an arbitrary widget to an image, it must first be wrapped around a
`RepaintBoundary` widget. From the docs:

> Creates a widget that isolates repaints.
> <cite>-- `RepaintBoundary`</cite>

This then allows us to capture the state of the widget and convert it to an image.
As usual in Flutter, we will use a key (which acts a bit like a pointer) so we
can perform the conversion when needed. Here is a bit of code from the wellbeing 
graph:

``` dart
// this is from the _getGraph method in wellbeing_graph.dart
return Flexible(
    child: RepaintBoundary(
        // wraps it in a [RepaintBoundary] so we can use .toImage()
        key: _printKey, // this [RepaintBoundary] will be 'printed'/shared
        child: charts.BarChart(
```

There is one more part before we can define `_fromWidgetKey()`. The PDF library
requires an `ImageProvider`, not an `Image`[^1], which is what `.toImage()` will
return. However, we can convert an `Image` by taking it's byte data and creating
an `ImageProvider` from it's raw byte data.

This is the implementation of `_fromWidgetKey()`:
``` dart
/// will get an [ImageProvider] for the widget associated with _printKey
Future<ImageProvider> _fromWidgetKey() async {
  // gets the RenderObject associated with the RepaintBoundary pointed to by _printKey:
  final RenderRepaintBoundary wrappedWidget =
      _printKey.currentContext.findRenderObject();
  final img = await wrappedWidget.toImage();

  // needs to be a PNG format, otherwise the conversion won't work
  final byteData = await img.toByteData(format: ImageByteFormat.png);
  return MemoryImage(byteData.buffer.asUint8List());
}
```

[^1]: The difference is that `ImageProvider` is a way to identify or reference an
      image, but `Image` is an actual image asset.

## Public Key Cryptography

### Key Generation & Storage

We used the [pointycastle](https://pub.dev/packages/pointycastle) library
to generate the RSA keypair. `PointyCastle` is a Dart port of a well-known
crypto library called `BouncyCastle` so we concluded that `PointyCastle` would
be a good choice.

It is simple to generate the keypair:

``` dart
final keyPair = await compute<SecureRandom, AsymmetricKeyPair<RSAPublicKey, RSAPrivateKey>>(
    generateRSAKeyPair, _getSecureRandom());
```

This gives us key objects `RSAPublicKey` and `RSAPrivateKey`. However, we need
to store this persistently so to do this we manually encode the keys into
a [PEM](https://en.wikipedia.org/wiki/Privacy-Enhanced_Mail) format string. We 
can then store this string using `SharedPreferences`.

To store the keys in PEM, the middle section consists of the base64 of the ASN.1 sequence
of components, defined in the appendix of [RFC 8017](https://tools.ietf.org/html/rfc8017#appendix-A).
We use the [PKCS#1](https://en.wikipedia.org/wiki/PKCS_1) definition of RSA.

#### Public Key - PEM Format

The RFC specifies how the keys should be identified in ASN.1:
``` 
RSAPublicKey ::= SEQUENCE {
    modulus           INTEGER,  -- n
    publicExponent    INTEGER   -- e
}
```

This tells us the order of the components expected. We can use
`ASN1Sequence` from `pointycastle` to then encode the appropriate sequence of 
bytes and wrap the base64 encoded string in the PEM header/footer:

``` dart
String encodePublicKeyInPem(RSAPublicKey key) {
    final asn = ASN1Sequence();

    // convert and add the two attributes of the key
    asn.add(ASN1Integer(key.modulus));
    asn.add(ASN1Integer(key.exponent));

    final bytes = asn.encode()
    final base64Data = base64.encode(bytes);
    return '-----BEGIN RSA PUBLIC KEY-----\n$base64Data\n-----END RSA PUBLIC KEY-----';
}
```

#### Private Key - PEM Format

```
RSAPrivateKey ::= SEQUENCE {
    version           Version,
    modulus           INTEGER,  -- n
    publicExponent    INTEGER,  -- e
    privateExponent   INTEGER,  -- d
    prime1            INTEGER,  -- p
    prime2            INTEGER,  -- q
    exponent1         INTEGER,  -- d mod (p-1)
    exponent2         INTEGER,  -- d mod (q-1)
    coefficient       INTEGER,  -- (inverse of q) mod p
    otherPrimeInfos   OtherPrimeInfos OPTIONAL
}
```

This is similar to the public key storage, except we compute the `exponent1`,
`exponent2` and the `coefficient` using the above expressions, instead of directly
using attributes of the key.

``` dart
String encodePrivateKeyInPem(RSAPrivateKey key) {
    final asn = ASN1Sequence();

    asn.add(ASN1Integer(BigInt.zero)); // version
    asn.add(ASN1Integer(key.n)); // modulus
    asn.add(ASN1Integer(key.exponent)); // public exponent
    asn.add(ASN1Integer(key.privateExponent));
    asn.add(ASN1Integer(key.p));
    asn.add(ASN1Integer(key.q));
    asn.add(ASN1Integer(key.privateExponent % (key.p - BigInt.one))); // exp1
    asn.add(ASN1Integer(key.privateExponent % (key.q - BigInt.one))); // exp2
    asn.add(ASN1Integer(key.q.modInverse(key.p))); // coefficient

    final base64Data = base64.encode(asn.encode());
    return '-----BEGIN RSA PRIVATE KEY-----\n$base64Data\n-----END RSA PRIVATE KEY-----';
}
```

### Encryption/Decryption

We store the public/private keys for the user as a string in `SharedPreferences`, so
when we wish to decrypt a message, e.g. `ciphertextBase64`, we can do the following:

``` dart
// load the public 
final pubKey = RSAKeyParser().parse(prefs.getString(RSA_PUBLIC_PEM_KEY))
    as pointyCastle.RSAPublicKey;
final privKey = RSAKeyParser().parse(prefs.getString(RSA_PRIVATE_PEM_KEY))
    as pointyCastle.RSAPrivateKey;

// create an Encrypter object that we can use to encrypt or decrypt
final encrypter = Encrypter(RSA(publicKey: pubKey, privateKey: privKey));

// decrypt some ciphertext string encoded in base64:
String plaintext = encrypter.decrypt64(ciphertextBase64);
```

For a given user, we store their friends' public keys in a database on their
device. So performing encryption is very similar except we retrieve the public
key from the database, and don't need to provide `Encrypter` with a private
key.

``` dart
// Parse `publicKey` attribute from `friend`, which is an object that stores
// the attributes of a row from the friend database.
final friendKey = 
    RSAKeyParser().parse(friend.publicKey) as pointyCastle.RSAPublicKey;
final encrypter = Encrypter(RSA(publicKey: friendKey));
final ciphertextBase64 = encrypter.encrypt(plaintext).base64;
```

## Database & Notifier/Listener Model

This section describes notable aspects of the SQLite database used for the
mobile client. We have two database helper classes that each manage their
own database[^2]. Both of these helper classes use the below ideas (Singleton,
Data Class, etc.).

[^2]: The reason we have two databases on the mobile client is the convenience 
      of splitting them into two separate files. In practice, they actually 
      behave like two tables in a database.

### Singleton Design Pattern

Although the singleton pattern is sometimes criticized, it is quite suitable for
the purpose of limiting the application to a single database connection.

Below is the code (from `user_model.dart`) that ensures only one instance of our 
database helper class exists:

``` dart
/// Singleton [ChangeNotifier] to read/write to DB.
/// Stores the user's wellbeing scores and steps.
class UserWellbeingDB extends ChangeNotifier {
    // create a static instance of this class, by calling the
    // private constructor
    static final UserWellbeingDB _instance = UserWellbeingDB._();
    static Database _database;

    // private constructor, so other code cannot create a new instance:
    UserWellbeingDB._(); 

    // factory used here, so we don't return a new instance when other code
    // calls UserWellbeingDB()
    factory UserWellbeingDB() =>
        _instance; 
```

Now that we've ensured that the *class* has only one instance, we also need
to ensure that the *database connection itself* has only one instance internally.

To do this, all methods of the database use a getter that lazily initializes[^3]
or returns an existing instance of the `_database`:

``` dart
/// getter that initializes or returns an existing database instance
Future<Database> get database async {
  if (_database == null) {
    // _init() opens a connection or creates a new database
    _database = await _init();
  }
  return _database;
}
```

_Read [this](https://dev.to/newtonmunene_yg/dart-getters-and-setters-1c8f) if
Dart's getter syntax is unfamiliar to you._

Here is one of the database methods that uses this getter:

``` dart
/// inserts a wellbeing record.
/// returns the id of the newly inserted record
Future<int> insert(WellbeingItem item) async {
  // Note how I call the getter `database` instead of using `_database`:
  final db = await database;

  final id = await db.insert(_tableName, item.toMap());
  notifyListeners();
  return id;
}
```

`notifyListeners` will be explained in a following section.

[^3]: Note that it is null by default. It is not initialized yet in
      the line `static Database _database;`.

### Database State Management

A crucial part of our implementation is how we handled the issue of state management
at runtime. It was clear early on that we would deal with two types of state, *persistent*
and *temporary* state (also called *ephemeral state*). Persistent state would be 
solved by using databases and temporary state could just be handled by `StatefulWidget`. 

However, there is an important third type of state: *persistent state loaded into 
memory*. This kind of state lead to problems where the underlying database (the persistent
state) may be modified but the state currently used to draw the UI is not updated.
As an example, suppose a screen displays the user's current username but then a
pop-up screen allows the user to modify it. Once the user returns to the underlying
screen Flutter would not rebuild the screen (if the code was implemented naïvely), 
instead displaying stale data.

One possible solution would be to constantly force the UI to rebuild the screen
and fetch the latest data from the persistent storage, whenever the screen is displayed.
However, this would lead to performance problems as Flutter relies on carefully
choosing when to rebuild and only doing so when necessary.

After watching [this talk from Google I/O](https://www.youtube.com/watch?v=d_m5csmrf7I) 
on state management in Flutter, we refactored the code to use the *notifier/listener
model*, which solved our state issue. This model specifies certain objects as
notifiers which *notify* listeners of any changes to their state. This is facilitated
by the `provider` package. 

This is how we extend `ChangeNotifier`:
``` dart
class FriendDB extends ChangeNotifier {
  // ... defining attributes here

  Future<int> insert(Friend item) async {
    // ... perform the insertion

    // The insertion counts as something that modifies the state of this object,
    // so we then notify any listeners.
    notifyListeners();
    
    // return appropriate value
  }
  
  // etc.
```

After extending `ChangeNotifier` we have access to `notifyListeners` which we call
after we perform some operation that modifies the internal state. We do not have
to call it for getters (and we shouldn't, for performance reasons).

At the top level of the widget tree, we wrap our app in a `MultiProvider`:

``` dart
return MultiProvider(
      // MultiProvider is a convenience widget to make multiple ChangeNotifiers
      // available to descendant widgets
      providers: [
        ChangeNotifierProvider(
          create: (context) => UserWellbeingDB(),
        ),
        ChangeNotifierProvider(
          create: (context) => FriendDB(),
        ),
      ],
      child: MaterialApp(
        title: 'NudgeMe',
        // etc.
```

This allows descendant widgets to listen and access the databases, without concern
of whether state should be updated or not, for example:

``` dart
FutureBuilder(
  future:
      // this implicitly listens to the database
      Provider.of<UserWellbeingDB>(context).getLastNWeeks(1),
  // etc.
```

This is the convenience of using the `provider` package. Now that we have defined
our `ChangeNotifier`, the above code is all that is needed to automatically listen 
and rebuild the UI if any changes to the database occur.

### Data Class Style for Rows

Data classes are a feature found in some OOP languages like Kotlin, and we use this
inspiration to manage insertion and retrieval from the database (although Dart
does not have official language features for data classes).

Here is the data class that represents a friend; the attributes correspond to the
columns of the database that stores friends:

``` dart
/// Data class of a friend.
/// Allows conversion from and to a map to work better with the SQL database.
class Friend implements Comparable {
  int id;
  String name;
  String identifier;
  String publicKey;

  /// json encoded string
  String latestData;

  /// 0 if unread, otherwise 1
  int read;

  /// nullable
  int currentStepsGoal;

  /// 1 if sent & active, 0 otherwise
  int sentActiveGoal;

  /// the step count value when a step goal was first started
  int initialStepCount;

  Friend({
    this.id, // this should be left null so SQL will handle it
    this.name,
    this.identifier,
    this.publicKey,
    this.latestData,
    this.read,
    this.currentStepsGoal,
    this.sentActiveGoal,
    this.initialStepCount,
  });

  Friend.fromMap(Map<String, dynamic> map) {
    // ...
  }

  Map<String, dynamic> toMap() {
    // ...
  }

  /// unread Friends < read Friends
  @override
  int compareTo(other) {
    // ...
  }
}
```

`Friend.fromMap` and `toMap` are straightforward methods that provide convenient
conversions to and from the representation that SQLite works with.

A notable method that uses this is `getFriends`:
``` dart
Future<List<Friend>> getFriends() async {
    final db = await database;
    
    // retrieve all the rows:
    List<Map> friendMaps = await db.query(_tableName, columns: _columns);
    final itemList = friendMaps
        // map each `Map` into a `Friend` object
        .map((friendMap) => Friend.fromMap(friendMap))
        .toList(growable: false);
    return itemList;
}
```

# Server-side

Below are details of how we implemented key parts of the backend server.

## Templating & Deeplinks

We use Go templates to render HTML with dynamic content.

One example of where it is used is in the creation of the page that allows
users to add someone to their network. Below are explanations of why we needed
this page and how we implemented it.

### The Custom URL Scheme Problem (& Our Solution)

We needed a way to allow a user to add someone else as a friend remotely. We had
initially developed the QR code method, where users can scan their friends QR 
code to add them. Then we realized that we could use deeplinking to pre-fill the 
string that would be retrieved from a QR code. (One of the requirements was to 
make it easy-to-use, so we couldn't rely on our users ability to copy and paste 
strings.)

So we defined a custom URL scheme like so:
```
nudgeme://addFriend?identifier="..."&pubKey="..."
```

After writing the relevant Flutter code, this did actually work - it correctly opened
and pre-filled the strings (skipping the QR scanning step of the add friend page).
However, there was a problem. Custom URL schemes are not recognised as clickable links
by many messaging apps. So if a user sends this link to a friend, there is a high
chance the messaging app will not allow them to click on the link (e.g. Whatsapp
does not allow this).

This is where the server is needed. If a website redirects a user to a custom URL scheme,
the corresponding app will be opened as expected. So we can serve a web page that
generates and redirects a user to our `nudgeme://` custom URL, thereby opening
the NudgeMe mobile app and pre-filling the user details in the add friend page.

This is where templating comes in.

### Templating

The HTML page is mostly static, except for the button that the user presses (since the URL
to redirect to needs to be generated dynamically). Here is the relevant HTML, from
`add_friend.html`:
```html
  <a href="nudgeme://addFriend?identifier={{ .Identifier }}&pubKey={{ .PubKey }}">
      <button>Add to Network</button>
  </a>
```

The Go server extracts the `identifier` and `pubKey` query parameters, creates a
`struct` that holds these strings and passes it as the input when rendering the
HTML template:
``` go
// data used in add_friend.html
type AddFriendTemplate struct {
  Identifier string
  PubKey     string
}

func handleAddFriend(c echo.Context) error {
  // extract the query paramters from the original HTTPS url that the user
  // used to reach here
  identifier := c.QueryParam("identifier")
  pubKey := c.QueryParam("pubKey")

  if isValidIDAndKey(identifier, pubKey) {
    // render the add_friend.html template if the parameters were valid
    return c.Render(http.StatusOK, "add_friend.html", AddFriendTemplate{
      Identifier: identifier,
      PubKey:     pubKey,
    })
  }
  return c.String(http.StatusBadRequest, "That link doesn't look right.")
}
```

## Caching Data - Mutexes & Goroutines

For the wellbeing visualization, we need to query the contents of the database
to get the stored wellbeing data. However, instead of performing this (relatively
expensive) database query everytime someone GETs our visualization, we cache the
relevant data. We use Go templates for the visualization page, so we can cache
the inputs to the template which are:

``` go
// data required by the map.html template
type MapTemplate struct {
  MAPDATA string
  SUPCODE string
}
```

So the idea is we have some `MapTemplate` that we will use every time
a user requests the map, while also periodically updating it.
(Since new wellbeing data may have been sent to us, the server.) However, this actually
introduces some potential concurrency bugs, which we will fix by using a mutex:
``` go
type SafeMapTemplate struct {
  // mutex that should be acquired before modifying `mapT`:
  mu   sync.Mutex
  // data required by map.html
  mapT MapTemplate
}

var mapTemplate SafeMapTemplate = SafeMapTemplate{}
```

We update `mapTemplate` with the following function:
``` go
// updates safeMapTemplate every `duration`
func updateTemplateCache(db *sql.DB, duration time.Duration) {
  // get the new data needed for map.html template
  mapT := getMapTemplate(db, false)

  // acquire the mutex
  mapTemplate.mu.Lock()
  // assign the new data
  mapTemplate.mapT = *mapT
  // release the mutex
  mapTemplate.mu.Unlock()

  // sleep for some time before recursively calling ourself
  time.Sleep(duration)
  updateTemplateCache(db, duration)
}
```

Which we can launch in a goroutine with 
`go updateTemplateCache(mainDb, time.Duration(2) * time.Minute)`.
Note that I retrieve the new data (`mapT`) *before* acquiring the mutex for a slight 
performance improvement.
