---
title: "☑️ Evaluation"
description: "Evaluating our achievements and development process."
layout: single
image: "images/evaluation.jpg"
date: 2021-03-09
draft: false
---
# Summary of Achievements
## Completion of Requirements 

| Requirement                                                                                      | Must/should/could have?  | Completed?  | Contributors   |
|--------------------------------------------------------------------------------------------------|--------------------------|-------------|----------------|
| The system must have the same functionality as version 1, omitting features no longer relevant.  | Must have                | Yes         | Saachi, Chris  |
| The system must have the same interface on Android & iOS.                                        | Must have                | Yes         | Saachi, Chris  |
| Well documented codebase.                                                                        | Must have                | Yes         | Saachi, Chris  |
| Easily maintainable codebase.                                                                    | Must have                | Yes         | Saachi, Chris  |
| Nudge user to share their graph as a PDF if their score falls twice over any two weeks.          | Must have                | Yes         | Chris          |
| Also nudge user if there is no step count in over two days.                                      | Must have                | Yes         | Chris          |
| The weekly wellbeing score must be gathered from the user at Sunday 12pm (by default).           | Must have                | Yes         | Saachi, Chris  |
| Ask the user for consent to collect their wellbeing data.                                        | Must have                | Yes         | Saachi, Chris  |
| If consented, share the user’s wellbeing data by POSTing to a server.                            | Must have                | Yes         | Chris          |
| Passively collect movement data from pedometer.                                                  | Should have              | Yes         | Saachi, Chris  |
| Display a graph that cross references pedometer and wellbeing data.                              | Should have              | Yes         | Chris          |
| Allow users to securely send their wellbeing data to other users (e.g. through e2e encryption).  | Could have               | Yes         | Chris          |
| Facilitate adding users to their network in a convenient way, considering lockdown/remote work.  | Could have               | Yes         | Chris          |
| Allow users to nudge other users through the app.                                                | Could have               | Yes         | Saachi, Chris  |
| Design the system for a user aged between 13 & 99.                                               | Should have              | Yes         | Saachi, Chris  |
| Present an accessible colour scheme to those who are colour-blind.                               | Could have               | Yes         | Saachi, Chris  |

We have completed 100% of the key requirements ('must have' and 'should have'). 
We have completed 100% of the optional requirements ('could have').

## A list of known bugs

We managed to fix almost all of the bugs that we encountered in our application. 

However, two issues remain due to time limitations:
1. Occasionally, the Wellbeing circle coach mark will drag and end up off-centre. - _Low Priority_
2. The weekly wellbeing check notification is dismissible, which means the user 
may accidentally close it without doing their weekly check. This could then lead to publishing old data to the server. - _Medium Priority_

## Individual Contribution Distribution Table
| Work package            | Saachi                                           | Chris                                                 |
|-------------------------|--------------------------------------------------|-------------------------------------------------------|
| Project Partner Liaison | 30                                               | 70                                                    |
| Requirement analysis    | 40                                               | 60                                                    |
| Research                | 50                                               | 50                                                    |
| UI design               | 60                                               | 40                                                    |
| Programming             | 30                                               | 70                                                    |
| Testing                 | 10                                               | 90                                                    |
| Development blog        | 50                                               | 50                                                    |
| Report Website          | 50                                               | 50                                                    |
| Video Production        | 80                                               | 20                                                    |
| Overall contribution    | 45                                               | 55                                                    |
| Roles                   | Front End developer, UI Designer, & Video Editor | Full Stack Developer, Software Architect, & Team Lead |

# Critical Evaluation
## User interface
 <img width="200" alt="ui 2" src="https://user-images.githubusercontent.com/55795994/111216907-e2cf6f80-85cc-11eb-99ff-c3e9a4113399.PNG"> <img width="200" alt="ui 2" src="https://user-images.githubusercontent.com/55795994/111216913-e3680600-85cc-11eb-8e2f-e97395f932da.PNG"> <img width="200" alt="ui 1" src="https://user-images.githubusercontent.com/55795994/111216916-e4993300-85cc-11eb-80a5-1e13c3ef6699.PNG"> <img width="200" alt="ui 1" src="https://user-images.githubusercontent.com/55795994/111216896-e19e4280-85cc-11eb-8f3e-6b1c871f2019.PNG">

Our user interface implements the design principles of _Visibility, Feedback and Affordance_. The first two are reflected by each button containing a clear symbol or a few words of explanation and the obviously interactive features in the Wellbeing Diary, Support Network and Settings (respectively). Affordance is implemented by how NudgeMe provides methods of keeping track of one’s own wellbeing and sharing it but these can be used flexibly by the user in whichever way suits them best. The UI   was praised by our testers for its simplicity. The wellbeing score circle and the step goal progress animation are 2 UI elements that we created from scratch, making the NudgeMe UI unique and memorable.

However, it could be more consistent with button colours as the buttons on the more recently implemented pages did not get changed from the default light blue colour (they should have been changed to our theme colours). If we had time, an unread symbol to indicate an unseen step goal also would have been a nice addition. Additionally, using a URL shortener for the deep link would prevent any confusion caused by the long and unfamiliar link. 

Since our application’s target group has a broad range of ages including older people who may not be as familiar with technology, it is important that the UI was simple, clear and easy to use, and I believe we did achieve this. 

Overall, we believe our UI is _good_.

## Functionality

