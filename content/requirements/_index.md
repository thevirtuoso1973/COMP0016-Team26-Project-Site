---
title: "📋 Requirements"
description: "Requirements gathering and list"
layout: requirements
date: 2021-01-05
image: "images/clients-logo/carefulai.png"
draft: false
---

## Project Background & Client

Our client is Dr Joseph Connor from CarefulAI and the NHS.

<img src="https://user-images.githubusercontent.com/55795994/111075490-0d8fca00-84e0-11eb-9e38-16cd2f262421.png" 
alt="ixn logo" 
width="250"/>

Version one of this project was called Carer Care. CarerCare was a wellbeing app made for carers in South Wales that tracked their wellbeing and plotted it against their steps and the amount that they interacted with their support network. This app aimed to encourage carers to take care of their wellbeing.

Version 2: NudgeMe is aimed instead at the general UK public, a change that was motivated by the COVID pandemic, which has greatly increased feelings of isolation and therefore has put the mental wellbeing of the general public at risk. We rebuilt Version 1, focusing only on wellbeing and steps as this was the most successful aspect of the previous version. We also implemented a feature where the user gets by a notification that ‘nudges’ them to walk when their score starts to drop.

CarerCare's wellbeing scores were sent to a server used to represent scores from different regions on a map visually. NudgeMe also has this feature. We hope that the NHS will benefit from monitoring the wellbeing of people across the country and how it is being affected by the COVID pandemic.

Below are two graphs that display the effect of lockdown on UK adults' mental health and wellbeing[^1].

The graph below shows the increasing rates of loneliness and hopelessness in the UK since mid-March 2020.
<img src="https://user-images.githubusercontent.com/55795994/111076321-c6a3d380-84e3-11eb-8f10-a3ae00ad82e4.png" 
alt="ixn logo" 
width="600"/> 

The graph below shows the decreasing levels of coping very or fairly well with pandemic-related stress.
<img src="https://user-images.githubusercontent.com/55795994/111076384-0a96d880-84e4-11eb-8310-a52e5f590c65.png" 
alt="ixn logo" 
width="600"/> 


## Project Goals
This project aimed to create an application that encourages people to look after themselves, especially in a time where people are isolated, and their mental wellbeing is suffering as a result.

The ways in which NudgeMe does this include:
* Allowing users to keep a weekly record of their wellbeing.
* Encouraging users to go on walks to improve their wellbeing.
    * By plotting their steps on a graph 
    * Allowing them to share this information with their support network 
    * Allowing them to set and receive goals for/from people in their support network 

## Requirements Gathering
We gathered initial requirements over a few meetings with our client and confirmed our understanding by using resources from Version 1, such as the Figma of CarerCare.

In short, these requirements outlined a cross-platform mobile app that tracks user’s wellbeing, plots it against their steps, and when their wellbeing drops - it ‘nudges’ them to go on a walk.

### Survey
We conducted a survey of structured questions to confirm these requirements were in the user’s interests and adapt them based on feedback. We carried this out remotely using Google Forms.

The questions we asked in the survey and the responses consisted of the following:

| Questions                                                                                           |  Open/Closed            |  Options                  |
|-----------------------------------------------------------------------------------------------------|-------------------------|---------------------------|
| Would you find it useful to monitor your wellbeing over time?                                       | Closed                  | Yes, No, Not sure         |
| Would you find it useful for others (e.g. friends/family) to monitor your wellbeing over time?      | Closed                  | Yes, No, Not sure         | 
| How likely would you be to monitor your wellbeing?                                                  | Closed                  | Daily, Weekly, in between |
| During the first lockdown, what did you do to keep your mental health stable?                       | Open                    | n/a                       |

The purpose of the closed questions was to confirm interest in the initial requirements. We aimed to use the responses to question 4 to inspire some additional features.

The following tables show the responses.

| Questions 1 and 2                                                                              | Yes  | No   | Not sure |
|------------------------------------------------------------------------------------------------|------|------|----------|
| Would you find it useful to monitor your wellbeing over time?                                  | 92.3 | 7.7  | 0        |
| Would you find it useful for others (e.g. friends/family) to monitor your wellbeing over time? | 76.9 | 15.4 | 7.7      |

| Questions 3                                        | Weekly    | Daily     | In between |
|----------------------------------------------------|-----------|-----------|------------|
| How likely would you be to monitor your wellbeing? | 30.8      | 53.8      | 15.4       |

Common answers to _Question 4_ were texting/calling friends, various types of exercise, cooking, and various arts and crafts. 

