# Contents

[Introduction [2](#introduction)](#introduction)

[Installation and Setup
[2](#installation-and-setup)](#installation-and-setup)

[1. Download MultiOTP and FreeOTP
[2](#download-multiotp-and-freeotp)](#download-multiotp-and-freeotp)

[2. Open Command Prompt [2](#open-command-prompt)](#open-command-prompt)

[3. Install the Web Service
[3](#install-the-web-service)](#install-the-web-service)

[Usage [3](#usage)](#usage)

[1. Create a Test User [3](#create-a-test-user)](#create-a-test-user)

[2. Configure User [4](#configure-user)](#configure-user)

[3. Generate QR Code [4](#generate-qr-code)](#generate-qr-code)

[4. Verify OTP Codes [4](#verify-otp-codes)](#verify-otp-codes)

[Verification of completion
[6](#verification-of-completion)](#verification-of-completion)

[Show User Info (Optional)
[7](#show-user-info-optional)](#show-user-info-optional)

[Conclusion and Real-Life Applications
[7](#conclusion-and-real-life-applications)](#conclusion-and-real-life-applications)

[License [8](#license)](#license)

# Introduction

This project demonstrates how to set up and test MultiOTP as an HOTP
(HMAC-based One-Time Password) server on a Windows machine. The goal is
to show that a local installation of MultiOTP can create OTP users,
generate shared secrets, and validate codes from an authenticator app
like FreeOTP. It serves as a proof of concept for implementing
two-factor authentication in a controlled environment.

# Installation and Setup

## 1. Download MultiOTP and FreeOTP

- Navigate to <https://download.multiotp.net/>  
  <img src="media/image1.png" style="width:4.2945in;height:2.7873in"
  alt="A screenshot of a computer AI-generated content may be incorrect." />

- Download **multiotp.zip**

- Extract it to a folder, for example: C:\multiotp

- Work only inside the folder: C:\multiotp\windows

- On a phone, download **FreeOTP by Red Hat**: [iOS App
  Store](https://apps.apple.com/us/app/freeotp-authenticator/id872559395)
  or [Google Play
  Store](https://play.google.com/store/apps/details?id=org.fedorahosted.freeotp).

## 2. Open Command Prompt

- Run Command Prompt as **Administrator**.

- Change to the MultiOTP Windows folder:

cd C:\multiotp\windows

<img src="media/image2.png" style="width:3.80743in;height:1.57226in"
alt="A screenshot of a computer program AI-generated content may be incorrect." />

## 3. Install the Web Service

- Execute:

> webservice_install.cmd  
> <img src="media/image3.png" style="width:4.07349in;height:0.96889in"
> alt="A black screen with white text AI-generated content may be incorrect." />

- This installs MultiOTP as a Windows service.

- Automatically takes you to the page after command execution:
  <http://localhost:8112>.

<img src="media/image4.png" style="width:5.62084in;height:1.8622in"
alt="A screenshot of a computer screen AI-generated content may be incorrect." />

# Usage

## 1. Create a Test User

multiotp.exe -fastcreatenopin testuser

- A user named testuser is created with no PIN required.

<img src="media/image5.png" style="width:5.55286in;height:0.63551in"
alt="A black screen with white text AI-generated content may be incorrect." />

## 2. Configure User

> multiotp.exe -set testuser algorithm=hotp

multiotp.exe -set testuser prefix-pin=0

<img src="media/image6.png" style="width:4.56049in;height:0.82477in"
alt="A black screen with white text AI-generated content may be incorrect." />

- The algorithm is set to HOTP (counter-based).

- The prefix PIN is disabled.

## 3. Generate QR Code

multiotp.exe -qrcode testuser testuser.png

- A PNG file with the HOTP secret will be created. The file should be
  called testuser.png

<img src="media/image7.png" style="width:4.011in;height:0.45981in"
alt="A black background with white text AI-generated content may be incorrect." />

<img src="media/image8.png" style="width:3.97168in;height:1.91429in"
alt="A screenshot of a computer AI-generated content may be incorrect." />

- The PNG is to be opened and scanned with FreeOTP (Red Hat) on the
  phone.

- The token type must be set to HOTP, not TOTP.

## 4. Verify OTP Codes

- Open FreeOTP app on mobile device and click Scan QR code in the marked
  spot.
  <img src="media/image9.jpeg" style="width:4.09167in;height:1.01788in"
  alt="A black background with white text AI-generated content may be incorrect." />

- Open testuser.png from pc and scan using phone.

> <img src="media/image10.jpeg" style="width:4.10158in;height:2.825in"
> alt="A qr code on a piece of paper AI-generated content may be incorrect." />

- Select any icon and click next on the displayed message

<img src="media/image11.jpeg" style="width:2.04735in;height:2.15278in"
alt="A screenshot of a phone AI-generated content may be incorrect." /><img src="media/image12.jpeg" style="width:2.25in;height:2.14856in"
alt="A screenshot of a phone AI-generated content may be incorrect." />

- Generate a code by tapping the icon token.

- Test in CLI, put the generated code in \<code\>:

multiotp.exe -check testuser \<code\>

- Example:

multiotp.exe -check testuser 994662

<img src="media/image13.png" style="width:5.30282in;height:0.64592in"
alt="A black screen with white text AI-generated content may be incorrect." />

# Verification of completion

- Visit <http://localhost:8112> and put credentials; username: admin ;
  password: 1234. Click Check a user.  
  <img src="media/image14.png" style="width:5.67716in;height:3.10489in"
  alt="A screenshot of a computer AI-generated content may be incorrect." />

<!-- -->

- Generate a new code from the phone and click check now.
  <img src="media/image15.png" style="width:5.14368in;height:2.95498in"
  alt="A screenshot of a computer AI-generated content may be incorrect." />

- The test result should show succeeded.

<img src="media/image16.png" style="width:5.13613in;height:1.42728in"
alt="A screenshot of a computer screen AI-generated content may be incorrect." />

## Show User Info (Optional)

multiotp.exe -user-info testuser

- Displays HOTP configuration, counters, and other details.

<img src="media/image17.png" style="width:5.21935in;height:2.08357in"
alt="A screen shot of a computer AI-generated content may be incorrect." />

# Conclusion and Real-Life Applications

By following these steps, a working HOTP server was demonstrated running
locally on Windows. This proof of concept shows that a Windows machine
can generate and validate one-time passwords using MultiOTP and FreeOTP.

In real life, such a setup can be extended to add two-factor
authentication for different systems:

- **VPNs and Firewalls**: Remote access can be protected by requiring an
  OTP in addition to a password.

- **Company Intranet Websites**: MultiOTP can be used as a backend to
  verify OTP codes during login.

- **Windows or Linux Logins**: With plugins, OTP can be enforced for
  operating system authentication.

- **Custom Projects**: Developers can integrate MultiOTP’s web service
  or CLI into their own apps to add secure OTP-based login.

This demonstrates how the simple test performed here can translate into
stronger security in real-world environments.

# License

This document is licensed under the [Creative Commons Attribution 4.0
International License.](https://creativecommons.org/licenses/by/4.0/)

© 2025 Shuja Irteza