- The application we are delivering covers 100% of the MoSCoW requirements. The 
application has been tested on users by the team and feedback has shown that NudgeMe fulfils the intended functionality. 
- We proposed and delivered an innovative way to connect with others privately 
(through our network sharing architecture), which extended the scope of the original requirement. 
- We provide multiple ways in which the user could engage in the main interactions of our app. For example,
to add a friend they can scan a QR code or they can tap on their friend's deeplink. To share their
wellbeing graph, they can share a generated PDF or share it in-app with someone in their network.

Therefore, we believe the functionality of our app is _very good_.

## Stability

As we walked through and tested the application, we ensured that even minor 
rendering bugs (e.g., due to screen sizes), were fixed. In addition, although 
we have not migrated to using Dart’s null safety (due to it being released 
near the end of the project), Sentry’s remote error reporting allowed us to 
track and fix many null pointer issues. Therefore, the final application is 
very stable and does not suffer from any crashes. 

We believe the application’s stability is _very good_. 

## Efficiency

We profiled the mobile application using integration tests with Flutter. This 
provided us with concrete data to determine if the application UI rendered 
smoothly. (In this case, ‘efficiency’ would directly translate to a smoother 
UI.) Our results showed that we had average build times of less than 16ms, 
translating to a framerate of about 60 FPS. One area of improvement may be to 
perform more profiling extensive tests, as there are parts of the UI we did 
not test rigorously (i.e., analysing frame build times). 

For the back-end visualization, we were pleased with the GTmetrix score of a 
B, which is much higher than the previous version. Having Google Maps embedded in a 
webpage usually reduces performances noticeably, which is why a score of “B” 
is more than satisfactory. 

Therefore, we believe the efficiency of the overall system is very good. 

## Compatability
<img width="800" alt="ui 1" src="https://user-images.githubusercontent.com/55795994/111227051-e74e5500-85d9-11eb-9d31-b6dc1d35bf79.png">

Flutter supports versions upward of iOS 8 and API 20. Throughout development, we tested the application on 2 iPhone 6's with iOS 13.6 and iOS 14.4, and 2 Android devices. Our testers also had different versions of iPhones. On all these devices, we ensured the UI and functionality were preserved. Since we did not have devices older than these and the simulators only support newer phones, we could not test on older devices than these and if we had, this would have slowed down the development process. 

Therefore, we believe NudgeMe's compatibility is _good_. 

## Maintainability

The core of maintainability is to set up a codebase in such a way that it is 
clear how the architecture of the system works. This makes it easier to 
refactor and/or extend. We believe we have done that. 

The structure of our Flutter codebase is split up into distinct parts, with 
top level files serving as utility code, the model directory holding database 
helpers, the pages directory holding widgets that display pages, etc. Our 
tests also mirror this structure. 

We have commented the codebase thoroughly, and given particular detail to
any sections that may contain subtle or unusual bits of logic.
For one example, we 
[gave a short paragraph of description](https://github.com/UCLComputerScience/COMP0016_2020_21_Team26/blob/67106460bcc6e293d6148fe3e248db245c969455/lib/pages/support_page.dart#L166-L171)
to explain the use of a certain widget on the support page.

One possible inconvenience that may arise from maintaining or extending
our codebase is that it *may* first need to be migrated to use the latest
Flutter/Dart null safety features before any changes could be made. This is because
the null safety feature was released *after* we had finished our development 
process (early March 2021). Regardless, it's not *necessary* to be migrated, but
would be recommended to take advantage of the latest bug fixes or features
from the *dependencies* we use.

Overall, we believe NudgeMe’s maintainability is quite good.

## Project Management

We heavily utilised GitHub’s issue tracker on the central repository. We had 
custom labels defined, such as “priority-high” or “bug”, to quickly assess the 
importance and general workload pending for that week.

<img width="800" alt="bug" src="https://user-images.githubusercontent.com/55795994/111233555-2209ba80-85e5-11eb-89b0-67028a9e6d57.png">

We also self-enforced a pull request + code review strategy when adding code 
to the main repository. This helped pick up any bugs and ensured that the 
other team member was aware of the change. 

In addition, we held a weekly stand-up to self-evaluate our progress for that 
week, assign tasks for the next week and re-evaluate the long-term goal of the project, if needed. 

We believe our project management was very good. 

# Future work

Given additional development we could perform the following improvements: 

- We could expand the application to track further attributes of a user. One of 
the goals of NudgeMe is to assist the user in determining what parts of their 
life may improve their wellbeing. We initially did not track metrics such as 
number of phone calls or messages, since these kinds of data may be considered 
sensitive to the user. However, with the development of our e2e encrypted data 
sharing, the user may be more comfortable sending and receiving sensitive data. 
- We would migrate our application to use Dart’s new null safety feature, 
eliminating a significant class of bugs.
- We could integrate a continuous testing service, like coveralls.io, to display
branch coverage and expand our test suite to hit some branch coverage target,
such as 90%. (Flutter only generates line coverage.)
- Use a URL shortening service like [bitly](https://bitly.com) to make our
deeplinks more user friendly. This could be done by performing an API call to bitly to
shorten the existing deeplink before sending the SMS message or opening the
native “Sharesheet”.

<img style="padding-top: 20px; padding-left: 25px;" width="240" alt="Bitly logo" 
src="https://cdn.freebiesupply.com/images/large/2x/bitly-logo-transparent.png">
- Possibly integrate Google’s Firebase service for real time push notifications,
deeplink generation and URL shortening. This would be an overhaul of the
architecture, potentially removing the need for our backend Go server.

<img width="360" alt="Firebase logo" src="https://firebase.google.com/images/brand-guidelines/logo-standard.png">
