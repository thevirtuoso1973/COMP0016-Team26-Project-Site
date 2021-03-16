---
title: "Appendics"
description: "Miscellaneous content."
layout: single
image: "images/system-design/gears.png"
date: 2021-03-09
draft: false
---

Our build(s) are located in the [Github releases](https://github.com/UCLComputerScience/COMP0016_2020_21_Team26/releases)
of our repo. [Here](https://github.com/UCLComputerScience/COMP0016_2020_21_Team26/releases/download/v1.4.4/app-release.apk)
is the latest APK (at the time of writing). Our deployment manual is located below, so you can build the APK or IPA
yourself.

# User Manual

Located [here](https://uclcomputerscience.github.io/COMP0016_2020_21_Team26/pdfs/usermanual.pdf).

# Deployment Manual

## Mobile Client

### Android

1. Install flutter, and use `flutter doctor` to check if it's set up correctly.
2. Run `flutter build apk -t lib/main_production.dart` in the project directory.
This builds the production version, meant for end users. It does not display the
dev screen or send remote error reports. For the version used during development,
simply run `flutter build apk`.
3. Install the apk on an Android device by copying the file to the device and
selecting it.

### iOS

To build a signed ipa, you will need a paid Apple Developer account and a Mac computer.

If you have both of these and have installed flutter (type 'flutter doctor' in the terminal to check there are no issues here), do the following:
1. Open Xcode and open this project by locating the project in Finder and opening the *.xcodeproj file.
2. Select Generic iOS Device as your project's device target (Product > Destination and then choose Generic iOS Device option).
3. In the Product menu, select Clean.
4. In the Product menu, select Archive. When the archiving process completes, you will see your application listed under Archives.
5. Select your application and click Export button on the right. 
6. When prompted for an export method, select iOS App Store to upload the app to the iOS App Store, Ad Hoc for internal distribution of the app, Enterprise for distribution outside the App Store, or Development for testing. 
7. Set these Distribution options:
    - Set App Thinning to None.
    - If you are building for app store, select Rebuild from Bitcode. Deselect if not.
    - Select Strip Swift symbols to reduce app size. This is optional.
    - Deselect Include manifest for over-the-air installation.
9. Select your Distribution Certificate and Provisioning Profile (Automatic or Manual). This will generate the .ipa file. 
10. When the file generation process completes, click Export and choose where to save the .ipa file.

## Back-end

_It is currently deployed on our client's server._

You need an installation of `go` (e.g. using your package manager). You can verify
you have it with `go version`.

Follow these steps on the Linode server:
- Clone or pull the repo into your home directory.
- `cd` into `team26-nudgeme-backend` and `go build` in that project directory.
- Modify the `/lib/systemd/system/nudgeme.service` to point to the `nudgeme` 
binary just created. The relevant variable is `ExecStart`.
- Start with `sudo systemdctl start nudgeme` or restart the systemd service with
`sudo systemctl restart nudgeme` (*if it is already running*).

Of course, this can be done on any server, but you'd need to set up your own
`nudgeme.service` file.

You can modify the nudgeme.service just like any systemd service, e.g. if you want to change
where it searches for the binary.
The service config file is located in `/lib/systemd/system/nudgeme.service`.

Current domain that links to the server:
`https://comp0016.cyberchris.xyz/`.
This is retrieved from the environment variable in the `nudgeme.service` file.

### Example `nudgeme.service` file

This is the service file currently in use on the Linode server, except, in the
actual file I use the actual password instead of '$PASSWORD' as below.

Also note the domain name variable, this would need to be changed with a 
new domain name.

```
[Unit]
Description=back-end for NudgeMe
Documentation=https://github.com/thevirtuoso1973/team26-nudgeme-backend
After=network.target

[Service]
WorkingDirectory=/home/ct/team26-nudgeme-backend
Type=simple
User=root
ExecStart=/home/ct/team26-nudgeme-backend/nudgeme
Restart=on-failure
Environment="SQL_PASSWORD=$PASSWORD"
Environment="DOMAIN_NAME=comp0016.cyberchris.xyz"

[Install]
WantedBy=multi-user.target
```

# Legal Issues & Processes

There are two distinct ways in which data is involved in our application:
data is collected for a visualization, and data is stored temporarily to pass
onto another mobile client.

## Data for Wellbeing Visualization

NudgeMe passively collects wellbeing data & steps, after the user has consented.
They can revoke their consent at any time in the Settings page.

The data collected is anonymised such that there is no way to determine with
certainty who the original individual was, given some data point.
Therefore, since the data subject is no longer identifiable, the GDPR
does not apply[^data].

[^data]: https://www.ucl.ac.uk/data-protection/guidance-staff-students-and-researchers/practical-data-protection-guidance-notices/anonymisation-and

## Network Sharing

We use end-to-end encryption when sharing wellbeing data with others
in their network to give the user reassurance that no-one except the desired
receiver can read that piece of data.

This reassurance is useful if, for example, a user suspected a server was 
(maliciously or otherwise) logging their IP addresses.
However, we do not do this, and therefore have no personal data stored on the
server.

# Development Blog

Can be found [here](https://uclcomputerscience.github.io/COMP0016_2020_21_Team26/).
