---
title: "⚙️ System Design"
description: "Explanation of the software architecture and design."
layout: system_design
date: 2021-03-08
image: "images/system-design/gears.png"
draft: false
---

## Diagrams & Explanation

### Dataflow of Wellbeing Visualization

One of the core requirements of NudgeMe was to publish data once a week to a 
server that uses this data to visualize wellbeing across different postcodes.
Below is a dataflow diagram that illustrates this.

<img src="https://user-images.githubusercontent.com/46009390/110238902-0135cb00-7f3c-11eb-88c4-445397e5ea50.png" 
alt="Dataflow diagram of wellbeing visualization"
width="960"/>

Here are some key points to note:
- After the user has performed their weekly wellbeing check, we store the data
locally, instead of just POSTing the data to the server. This is so we
can display their past wellbeing scores and step counts.
- We use local differential privacy to 'anonymize wellbeing' data, i.e. their
recorded wellbeing score is randomized before it is sent 30% of the time.

### Architecture of NudgeMe

_See the embedded Figma at the top of the page for a more convenient way to zoom
in and read this diagram._

<img src="https://user-images.githubusercontent.com/46009390/110238878-dd728500-7f3b-11eb-9c0d-6eb785270703.png"
alt="Architecture diagram of NudgeMe" 
width="960"/>

#### 1. Wellbeing Visualization (& Core Features)

The end user interacts with the mobile app (built with Flutter) on
Android or iOS. Any data stored on device is done so using SQLite or
`SharedPreferences`, using the 
[shared_preferences Flutter package](https://pub.dev/packages/shared_preferences).
`SharedPreferences` is a key-value store inspired by Android's implementation
(but works cross-platform due to the Flutter package). This offers us convenient
storage of simple data (e.g. persistent configuration flags). We use the SQLite
database for structured data.

For the server code, we use Go which runs as a `systemd` service on the Linode
server provided by our client. When web users request the webpage, the Go server
will use pre-cached[^1] wellbeing data to generate the HTML from our template file.
In addition, this Go server is an HTTPS server which runs on port 443. We use
Auto-TLS to automatically set up the certificates. Being able to use HTTPS is
important so sensitive request data is not sent in plaintext (like with HTTP).

[^1]: Pre-caching involves loading the data into memory and structuring it so
      it can be passed to the template file. This happens periodically.

#### 2. Network Sharing

This part is built on top of the wellbeing visualization architecture, but is separate and
works independently. 
To share data between mobile clients, we designed an infrastructure that passes
data/'messages'[^2]. This is then used along with client-side asymmetric key
encryption to support E2E encrypted message passing between users of our app.

_Whenever, the term 'app' or application is used, we are referring to the end user
mobile application built in Flutter._

##### Message Passing

_The specific endpoints mentioned in this section are found in the README.md of the 
codebase._

Mobile clients running NudgeMe are considered to be users. 

Users make themselves known to the server by POSTing to an endpoint during the 
initial setup. This request will contain the user's identifier (which is a random,
unique string) along with a random password, generated on device. For future 
requests, the user must send this password to authenticate themselves.
(This is to prevent anyone from requesting data which is not meant for them.)

Users can add each other in two ways, but these are specific to the use of
encryption, so will be described in the next section.

Now, if User 1 wishes to send data to User 2, User 1 sends POSTs to an
endpoint on the server with the following contained in the JSON
request data:
1. Sender's identifier
2. Receiver's identifier
3. Sender's password 
4. The data itself

This will be stored in a database of pending messages.

Periodically, users POST to another endpoint requesting any pending messages.
This will occur every 15 minutes (due to restrictions on how often we can
execute background code on device). So for example, User 2 will send this
request and receive the data User 1 has sent. Note that the data is stored
as a JSON data type in the database, so the data format is easy to change
and is determined by the clients, not the server.

##### Asymmetric/Public Key Encryption

