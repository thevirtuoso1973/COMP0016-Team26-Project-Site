---
title: "🔎 Research"
description: "Researching ideas."
date: 2021-03-01
draft: false
layout: single
image: "images/research/small-research.png"
---

## Related Projects Review

We found two phone applications that bore a resemblance to our NudgeMe requirements. 

One is a free mental wellbeing app called *MyPossibleSelf*, available on both iOS and Android. 

<img src="https://user-images.githubusercontent.com/55795994/111619117-11bc3000-87dd-11eb-85cf-a15c0e43e75f.png" 
alt="MyPossibleSelf" 
width="700"/>

### MyPossibleSelf

_Mental health/wellbeing phone app._

#### What is MyPossibleSelf?

It _tracks daily mood_ and allows users to _document_ how they are feeling using tags. It also provides _‘series’_ on factors that affect wellbeing, such as sleep, anxiety, work stress and depression. 

These series include:  

- Quizzes (e.g. "Exploring my anxiety").

- Affirmations for different situations (e.g. feeling insecure, anxious etc.)

- Video guides containing tips. These are free  dfor 1 month. 

- Options to set reminders for themselves.

- Options to track the factors mentioned amove (sleep, anxiety, exercise...) alongside daily mood. 

- External resources.  

#### What we learned from MyPossibleSelf

- Using notifications to remind users encourages consistent/daily use. Notifications are useful for applications that rely on users logging how they are feeling.

- Daily tracking 4 to 5 things can take up a lot of the user’s time and energy, which can be discouraging.

- Too many colours and sections can be confusing. It is hard to remember the path to each section. 

- Free services become in-app purchases after some time, which makes the application not widely accessible.


The second is a free app available on both iOS and Android that connects to the popular fitness smart-watch, the FitBit.

<img src="https://user-images.githubusercontent.com/55795994/111070611-710efd00-84ca-11eb-84b6-0640528ad65c.png" 
alt="Fitbit 1" 
width="700"/>

### FitBit: Health and Fitness
_Steps and health tracker phone app._

#### What is FitBit: Health and Fitness?
It tracks steps, bpm, sleep based on data from FitBit watch. Users can also track weight by logging it manually. 

It provides the following: 

- ‘Challenges’ e.g. completing a certain number of steps or family step competitions
- 'FitBit coach’: exercise videos involving cardio, yoga etc. 
- ‘Guided programs’: courses to encourage more exercise or a change of habits e.g. ‘Habits for restful sleep: a 2 week course’ and ‘Simple Beginner Running: 3 week course’ 

#### What we learned from FitBit: Health and Fitness

- Having only 3 tabs makes it easy to navigate between sections.

- The app is free but requires owning a Fitbit watch which ranges from £80-120. This is not widely accessible.

- They store personally identifiable health data which is unethical and off-putting. 

- It is not possible to track different variables on the same graph. Lacks _Affordance_.

- It seems as if it was only made to improve physical wellbeing and was not made with mental wellbeing in mind. This is because it presents exercise as a competition rather than self improvement. This is not effective for people who struggle with their mental health and just need to be encouraged to move at all. 

- Weight loss tracking can endanger people who suffer from disordered eating. This may discourage this group of users from FitBit: Health and Fitness.

<img src="https://user-images.githubusercontent.com/55795994/111070614-73715700-84ca-11eb-98ee-0cb5d571a19d.png" 
alt="Fitbit 2" 
width="700"/>

## Technology Review
<img width="600" alt="devices" src="https://user-images.githubusercontent.com/55795994/111075349-8fcbbe80-84df-11eb-9062-27ba0e450808.png">

### Solutions 

Possible solutions include a web app or a phone app (for iOS and/or for Android).  

We concluded that having a web app would not be very useful. Phone apps are more suitable for a wellbeing and exercise application as most people carry their phones around all the time. Therefore:

* A phone app _can count steps whilst the application is not open_ (making the step levels much more accurate). Users would be unlikely to keep a web app open on their phone to allow step counter to count steps throughout their week. While having a web app would make NudgeMe accessible through more devices, desktop computers do not tend to contain pedometers or motion sensors so this would not be useful. 

* _Notifications_ on a phone app are more likely to be seen and addressed. Users would be unlikely to log their wellbeing into a web app without being prompted. 

### Devices 

Our app can be deployed to both Android and iOS phones, as most people in the UK have these devices. As 
shown in the graph below: 

<img width="800" alt="Market share of mobile devices" src="http://students.cs.ucl.ac.uk/2020/group26/images/mobileOS.png">


We used Linux and Mac laptops to develop/test on each of these platforms.

### Programming languages, Frameworks and Libraries 
<img width="800" alt="languages and frameworks" src="https://user-images.githubusercontent.com/55795994/111075143-7fffaa80-84de-11eb-89bb-605b5fd841bb.png">

