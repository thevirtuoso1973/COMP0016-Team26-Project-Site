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
in and read the diagram._

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

##### Message Passing

TODO

##### Asymmetric/Public Key Encryption

TODO

[^2]: In the context of this architecture, the term 'messages' just refers to some
      data that some client wishes to send to another, and which they have both
      agreed the format of.

## Sequence Diagram

## Class Diagram

## Data Storage

### Schema

