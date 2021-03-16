---
title: "☑️ Evaluation"
description: "Evaluating our achievements and development process."
layout: single
image: "images/system-design/gears.png"
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

We have completed 100% of the functional requirements. 
We have completed 100% of the non-functional requirements.

## A list of known bugs
We managed to fix almost all of the bugs that we encountered in our application. 

However, two issues persist:

* Occasionally, the Wellbeing circle coach mark will drag and end up off-centre. 

* The weekly wellbeing check notification is dismissible, which means the user may accidentally close it without doing their weekly check. This could then lead to publishing old data to the server. 

Our team used the GitHub issue tracker to keep track of bugs. As you can see from this screenshot of our issue list (taken on 15th March 2021), there are no open issues with the `bug` label.

<img width="800" alt="bug" src="https://user-images.githubusercontent.com/55795994/111233555-2209ba80-85e5-11eb-89b0-67028a9e6d57.png">


## Individual Contribution Distribution Table
| Work package             | Saachi                                          | Chris                                            |
|--------------------------|-------------------------------------------------|--------------------------------------------------|
| Project partner Liaison  | 30                                              | 70                                               |
| Requirement analysis     | 40                                              | 60                                               |
| Research                 | 50                                              | 50                                               |
| UI design                | 60                                              | 40                                               |
| Programming              | 30                                              | 70                                               |
| Testing                  | 10                                              | 90                                               |
| Development blog         | 50                                              | 50                                               |
| Website                  | 50                                              | 50                                               |
| Video                    | 80                                              | 20                                               |
| Overall contribution     | 45                                              | 55                                               |
| Roles                    | Front End developer, UI Designer, Video Editor  | Client Liaison, Team Lead, Full Stack Developer  |

# Critical Evaluation
## User interface
 <img width="200" alt="ui 2" src="https://user-images.githubusercontent.com/55795994/111216907-e2cf6f80-85cc-11eb-99ff-c3e9a4113399.PNG"> <img width="200" alt="ui 2" src="https://user-images.githubusercontent.com/55795994/111216913-e3680600-85cc-11eb-8e2f-e97395f932da.PNG"> <img width="200" alt="ui 1" src="https://user-images.githubusercontent.com/55795994/111216916-e4993300-85cc-11eb-80a5-1e13c3ef6699.PNG"> <img width="200" alt="ui 1" src="https://user-images.githubusercontent.com/55795994/111216896-e19e4280-85cc-11eb-8f3e-6b1c871f2019.PNG">

Our user interface implements the design principles of _Visibility, Feedback and Affordance_. The first two are reflected by each button containing a clear symbol or a few words of explanation and the obviously interactive features in the Wellbeing Diary, Support Network and Settings (respectively). Affordance is implemented by how NudgeMe provides methods of keeping track of one’s own wellbeing and sharing it but these can be used flexibly by the user in whichever way suits them best. The UI   was praised by our testers for its simplicity. The wellbeing score circle and the step goal progress animation are 2 UI elements that we created from scratch, making the NudgeMe UI unique and memorable.

However, it could be more consistent with button colours as the buttons on the more recently implemented pages did not get changed from the default light blue colour (they should have been changed to our theme colours). If we had time, an unread symbol to indicate an unseen step goal also would have been a nice addition. Additionally, using a URL shortener for the deep link would prevent any confusion caused by the long and unfamiliar link. 

Since our application’s target group has a broad range of ages including older people who may not be as familiar with technology, it is important that the UI was simple, clear and easy to use, and I believe we did achieve this. 

Overall, we believe our UI is _good_.

## Functionality
The application we are delivering covers 100% of the MoSCow requirements. The code is readable, and the backend is easy-to-use and extendable. The application has been tested on users and the team and feedback has shown that NudgeMe fulfils the intended functionality. 

Therefore, we believe the functionality of our app is _very good_.

## Stability

## Efficiency
The performance of our map visualisation is very good.


## Compatability
<img width="800" alt="ui 1" src="https://user-images.githubusercontent.com/55795994/111227051-e74e5500-85d9-11eb-9d31-b6dc1d35bf79.png">

Flutter supports versions upward of iOS 8 and API 20. Throughout development, we tested the application on 2 iPhone 6's with iOS 13.6 and iOS 14.4, and 2 Android devices. Our testers also had different versions of iPhones. On all these devices, we ensured the UI and functionality were preserved. Since we did not have devices older than these and the simulators only support newer phones, we could not test on older devices than these and if we had, this would have slowed down the development process. 

Therefore, we believe NudgeMe's compatibility is _good_. 

## Maintainability


## Project Management


# Future work