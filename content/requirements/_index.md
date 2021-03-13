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

The version that we were given was version 2: NudgeMe. NudgeMe is instead aimed at the general UK public - and this change was motivated by the COVID pandemic as it has put the mental wellbeing of the general public at risk since everyone is isolated. We were asked to rebuild the app but focusing only wellbeing and steps as this was the most successful aspect of the previous version, and to also implement a feature where the user gets by a notification that ‘nudges’ them to go for a walk when their score starts to drop.

In CarerCare, there was also a server to which the wellbeing scores of different regions, from users who chose to send them, were visually represented on a map. NudgeMe also had to have this feature, as the NHS would benefit from being able to monitor the wellbeing of people across the country and especially how it is being affected by the pandemic. 

## Project Goals
The aim is to create an application that encourages people to look after themselves, especially in this time where people are isolated and their mental wellbeing is suffering as a result.

The ways in which we were asked to do this is:
- allowing users to keep a weekly record of their wellbeing
- encourage users to go on walks to improve their wellbeing

## Requirements Gathering
Over a few meetings with the client, and using resources such as the Figma of the version 1 app (CarerCare), we began to understand the requirements of this project.

This was a cross-platform mobile app that tracks user’s wellbeing, plots it against their steps, and when their wellbeing drops - the app ‘nudges’ them to go on a walk. 

We conducted a survey of structured questions to confirm these requirements were in the user's interests and to adapt them based on feebdack. The questions we asked in the survey and the response consisted of the following:

| Questions                                                                                           |  Open/Closed            |  Options                  |
|-----------------------------------------------------------------------------------------------------|-------------------------|---------------------------|
| Would you find it useful to monitor your wellbeing over time?                                       | Closed                  | Yes, No, Not sure         |
| Would you find it useful for others (e.g. friends/family) to monitor your wellbeing over time?      | Closed                  | Yes, No, Not sure         | 
| How likely would you be to monitor your wellbeing?                                                  | Closed                  | Daily, Weekly, in between |
| During the first lockdown, what did you do to keep your mental health stable?                       | Open                    | n/a                       |

| Questions 1 and 2                                                                              | Yes  | No   | Not sure |
|------------------------------------------------------------------------------------------------|------|------|----------|
| Would you find it useful to monitor your wellbeing over time?                                  | 92.3 | 7.7  | 0        |
| Would you find it useful for others (e.g. friends/family) to monitor your wellbeing over time? | 76.9 | 15.4 | 7.7      |

| Questions 3                                        | Weekly    | Daily     | In between |
|----------------------------------------------------|-----------|-----------|------------|
| How likely would you be to monitor your wellbeing? | 30.8      | 53.8      | 15.4       |

        
Common answers to Question 4 were texting/calling friends, types of exercise, cooking, various types of arts and crafts.

From this survey, we analysed the closed questions and confirmed interest in the initial requirements. We brainstormed additional features to incorporate activities mentioned in the responses to question 4, and landed on peer-to-peer wellbeing sharing feature within the app, as this would allow people to share their wellbeing with their friends or support network easily and privately.

## Personas
To create the personas, we began with some rough ideas of who our potential users could be (e.g. carers under duress), but after clarifying the requirements with our client, we discovered the application is aimed for use by the entire British population, between age 13 to 99, who have been affected due to lockdown. Therefore, we tried to capture a variety of different personality types that would benefit from an wellbeing app, without being too generic or unspecific.

Here are the personas that we created:

Naima Sultana

<img src="https://user-images.githubusercontent.com/55795994/111051715-27cc9800-844d-11eb-9c74-27e1a9cc0eb7.png" 
alt="Naima persona" 
width="700"/>


Dorris Dibb

<img src="https://user-images.githubusercontent.com/55795994/111051710-256a3e00-844d-11eb-8c50-0cfa0a56c516.png" 
alt="Dorris persona" 
width="700"/>


John Smith

<img src="https://user-images.githubusercontent.com/55795994/111051714-27340180-844d-11eb-8971-709f0b8fe731.png" 
alt="Dorris persona" 
width="700"/>


## Use cases

Our use case diagram:

<img src="https://user-images.githubusercontent.com/55795994/111051716-28652e80-844d-11eb-8024-02f8d6425a73.png" 
alt="Dorris persona" 
width="700"/>

Our use case table can be found [on Google Drive](https://drive.google.com/file/d/1ByhhvDdvM3YLbZacD7vf7w1CJf-8_3VT/view?usp=sharing).

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

## User flow: