---
title: Description
layout: home
nav_order: 5
---

# SoloID Authenticator setup description
The SoloID Authenticator API provides the means to initiate and poll SoloID Authenticator app flows and supports various flow variants suited for different usecases and requirements.

## Setup architecture
The SoloID Authenticator setup consists of a backend infrastructure and the iOS and Android SoloID Authenticator apps.
The backend is hosted in a highly secure and available two datacenter setup shared with the Signaturgruppen Broker (MitID) and undergoes continuous security and audit certifications and monitoring to ensure compliance and SLA that lives up to the requirements for national security standards. 
The app is built from the ground up with the focus to support various authentication models and usecases required to meet security requirements for the same national standards (such as NIST and the danish NSIS).

## Flow types and features
The SoloID Authenticator supports the following flowtypes

* Step-up (single factor, NIST AAL level 1 and NSIS level low)
* Authentication (two factor, NIST ALL level 2 and NSIS level substantial)
* Secure OTP codes
* Appswitch support
* eID support: MitID and other IDPs available through Signaturgruppen Broker
* eID flows: Supports backend initiated eID flows

## Security features
The SoloID Authenticator app supports the following security features

* Channel-binding: Optional, but can be forced.
* Hardware-based cryptographics keys: Non-exportable, security best practice on Android and iOS
* Key attestation for device keys
* App integrity protection using Apple and Google built-in features to ensure non-rooted, non-jailed-breaked devices and that the SoloID Authenticator app has been installed from the official app stores signed by Apple or Google.
* Using device built-in biometrics and device unlock security features to ensure the proper balance between usability, ease of use and security
* eID binding: Bind eID to device to create a strong identity binding and registration to the app and corresponding SoloID Authenticator AppID.

## Swipe flows (approve)
The basic and most dynamic flows consists of the swipe/approve flows where an authentication request is displayed in the SoloID Authenticator app with the name and logo of the requesting service alongside an optionally text bound to the flow. 
The user can then either approve by swiping the approve button slider in the bottom of the app, or reject the flow.

Options:
* Push notifications: It is possible to trigger push notifications when starting a flow to targeted devices.
* Channel-binding: Require the approving device to scan a generated QR code or transfer the generated code using appswitch (same device) - automatically supported when using the iframe setup.
* Choice of authentication strength: one or two factor (NIST AAL level 1 or 2, NSIS level low and substantial). Two factor triggers requirement for biometric approval.
* Request and require eID binding to device: Dynamically handled by app and backend for users.
* eID flow: Option to force an eID approval, i.e. trigger flow from app that starts a secure eID flow handled by the SoloID Authenticator app and backend.
* Appswitch options: Options for controlling and specifying appswitch behavior for better UX.

## Secure OTP codes
Generate a secure one-time code sent to the specified devices (using device AppID or eID identifiers).

## Pure back-channel vs. iframed SoloID Authenticator flow
The PostMan examples includes an example that initiates a new SoloID flow without specifying an AppID and thus initiates a flow that is not bound to a specific set of devices. In order for a device to successfully hook into this flow, the device will have to either scan the corresponding SoloID Authenticator QR code or the user will have to click the appswitch button, both dynamically created inside the SoloID Authenticator flow iframe.

The [SoloID Authenticator online demo for the PP environment](https://demo-pp.soloid.dk) demonstrates the usage of the iframe, which is the default behavior for SoloID flows, as this will align the expected UX.

The [quick iframe HTML example](https://raw.githubusercontent.com/Signaturgruppen-A-S/soloid-authenticator-documentation/main/iframe-example/soloid-authenticator-iframe-example.html) demonstrates the bare minimum for setting up the SoloID Authenticator iframe. Start a flow and insert the generated flowId into the HTML and run the HTML file in your browser to see it in action. 

### QR code and App Switch without iframe
The SoloID Authenticator API includes the following API, which enables services to retrieve a QR code and an app switch URL, that can be utilized to setup the SoloID Authenticator QR code for the specific flow (FlowID) or enable app switch directly to the SoloID Authenticator app using Universal Links  or App Links.

```
POST /api/sp/v2/qrAppSwitchUrl
```

