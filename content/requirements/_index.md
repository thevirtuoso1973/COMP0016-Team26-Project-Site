---
title: "📋 Requirements"
description: "Requirements gathering and list"
layout: requirements
date: 2021-01-05
image: "images/clients-logo/carefulai.png"
draft: false
---

## Project Background & Client
Our client is Dr Joseph Connor from CarefullAI and the NHS.

Version one of this project was called Carer Care. CarerCare was a wellbeing app made for carers in South Wales, that tracked their wellbeing and plotted it against their steps and the amount that they interacted with their support network. The aim of this app was to encourage carers to take care of their wellbeing.

The version that we made is version 2: NudgeMe. NudgeMe is instead aimed at the _general UK public_, a change that was motivated by the COVID pandemic as it has greatly increased feelings of isolation and therefore has put the mental wellbeing of the general public at risk. We were asked to rebuild Version 1, focusing only wellbeing and steps as this was the most successful aspect of the previous version and to implement a feature where the user gets by a notification that ‘nudges’ them to go for a walk when their score starts to drop.

In CarerCare, there was also a server to which the wellbeing scores of different regions, from users who chose to send them, were sent and these were used to visually represented scores on a map. NudgeMe also has this feature. We hope that the NHS will benefit from being able to monitor the wellbeing of people across the country and especially how it is being affected by the pandemic. 

## Project Goals
The aim of this project was to create an application that encourages people to look after themselves, especially in this time where people are isolated and their mental wellbeing is suffering as a result.

The ways in which we were asked to do this is:
* allowing users to keep a weekly record of their wellbeing
* encouraging users to go on walks to improve their wellbeing

## Requirements Gathering
We gathered the requirements for NudgeMe over a few meetings with the client and using resources from Version 1, such as the Figma of the CarerCare.

In short, these requirements outlined a cross-platform mobile app that tracks user’s wellbeing, plots it against their steps, and when their wellbeing drops - it 'nudges’ them to go on a walk. 

### Survey
We conducted a survey of structured questions to confirm these requirements were in the user's interests and to adapt them based on feebdack. We carried this out remotely using Google Forms. 

The questions we asked in the survey and the responses consisted of the following:

| Questions                                                                                           |  Open/Closed            |  Options                  |
|-----------------------------------------------------------------------------------------------------|-------------------------|---------------------------|
| Would you find it useful to monitor your wellbeing over time?                                       | Closed                  | Yes, No, Not sure         |
| Would you find it useful for others (e.g. friends/family) to monitor your wellbeing over time?      | Closed                  | Yes, No, Not sure         | 
| How likely would you be to monitor your wellbeing?                                                  | Closed                  | Daily, Weekly, in between |
| During the first lockdown, what did you do to keep your mental health stable?                       | Open                    | n/a                       |

The purpose of the closed questions were to confirm interest in the initial reqiurements. We aimed to use the responses to question 4 to inspire some additional features.

The responses are shown in the following tables.

| Questions 1 and 2                                                                              | Yes  | No   | Not sure |
|------------------------------------------------------------------------------------------------|------|------|----------|
| Would you find it useful to monitor your wellbeing over time?                                  | 92.3 | 7.7  | 0        |
| Would you find it useful for others (e.g. friends/family) to monitor your wellbeing over time? | 76.9 | 15.4 | 7.7      |

| Questions 3                                        | Weekly    | Daily     | In between |
|----------------------------------------------------|-----------|-----------|------------|
| How likely would you be to monitor your wellbeing? | 30.8      | 53.8      | 15.4       |

Common answers to _Question 4_ were texting/calling friends, various types of exercise, cooking and various types of arts and crafts. This helped us to land on end-to-end encrypted,peer-to-peer wellbeing sharing feature within the app as an additional feature to implement, as this would allow people to share their wellbeing with their friends or support network privately and quickly.

During the second half of the project, we developed this feature and added the User Nudge which allows users to send each other step goals. As this change was made later in the project, we created an updaetd User Flow Figma that reflected the present NudgeMe user flow to ensure the client has an accurate mental map of the application. You can find this at the bottom of this page, or [here](https://www.figma.com/proto/53Di5ADgodaHYWmMHXB8xv/NudgeMe-User-Flow?scaling=scale-down&node-id=1%3A10).

## Personas
To create the personas, we tried to capture a variety of different personality types that would benefit from an wellbeing app without being too generic or unspecific, as the user group for NudgeMe is 13-99 year olds (very broad).

Here are the personas that we created:


<img src="https://user-images.githubusercontent.com/55795994/111051715-27cc9800-844d-11eb-9c74-27e1a9cc0eb7.png" 
alt="Naima persona" 
width="700"/>


<img src="https://user-images.githubusercontent.com/55795994/111051710-256a3e00-844d-11eb-8c50-0cfa0a56c516.png" 
alt="Dorris persona" 
width="700"/>


<img src="https://user-images.githubusercontent.com/55795994/111051714-27340180-844d-11eb-8971-709f0b8fe731.png" 
alt="Dorris persona" 
width="700"/>


## Use cases

Below is our use case diagram. It contains every use case and the action that is taken, or the service that is used, to carry it out.

<img width="800" alt="Screenshot 2021-03-14 at 14 15 23" src="https://user-images.githubusercontent.com/55795994/111071807-bda90700-84cf-11eb-8393-0e7e89b6c637.png">

Our use case table can be found [on Google Drive](https://drive.google.com/file/d/1ByhhvDdvM3YLbZacD7vf7w1CJf-8_3VT/view?usp=sharing). This is 


## MoSCoW list

| Functional Requirement                                                                              | Must/Should/Could have? |
|-----------------------------------------------------------------------------------------------------|-------------------------|
| The system must have the same functionality as version 1, omitting features no longer relevant.[^1] | Must have               |
| The system must have the same interface on Android & iOS.                                           | Must have               |
| Well documented codebase.                                                                           | Must have               |
| Easily maintainable codebase.                                                                       | Must have               |
| Nudge user to share their graph as a PDF if their score falls twice over any two weeks.             | Must have               |
| Also nudge user if there is no step count in over two days.                                         | Must have               |
| The weekly wellbeing score must be gathered from the user at Sunday 12pm (by default).              | Must have               |
| Ask the user for consent to collect their wellbeing data.                                           | Must have               |
| If consented, share the user's wellbeing data by POSTing to a server.                               | Must have               |
| Passively collect movement data from pedometer.                                                     | Should have             |
| Display a graph that cross references pedometer and wellbeing data.                                 | Should have             |
| Allow users to *securely* send their wellbeing data to other users (e.g. through e2e encryption).   | Could have              |
| Facilitate adding users to their network in a convenient way, considering lockdown/remote work.     | Could have              |
| Allow users to nudge other users through the app.                                                   | Could have              |

| Non functional Requirements                                                                         | Must/Should/Could have? |
|-----------------------------------------------------------------------------------------------------|-------------------------|
| Design the system for a user aged between 13 & 99.                                                  | Should have             |
| Present an accessible color scheme to those who are colorblind.                                     | Could have              |

[^1]: Since we were adapting the application for a wider audience (general UK population),
      and for a different purpose (to assist the public in maintaining their wellbeing),
      some of the features designed specifically for carers in the Welsh area were no
      longer relevant.