The _programming languages and frameworks_ that we considered using included: 

- _Multiplatform Kotlin_ for shared business logic, _Kotlin/Swift_ for Android/iOS UI code
- _Javascript/React Native_ for both Android and iOS 
- _Dart/Flutter_ for both Android and iOS, which we used.

Multiplatform Kotlin development is a good choice for handling applications with complex logic, and constantly changing business requirements. The downside is the need to write custom UI code in Kotlin (for Android) and Swift (for iOS), which would require carefully co-ordinated UI designs between sub-teams. These two points directly oppose our actual development use cases: our requirements are (mostly) fixed, with (relatively) simple business logic yet it is a strong requirement to have high quality, consistent interfaces between platforms. 

The other two options were Dart/Flutter and React Native. While both seemed like good options, Flutter seemed more suitable for this project, as our team consisted of people with varying experience (some in front-end, some in back-end) and languages (Python, Dart, Kotlin, Swift, React Native).  Additionally, while React Native has a much bigger community of programmers and consequently better online support, Flutter is compiled with a C library, which is closer to machine language and therefore has better native performance[^1]. Lastly, the whole team either wanted to learn Flutter or to gain more experience with Flutter. Thus the language Dart within the Flutter framework seemed to be the most suitable for building NudgeMe. 

#### Back-end

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/d/d9/Node.js_logo.svg/1920px-Node.js_logo.svg.png" 
alt="Node.js logo" 
width="200" style="white-space: nowrap;"/>
*versus*
<img src="http://cdn.codesamplez.com/wp-content/uploads/2015/12/golang.png" 
alt="Golang Mascot" 
width="200" style="white-space: nowrap;"/>

From version 1 of the app, there was an existing `node.js` backend that 
generated and served a visualization of the wellbeing data stored on the 
database. 

Since we anticipated that we would need to make some changes or build some 
additional features with it, we decided to rewrite it in `Go`. This is 
preferable since it is strongly typed and generally more performant than node.js[^node-go]. 

The core of the original (`node.js`) backend could fit into a single file, so 
`node.js` may be suitable for the scope of the *original* idea. However, as the 
complexity of our backend grew somewhat, we were only able to confidently 
refactor and build features *due to the strength of the Go language*, which
may not have been possible if we had stuck with `node.js`.

#### Libraries

The code below is from our `pubspec.yaml` file. This contains the names and versions of all the Flutter libraries that we used, separated into the categories util, data-related and UI. 

The Flutter *community* (not necessarily the Flutter dev team) are the main source
of development for these libraries, so we carefully evaluated the use of each one
to ensure they were maintained and of high quality.
```
dependencies:
  flutter:
    sdk: flutter

  # util
  http: ^0.12.2
  flutter_local_notifications: ^3.0.2
  pedometer: ^2.0.2
  timezone: ^0.5.9 # needed for scheduling notifications
  workmanager: ^0.2.3
  pdf: ^1.13.0
  printing: ^3.7.2
  clock: ^1.0.1 # useful for testing
  permission_handler: ^5.0.1+1
  encrypt: ^4.1.0 # high-level API
  pointycastle: ^2.0.1 # used for keygen
  random_string: ^2.1.0
  qr_code_scanner: ^0.3.0
  cron: ^0.2.4
  sentry_flutter: ^4.0.4 # error monitoring
  url_launcher: ^5.7.10
  uni_links: ^0.4.0
  share: ^0.6.5+4
  settings_ui: ^0.6.0
  contacts_service: ^0.4.6
  flutter_sms: ^2.1.1

  # data-related
  provider: ^5.0.0
  shared_preferences: ^0.5.12+4
  sqflite: ^1.3.2+1

  # UI
  charts_flutter: ^0.9.0
  introduction_screen: #forked the intro screen package to add a scrollbar
    git:
      url: https://github.com/saachipahwa/introduction_screen.git
  highlighter_coachmark:  ^0.0.3
  qr_flutter: ^3.2.0 # generates a QR code
  liquid_pull_to_refresh: ^2.0.0
  convex_bottom_bar: ^2.6.0
  sleek_circular_slider: ^1.2.0+web
  flutter_slidable: ^0.5.7
  ```

Below are explanations of some of the libraries we used, and how we evaluated them.

#### Utility Libraries

