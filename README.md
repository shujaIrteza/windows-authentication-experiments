# Authentication Demos on Windows

This repository contains proof-of-concept demos for authentication methods tested on Windows.  
It includes both passwordless authentication using **FIDO2/WebAuthn** and one-time password authentication using **MultiOTP HOTP**.

## Contents
- [FIDO2-WebAuthn Demo](./FIDO2-WebAuthn/README.md)  
- [MultiOTP-HOTP Demo](./MultiOTP-HOTP/README.md)  

## Purpose
The goal of this repository is to demonstrate different authentication mechanisms in a controlled local environment.  
- **FIDO2/WebAuthn** → Shows how passkeys work and highlights the domain binding property that prevents phishing.  
- **MultiOTP HOTP** → Demonstrates HMAC-based one-time password generation and validation with FreeOTP.  

## License
This repository is licensed under the [Creative Commons Attribution 4.0 International License](./LICENSE).  
© 2025 Shuja Irteza
