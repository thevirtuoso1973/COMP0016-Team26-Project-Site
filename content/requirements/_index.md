---
title: "Requirements"
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
The aim is to create an application that enourages people to look after themselves, especially in this time where people are isolated and their mental wellbeing is suffering as a result.

The ways in which we were asked to do this is:
- allowing users to keep a weekly record of their wellbeing
- encourage users to go on walks to improve their wellbeing

## Requirements Gathering
Over a few meetings with the client, and using resources such as the Figma of the version 1 app (CarerCare), we began to understand the requirements of this project.

This was a cross-platform mobile app that tracks user’s wellbeing, plots it against their steps, and when their wellbeing drops - the app ‘nudges’ them to go on a walk. 

We conducted a survey of structured questions to confirm these requirements were in the user's interests and to adapt them based on feebdack. The questions we asked in the survey and the response consisted of the following:

1. Would you find it useful to monitor your wellbeing over time 
    92.3% yes, 7.7% no, 0% not sure

2. Would you find it useful for others (e.g. friends/family) to monitor your wellbeing over time? 
    76.9% yes, 15.4% no, 7.7% no

3. How likely would you be to monitor your wellbeing?  

    30.8% every day, 53.8% once a week, 15.4% more than once a week but not every day

4. (Open) During the first lockdown, what did you do to keep your mental health stable (e.g. yoga, painting, video calling friends)? 
        
Common answers to 4 were texting/calling friends, types of exercise, cooking, various types of arts and crafts.

From this survey, we analysed the closed questions and confirmed interest in the initial requirements. We brainstormed additional features to incorporate activities mentioned in the responses to question 4, and landed on peer-to-peer wellbeing sharing feature within the app, as this would allow people to share their wellbeing with their friends or support network easily and privately.

## Personas

To create the personas, we began with some rough ideas of who our potential users could be (e.g. carers under duress), but after clarifying the requirements with our client, we discovered the application is aimed for use by the entire British population, between age 13 to 99, who have been affected due to lockdown. Therefore, we tried to capture a variety of different personality types that would benefit from an wellbeing app, without being too generic or unspecific.

Here are the personas that we created:
Naima Sultana
![Persona 1](https://github.com/thevirtuoso1973/COMP0016-Team26-Project-Site/static/images/requirements/naima_persona.png "Naima Sultana")

Dorris Dibb
![Persona 2](https://github.com/thevirtuoso1973/COMP0016-Team26-Project-Site/static/images/requirements/dorris_persona.png "Dorris Dibb")

John Smith
![Persona 3](https://github.com/thevirtuoso1973/COMP0016-Team26-Project-Site/static/images/requirements/john_persona.png "John Smith")

## Use cases
![Use case](https://github.com/thevirtuoso1973/COMP0016-Team26-Project-Site/static/images/requirements/use_case.png "user")

## MoSCoW list
### Function requirements
#### Must have
The system must have same functionality as version 1 omitting the the networks that uses previous look at access via the app. This is to ensure that the application is more generic. 

The system must have have a user interface which is the same for both Android and iOS. 

The system must have a code base that is well documented and annotated and easily maintainable.

People must be nudged to share their wellbeing score as a pdf/jpeg is their score falls twice over any two week period. This will be facilitated. They will also be encouraged to do the same if there is no pedometer reading over two days. 

On a Monday each week they must be asked if they to share their average wellbeing score (in a locally differentially private manner) with a central wellbeing hub. This hub will request put requests in the same manner as the previous App.

The wellbeing score must be gathered at 12 pm on a Sunday.

#### Should have

It should passively gather movement data from the pedometer and cross reference this against a self reported wellbeing score.

#### Could have
The system could have options for connecting it's well-being score to other systems including wearables.

The system could have options for for gathering user-defined preferences for for web sites sounds videos and and text that is meaning for to their general well-being.

### Non-functional requirements
#### Should have
The system should be designed for a user between 13 and 99.
The target user is a person who wishes to share their wellbeing with others.

## User flow
