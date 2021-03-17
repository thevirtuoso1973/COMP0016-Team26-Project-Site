---
title: "Appendices"
description: "Miscellaneous content."
layout: single
image: "images/manual.png"
date: 2021-03-09
draft: false
---

Our build(s) are located in the [Github releases](https://github.com/UCLComputerScience/COMP0016_2020_21_Team26/releases)
of our repo. [Here](https://github.com/UCLComputerScience/COMP0016_2020_21_Team26/releases/download/v1.4.4/app-release.apk)
is the latest APK (at the time of writing). 

Our deployment manual is located on the system design page.

# Individual Contribution Distribution Table

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

# User Manual

Located [here](https://uclcomputerscience.github.io/COMP0016_2020_21_Team26/pdfs/usermanual.pdf).

# Legal Issues & Processes

## Software License

All of the *build dependencies* for our mobile client are licensed
under (either) MIT, Apache or BSD (permissive licenses).
NudgeMe itself is licensed under AGPL-3.0, which includes the Go backend
and the Flutter mobile app. Here is the full list of dependencies:

| Package Name                | License |
|-----------------------------|---------|
| http                        | BSD     |
| flutter_local_notifications | BSD     |
| pedometer                   | MIT     |
| timezone                    | BSD     |
| workmanager                 | MIT     |
| pdf                         | Apache  |
| printing                    | Apache  |
| clock                       | Apache  |
| permission_handler          | MIT     |
| encrypt                     | BSD     |
| pointycastle                | MIT     |
| random_string               | BSD     |
| qr_code_scanner             | BSD     |
| cron                        | BSD     |
| sentry_flutter              | MIT     |
| url_launcher                | BSD     |
| uni_links                   | BSD     |
| share                       | BSD     |
| settings_ui                 | Apache  |
| contacts_service            | MIT     |
| flutter_sms                 | MIT     |
| provider                    | MIT     |
| shared_preferences          | BSD     |
| sqflite                     | MIT     |
| charts_flutter              | Apache  |
| introduction_screen         | MIT     |
| highlighter_coachmark       | MIT     |
| qr_flutter                  | BSD     |
| liquid_pull_to_refresh      | MIT     |
| convex_bottom_bar           | Apache  |
| sleek_circular_slider       | MIT     |
| flutter_slidable            | MIT     |
| cupertino_icons             | MIT     |
| testify                     | MIT     |

## Data Protection/GDPR

There are two distinct ways in which data is involved in our application:
data is collected for a visualization, and data is stored temporarily to pass
onto another mobile client.

### Data for Wellbeing Visualization

NudgeMe passively collects wellbeing data & steps, after the user has consented.
They can revoke their consent at any time in the Settings page.

The data collected is anonymised such that there is no way to determine with
certainty who the original individual was, given some data point.
Therefore, since the data subject is no longer identifiable, the GDPR
does not apply[^data].

[^data]: https://www.ucl.ac.uk/data-protection/guidance-staff-students-and-researchers/practical-data-protection-guidance-notices/anonymisation-and

### Network Sharing

We use end-to-end encryption when users share wellbeing data with others
in their network, to give the user reassurance that no-one except the desired
receiver can read that piece of data.
This reassurance is useful if, for example, a user suspected a server was 
(maliciously or otherwise) logging their IP addresses.
However, we do not do this (log IP addresses or similar data), and therefore have no 
personal data stored on the server. (Of course, many users may not trust that previous
sentence which is why we have e2e encryption in the first place.)

Furthermore, even if all data was unencrypted and stored on the server. The
*identifiers* we use are random strings generated from that installation[^fingerprint] of
NudgeMe. This can therefore be treated as pseudonymization.
However, the mobile client/user *themselves* are initially *the only party that can re-identify
the data* (i.e. reverse the pseudonymization). By design, if two users add each other
to their network, they can "re-identify" each other, but we (the server) are unable 
to make that link between the identifier string and an actual person.

[^fingerprint]: Specifically, after NudgeMe is set up, a keypair is generated
                and the user's identifier is derived from the public key
                as a fingerprint. Since the initial public key is random,
                the fingerprint or identifier is essentially random.

# Development Blog

Can be found [here](https://uclcomputerscience.github.io/COMP0016_2020_21_Team26/).