- [Flutter local notifications](https://pub.dev/packages/flutter_local_notifications)
    <img src="https://user-images.githubusercontent.com/55795994/111074226-f1892a00-84d9-11eb-8026-2c63e4e54f18.png" alt="notification screenshot" width="250"/>
    - A popular flutter library used to schedule push notifications on both platforms.
    - We chose this due to its popularity and clear, extensive documentation.
    - It is also part of the 'Flutter Favorites'[^fav] program, which means Flutter recommendeds using it.
        
- [Pedometer](https://pub.dev/packages/pedometer)
    <img src="https://user-images.githubusercontent.com/55795994/111074369-812ed880-84da-11eb-9071-cfae7dd98922.png" alt="step progress circle" width="150"/>
    - We initially considered writing our own native code to deal with the step counter, however, we found `pedometer` instead.
    - It provides access to the cumulative steps through a stream.
    - After evaluating the codebase of this plugin, we determined that it was simple enough to allow us to dig into the codebase
      and make our own changes if it was needed. 
    - We needed to verify this since it was not a particularly well-known or popular plugin, so we double-checked the
      quality of the codebase.

- [Encrypt](https://pub.dev/packages/encrypt) & [Pointy Castle](https://pub.dev/packages/pointycastle)
  - There are many cryptography libraries, and care has to be taken when
    choosing one. With cryptography procedures, a single bug could void any security guarantees.
  - We decided to go with `pointycastle` since it is a port of a well known cryptography library
    from Java[^bouncy]. Since it is a port, there is less risk of bugs due to 'reinventing
    the wheel'.
  - We then used `encrypt` to provide higher-level APIs to perform the actual 
    encryption/decryption. We chose `encrypt` since it runs on top of `pointycastle`.
  
[^bouncy]: http://bouncycastle.org/
           https://en.wikipedia.org/wiki/Bouncy_Castle_(cryptography)
    
#### Data-related Libraries

- [Provider](https://pub.dev/packages/provider)
  - The approach to managing state which is currently recommended[^state-docs] by Flutter.
  - We also explored and researched other approaches such as `flutter_redux`[^redux] 
    (inspired by the JavaScript state container), `BLoC`[^bloc], and `GetX`[^getx].
  - `flutter_redux` would be a good choice if familiar with the original Redux JS library,
    but we are not.
  - `BLoC` is one of the more complex approaches, that additionally aims to separate business logic from 
    presentation/UI. However, our business logic is relatively straightforward.
  - `GetX` would be the second best choice since it has a very intuitive style
    of managing state. However, it overhauls other parts of the API such as the `Navigator`,
    but we were already satisfied with the existing approach to managing this.
  - Therefore, we decided to use `provider`, which was also a perfect fit
    for the part of the app state we were actually trying to manage - the databases.
    (See the implementation section for further explanation.)
- [Shared Preferences](https://pub.dev/packages/shared_preferences)
  - A key-value store inspired by Android's SharedPreferences.
  - Recommended by the Flutter team.

[^state-docs]: https://flutter.dev/docs/development/data-and-backend/state-mgmt/simple
[^redux]: https://pub.dev/packages/flutter_redux
[^bloc]: https://bloclibrary.dev/
[^getx]: https://pub.dev/packages/get

#### UI Libraries

- [Introduction Screen](https://pub.dev/packages/introduction_screen)
    - We chose this package because this introduction screen format seemed suitable for our onboarding process, and fit the designs we had in mind.
    - We did encounter issues with widgets being cut off on smaller screens. We fixed this by [forking the repo](https://github.com/saachipahwa/introduction_screen) and wrapping the `IntroContent` (in the `IntroPage` file) with the `Scrollbar` widget. This widget presents a scrollbar on the side of the screen if there are widgets hidden from view. 
    - Below is an example of a page with a scroll bar.

        <img width="150" alt="scrollbar" src="https://user-images.githubusercontent.com/55795994/111074837-e4216f00-84dc-11eb-8ea7-ec7da22f4a80.png">

    - Below is the relevant code:
    
        ``` dart
        child: Scrollbar(
                    isAlwaysShown: true,
                    controller: _scrollController,
                    child: SingleChildScrollView(
                        controller: _scrollController,
                        physics: const BouncingScrollPhysics(),
                        child: IntroContent(page: page),
        ```
      You can view this change on Github [here](https://github.com/saachipahwa/introduction_screen/commit/e08341c5d2955b24697c3fa4df2c766f1bc1701e).

- [Highlighter Coachmark](https://pub.dev/packages/highlighter_coachmark)
    <img width="175" alt="coach mark" src="https://user-images.githubusercontent.com/55795994/111074901-32cf0900-84dd-11eb-8771-ce0b7e5febcb.png">
    - These coach marks are the slides in the tutorials that play when users finish the introduction screen and views the main app pages for the first time and when they press the information button on the Wellbeing page. 
    - We chose this package instead of Tutorial Coach Mark, despite that one having more likes, because we
    preferred the API exposed by `highlighter_coachmark`. It was less verbose and allowed us to
    define the tutorial with fewer lines of code, which contributes to readability.

## References 

[^1]: [Hackr.io: Flutter vs React](https://hackr.io/blog/react-native-vs-flutter)
[^node-go]: https://devathon.com/blog/node-js-vs-or-and-golang/
[^fav]: https://flutter.dev/docs/development/packages-and-plugins/favorites
