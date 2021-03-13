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

## Class Diagram

## Data Storage

### Schema