The first answer, texting/calling friends, helped us land on the end-to-end encrypted, peer-to-peer wellbeing sharing as the additional feature to implement. We chose this to allow people to share their wellbeing with their friends or support network privately and quickly.

During the second half of the project, we developed this feature and added the User Nudge, allowing users to send each other step goals. As we made this change later in the project, we created an updated User Flow Figma to ensure the client has an accurate mental map of the application. You can find this at the bottom of this page or[here](https://www.figma.com/proto/53Di5ADgodaHYWmMHXB8xv/NudgeMe-User-Flow?scaling=scale-down&node-id=1%3A10).

## Personas
We began with some rough ideas of who our potential users could be (e.g. carers under duress) to create the personas. After clarifying our client's requirements, we discovered the application is aimed for use by the entire British population (between ages 13 and 99) who have been affected due to lockdown. Therefore, we tried to capture various personality types that would benefit from a wellbeing app without being too generic or unspecific. 

Here are the scenarios and personas that we created:

* _Naima Sultana_ is feeling lonely. She is struggling doing university work by herself without peer support​. She Would like some way for her friends to keep track of her wellbeing.  

<img src="https://user-images.githubusercontent.com/55795994/111051715-27cc9800-844d-11eb-9c74-27e1a9cc0eb7.png" alt="Naima persona" width="700"/>

* _Dorris Dibb_'s mother has a bad memory. Dorris' mother needs to be reminded to keep her steps up, and sometimes gets lonely in her nursing home.​ It would be useful for Dorris to be able to remind her to move and to see how she is feeling.​

<img src="https://user-images.githubusercontent.com/55795994/111051710-256a3e00-844d-11eb-8c50-0cfa0a56c516.png" 
alt="Dorris persona" 
width="700"/>

* _John Smith_ has been laid-off due to budget cuts caused by the COVID-19 pandemic. He is experiencing higher stress + cortisol levels that is decreasing his cognitive performance, thereby further reducing the chance of acquiring future jobs.​ He needs a way to monitor his wellbeing.​

<img src="https://user-images.githubusercontent.com/55795994/111051714-27340180-844d-11eb-8971-709f0b8fe731.png" 
alt="Dorris persona" 
width="700"/>


## Use cases

Below is our use case diagram. It contains every use case and the action or the service that carries it out.

<img width="800" alt="Screenshot 2021-03-14 at 14 15 23" src="https://user-images.githubusercontent.com/55795994/111071807-bda90700-84cf-11eb-8393-0e7e89b6c637.png">

Our use case table can be found [on Google Drive](https://drive.google.com/file/d/1ByhhvDdvM3YLbZacD7vf7w1CJf-8_3VT/view?usp=sharing). 


## MoSCoW list

| Functional Requirements                                                                           | Must/Should/Could have? |
|---------------------------------------------------------------------------------------------------|-------------------------|
| The system must have the same functionality as version 1, omitting features no longer relevant.*  | Must have               |
| The system must have the same interface on Android & iOS.                                         | Must have               |
| Well documented codebase.                                                                         | Must have               |
| Easily maintainable codebase.                                                                     | Must have               |
| Nudge user to share their graph as a PDF if their score falls twice over any two weeks.           | Must have               |
| Also nudge user if there is no step count in over two days.                                       | Must have               |
| The weekly wellbeing score must be gathered from the user at Sunday 12pm (by default).            | Must have               |
| Ask the user for consent to collect their wellbeing data.                                         | Must have               |
| If consented, share the user's wellbeing data by POSTing to a server.                             | Must have               |
| Passively collect movement data from pedometer.                                                   | Should have             |
| Display a graph that cross references pedometer and wellbeing data.                               | Should have             |
| Allow users to *securely* send their wellbeing data to other users (e.g. through e2e encryption). | Could have              |
| Facilitate adding users to their network in a convenient way, considering lockdown/remote work.   | Could have              |
| Allow users to nudge other users through the app.                                                 | Could have              |

| Non functional Requirements                                                                         | Must/Should/Could have? |
|-----------------------------------------------------------------------------------------------------|-------------------------|
| Design the system for a user aged between 13 & 99.                                                  | Should have             |
| Present an accessible color scheme to those who are colorblind.                                     | Could have              |

\*_Since we were adapting the application for a wider audience (general UK 
population) and for a different purpose (to assist the public in maintaining 
their wellbeing), some of the features designed specifically for carers in the Welsh area were no longer relevant._

## References 

[^1]: [Mental Health Foundation - 9 Month Study](https://www.mentalhealth.org.uk/news/nine-month-study-reveals-pandemics-worsening-emotional-impacts-uk-adults)