Our app uses [public key encryption](https://en.wikipedia.org/wiki/Public-key_cryptography)
to provide confidentiality, so end users
do not have to trust in the server. They would only have to trust that the
mobile application correctly implements the cryptographic procedures, which is
easy to verify since our app is open source[^3].

During initialization of the app, an RSA public/private key pair is generated
and stored locally for that user.

To encrypt data to be sent to another user, the receiver's public key is needed.
This is the main purpose of requiring users to add each other; it is a way to
exchange identity strings and public keys.
To add someone to your network, you could scan their QR code, or click on their
add friend link which they will send you, but these are implementation details.

Now assuming User 1 has added User 2, before sending the request to the server
the mobile client can encrypt the data using User 2's public key.
Note that this isn't necessary, it is up to the mobile clients to determine
if they wish to encrypt or not. Currently, I use two features of the app to demonstrate
these two options, sending wellbeing data uses encryption but sending step goals
does not. However they both use the message passing infrastructure.

This decouples the client from the server and makes it easier to change either of
them if needed.

[^2]: In the context of this architecture, the term 'messages' just refers to some
      data that some client wishes to send to another, and which they have both
      agreed the format of.

[^3]: The server is also open source, however, there is no guarantee for the user
      that a server is actually running the code that it claims to run.
      On the other hand, you can always inspect a mobile application running
      locally on your device.

##### Sequence Diagram

Here is the sequence diagram for Bob sending Alice wellbeing data.

<img src="https://user-images.githubusercontent.com/46009390/111034657-9b9b8000-840e-11eb-8c2e-7cf230c3b103.png"
alt="Sequence diagram of wellbeing sharing"
/>

Note that as described previously, the mobile client checks for pending messages
every 15 minutes, so it's only a convenient coincidence that in the diagram
Alice made this check directly after Bob sent his message.

## Backend UML Class Diagram

Although Go has limited OOP features compared to some languages, it still supports
interfaces. Here I define an interface of a `DataSource` which has the methods I
need to interact with the database. This is easier to work with than only using
raw SQL.
Below the interface are two implementations (or 'realizations' in UML terms) of 
the interface. `MyDB` holds a connection to a database and is the actual one we
use whereas the other is a mocked database object which we use in unit testing.

<img src="https://user-images.githubusercontent.com/46009390/111036466-3b5d0c00-8417-11eb-954e-d84d13f0a195.png"
alt="UML Diagram of back-end database"
/>

_Note: the data types used in the diagram are from Go._

## Data Storage

The mobile app stores data through a SQLite database on the device whereas the back-end 
stores data through a MySQL database.

### Back-end Schema/ER Diagram

<img src="https://user-images.githubusercontent.com/46009390/111037852-dfe24c80-841d-11eb-8b73-bce6b650202f.png"
alt="ER diagram of the back-end database."/>

The scores table is where we store data used for the wellbeing visualization.
The other tables are used for network sharing.

# Deployment Strategy

The main part that needs to be 'deployed' is the back-end Go server, which needs to be
running before end-users install and setup the Flutter mobile application. (The
mobile application doesn't *need* to be deployed to app stores, since one could
just distribute pre-built APKs or APIs.)

Since there only needs to be a single server, we don't need to use container
orchestration like Kubernetes, and consequently do not need to dockerize the
backend.

However, we still need a convenient way to manage redeployments instead of finding
and killing the PID and manually executing the binary again. Therefore, we
decided to use `systemd` to manage a service called `nudgeme.service`, which we define.
(The previous version/team appeared to use GNU `screen` but this would be dependent on
SSH sessions.)
Using `systemd` is also useful for these reasons:
- Automatic restart in case our program crashed.
- Restarts our program in case the server rebooted.
- Holds relevant environment variables in one specific file (the unit file).

# Deployment Manual

## Mobile Client

### Android

1. Install flutter, and use `flutter doctor` to check if it's set up correctly.
2. Run `flutter build apk -t lib/main_production.dart` in the project directory.
This builds the production version, meant for end users. It does not display the
dev screen or send remote error reports. For the version used during development,
simply run `flutter build apk`.
3. Install the apk on an Android device by copying the file to the device and
selecting it.

### iOS

To build a signed ipa, you will need a paid Apple Developer account and a Mac computer.

If you have both of these and have installed flutter (type 'flutter doctor' in the terminal to check there are no issues here), do the following:
1. Open Xcode and open this project by locating the project in Finder and opening the *.xcodeproj file.
2. Select Generic iOS Device as your project's device target (Product > Destination and then choose Generic iOS Device option).
3. In the Product menu, select Clean.
4. In the Product menu, select Archive. When the archiving process completes, you will see your application listed under Archives.
5. Select your application and click Export button on the right. 
6. When prompted for an export method, select iOS App Store to upload the app to the iOS App Store, Ad Hoc for internal distribution of the app, Enterprise for distribution outside the App Store, or Development for testing. 
7. Set these Distribution options:
    - Set App Thinning to None.
    - If you are building for app store, select Rebuild from Bitcode. Deselect if not.
    - Select Strip Swift symbols to reduce app size. This is optional.
    - Deselect Include manifest for over-the-air installation.
9. Select your Distribution Certificate and Provisioning Profile (Automatic or Manual). This will generate the .ipa file. 
10. When the file generation process completes, click Export and choose where to save the .ipa file.

## Back-end

_Note: it is currently deployed on our client's server._

You need an installation of `go` (e.g. using your package manager). You can verify
you have it with `go version`.

Follow these steps on the Linode server:
- Clone or pull the repo into your home directory.
- `cd` into `team26-nudgeme-backend` and `go build` in that project directory.
- Modify the `/lib/systemd/system/nudgeme.service` to point to the `nudgeme` 
binary just created. The relevant variable is `ExecStart`.
- Start with `sudo systemdctl start nudgeme` or restart the systemd service with
`sudo systemctl restart nudgeme` (*if it is already running*).

Of course, this can be done on any server, but *you'd need to set up your own
`nudgeme.service` file and SQL database connection*. An example `nudgeme.service`
file is given below. For the SQL database, see the backend database schema. If
you wish to change the server which hosts the SQL database, please modify the
`ADDRESS` variable in `main.go`.

You can modify the nudgeme.service just like any systemd service, e.g. if you want to change
where it searches for the binary.
The service config file is located in `/lib/systemd/system/nudgeme.service`.

Current domain that links to the server:
`https://comp0016.cyberchris.xyz/`.
This is retrieved from the environment variable in the `nudgeme.service` file.

### Example `nudgeme.service` file

This is the service file currently in use on the Linode server, except, in the
actual file I use the actual password instead of '$PASSWORD' as below.

Also note the domain name variable, this would need to be changed with a 
new domain name.

```
[Unit]
Description=back-end for NudgeMe
Documentation=https://github.com/thevirtuoso1973/team26-nudgeme-backend
After=network.target

[Service]
WorkingDirectory=/home/ct/team26-nudgeme-backend
Type=simple
User=root
ExecStart=/home/ct/team26-nudgeme-backend/nudgeme
Restart=on-failure
Environment="SQL_PASSWORD=$PASSWORD"
Environment="DOMAIN_NAME=comp0016.cyberchris.xyz"

[Install]
WantedBy=multi-user.target
```
