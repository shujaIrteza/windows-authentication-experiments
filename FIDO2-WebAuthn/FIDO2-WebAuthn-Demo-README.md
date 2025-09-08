# Contents

[Introduction [2](#introduction)](#introduction)

[Installation & Setup [2](#installation-setup)](#installation-setup)

[1. Install Apache and PHP with XAMPP
[2](#install-apache-and-php-with-xampp)](#install-apache-and-php-with-xampp)

[2. Put the WebAuthn project in Apache’s web root
[4](#put-the-webauthn-project-in-apaches-web-root)](#put-the-webauthn-project-in-apaches-web-root)

[3. Verify PHP runs [5](#verify-php-runs)](#verify-php-runs)

[Usage & Verification [6](#usage-verification)](#usage-verification)

[1. Open the WebAuthn demo UI
[6](#open-the-webauthn-demo-ui)](#open-the-webauthn-demo-ui)

[2. Register a passkey on localhost
[6](#register-a-passkey-on-localhost)](#register-a-passkey-on-localhost)

[Domain Binding Property [8](#_Toc208167331)](#_Toc208167331)

[Steps to verify [8](#_Toc208167332)](#_Toc208167332)

[Conclusion and Real life Applications
[9](#conclusion-and-real-life-applications)](#conclusion-and-real-life-applications)

# Introduction

This document explains the step-by-step process of hosting and running
the WebAuthn PHP demo server locally on a Windows machine. The goal of
this setup is to demonstrate how passkeys (FIDO2 credentials) work, and
more importantly, how they are cryptographically bound to a specific
domain origin. By using Apache with PHP, the WebAuthn library can be
served on http://localhost, where browsers make a special exception to
allow WebAuthn over HTTP. The demo provides a working environment to
create new registrations, verify credentials, and observe how passkeys
cannot be reused across different origins, thereby preventing phishing
attacks.

# Installation & Setup

## Install Apache and PHP with XAMPP

- Download XAMPP: <https://www.apachefriends.org/index.html>.
  <img src="media/image1.png" style="width:6.33333in;height:2.82497in"
  alt="A screenshot of a computer AI-generated content may be incorrect." />

> <img src="media/image2.png" style="width:6.36319in;height:2.425in" />

- Run the installer. Press ok when the warning appears, keep defaults
  and path will be C:\xampp.

> <img src="media/image3.png" style="width:2.34167in;height:2.30833in"
> alt="A screenshot of a computer error AI-generated content may be incorrect." /><img src="media/image4.png" style="width:3.275in;height:2.30833in" />

- Open XAMPP Control Panel and click Start next to Apache. The bar turns
  green.

> <img src="media/image5.png" style="width:5.375in;height:3.61667in" />

- Test in a browser: go to http://localhost/. XAMPP page should be
  visible.

> <img src="media/image6.png" style="width:5.43333in;height:1.95833in" />

## Put the WebAuthn project in Apache’s web root

- Go to <https://github.com/lbuchs/WebAuthn> and download the Zip file
  of WebAuthn and extract it.

> <img src="media/image7.png" style="width:5.68333in;height:3.66667in" />

- Open folder: C:\xampp\htdocs\\

- Move the extracted folder into C:\xampp\htdocs\\ and name it
  WebAuthn-master.

> <img src="media/image8.png" style="width:5.8in;height:3.4in" />

- Confirm path: C:\xampp\htdocs\WebAuthn-master\\

## Verify PHP runs

- Create file C:\xampp\htdocs\phpinfo.php with this content:

> \<?php phpinfo();
>
> <img src="media/image9.png" style="width:5.48333in;height:2.63333in" />
>
> <img src="media/image10.png" style="width:5.49167in;height:2.375in" />

- Open <http://localhost/phpinfo.php> where PHP info page should be
  visible.

<img src="media/image11.png" style="width:5.51667in;height:2.78333in"
alt="A screenshot of a computer AI-generated content may be incorrect." />

# Usage & Verification

## Open the WebAuthn demo UI

- Go to: <http://localhost/WebAuthn-master/_test/client.html>

- Buttons like new registration and check registration should be
  visible.

- Keep RP ID as localhost.

## Register a passkey on localhost

- In the demo page click new registration.

> <img src="media/image12.png" style="width:4.45455in;height:3.27986in"
> alt="A screenshot of a computer AI-generated content may be incorrect." />

- Windows will open a passkey prompt. Use your security key.
  <img src="media/image13.png" style="width:2.41667in;height:2.5303in"
  alt="A screenshot of a computer security system AI-generated content may be incorrect." /><img src="media/image14.png" style="width:2.46389in;height:2.5232in"
  alt="A screen shot of a computer security system AI-generated content may be incorrect." />

<img src="media/image15.png" style="width:2.59486in;height:2.56548in"
alt="A screenshot of a computer AI-generated content may be incorrect." /><img src="media/image16.png" style="width:3.15833in;height:2.5804in"
alt="A screen shot of a computer security AI-generated content may be incorrect." />

- After success, look at the right panel. You should see a credentialId
  listed. That means the server stored your credential for this session
  and the site is verified.

<img src="media/image17.png" style="width:6.08333in;height:5.66667in" />

<span id="_Toc208167331" class="anchor"></span>Domain Binding Property

The domain binding property in FIDO2 ensures that every credential, or
passkey, is cryptographically tied to the exact domain (RPID) where it
was first created. This means that a passkey registered on one domain,
such as *localhost*, cannot be used on another, like *localghost*. The
browser strictly enforces this rule, rejecting any attempt to
authenticate with a mismatched domain. This property is critical because
it prevents attackers from reusing or stealing credentials on phishing
sites, ensuring that passkeys only function on their original trusted
domain.

<span id="_Toc208167332" class="anchor"></span>Steps to verify

- On the demo website, click *Clear All Registrations*.  
  <img src="media/image18.png" style="width:5.67788in;height:1.94819in"
  alt="A screenshot of a web page AI-generated content may be incorrect." />

- In the RPID box, change the value from *localhost* to Localghost.  
  <img src="media/image19.png" style="width:5.80208in;height:1.15in"
  alt="A black text on a white background AI-generated content may be incorrect." />

- Attempt to use the passkey → the browser shows a message denying
  entry.

<img src="media/image20.png" style="width:5.81331in;height:1.94819in"
alt="A black screen with white text AI-generated content may be incorrect." />

**  **

# Conclusion and Real life Applications

By completing this project, a functioning WebAuthn demo server was
successfully set up and tested on a Windows environment using Apache and
PHP. The process demonstrated not only how passkeys can be registered
and verified but also highlighted the domain binding property, which
ensures that credentials are locked to a specific origin and cannot be
reused elsewhere. This property is what makes FIDO2 authentication
resistant to phishing attacks and far more secure than traditional
password-based systems.

In real life, this proof of concept shows how WebAuthn and FIDO2 can be
applied in various security-sensitive areas. For example, online banking
platforms can use passkeys to protect accounts from phishing attempts,
corporate systems can deploy them for employee logins to prevent
credential theft, and VPN or remote access gateways can integrate
WebAuthn for an additional layer of strong authentication. Developers
can also integrate these mechanisms into custom web applications,
providing users with simple but highly secure passwordless logins.
Overall, this experiment provides insight into how FIDO2 can be used to
strengthen authentication in everyday digital environments.

# License

This document is licensed under the [Creative Commons Attribution 4.0
International License.](https://creativecommons.org/licenses/by/4.0/)

© 2025 Shuja Irteza
