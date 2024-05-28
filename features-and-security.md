---
title: Features and security
layout: home
nav_order: 5
---

# Features and security overview
{: .no_toc }

The SoloID Authenticator is a general purpose multifactor authentication app targeting iOS and Android, with additional specialized functionality built around the provided functionality of the Signaturgruppen Broker with support for strong eIDs such as, but not limited to, MitID.
The SoloID Authenticator app and backend setup is built and designed to be audited and used as part of setups under strict security audits, including the danish NSIS and the european GDPR.

## Table of contents
{: .no_toc .text-delta }

- TOC
{:toc}

## Features
* Step-up single factor
* Authentication two factor
* Back-channel initiated OpenID Connect flows using Signaturgruppen Broker
* OTP one-time-password
* Channel binding
* Push notications
* Shared device multiuser mode

## Security measures

* Hardware backed non-exportable cryptographic keys, utilizing modern smartphones built-in hardware security chips. Registration of keys includes hardware-backend attestation on both platforms, ensuring the keys are hardware backed and non-exportable.
* Hardware backend key used to register device, access backend APIs and approve flows: without the private key it is not possible to approve any flows or retrieve information from the backend such as secure OTP codes.
* Integrity validation of client app and device on both iOS and Android, using platform available measures. This includes detection of rooted devices and Apple and Google signed attestation that app is installed from official app store and that the app is the SoloID Authenticator app.
* Utilization of device built-in biometrics and device unlock mechanics for signing with hardware backed device key: fingerprint, facial recognition, pattern unlock, pincodes. 
* Replay protected protocol between app and backend, utilzing secure unique and random generated challenges.
* Backend hosted in same datacenters as Signaturgruppen Broker and is built under the same security and audit requirements. This ensures compliance with applicable certifications and requirements and ensures availability and scalability to ensure the same high SLA as provided by Signaturgruppen Broker.
* NSIS compliant audit log.
* Backend generated secure random OTP codes for one-time-password flows.
* Browser-based flows is done using best-practices platform specific secure browser usage (SFSafariViewController and CustomTabs).
* Appswitch protocols is implemented by best-practices Universal Links / App Links protocols.
* Android and iOS apps is developed, coded, released and managed by Makeable and written in native code on both platforms.
* Server-side validated pincode for shared mode devices and registrations.
* Always displaying requesting logo and service name to user as part of approve flows and OTP messages.
* Always displaying the approve text if specified by requesting service.

## Stored data
Data stored for the SoloID Authenticator app and associated flows can be divided into the app and the correponding backend services involved in the SoloID Authenticator flows. 

### SoloID Authenticator app
On each SoloID Authenticator app device, only the data required for the actual device to function is stored. This corresponds of
* Hardware backend non-exportable private keys used for registration, signing and approving flows.
* Specific SoloID Authenticator device information: AppID, eID info, device short name, basic device data (all can be seen from the settings page in the app)

All data is marked as non-exportable to avoid cloud synchronization and only available through the installed app on the device.

### SoloID Authenticator backend 
* Registered devices, including public keys and AppID, device short name
* Audit logs (NSIS compliant, same setup as for Signaturgruppen Broker)
* Application logs (3 months retention, kept inside Nets access control, same setup as for Signaturgruppen Broker)
* Registered eID bindings: IDP + IDP global ID, such as MitID UUID.

## UX and app behavior
This section describes the specific details for the UX handling of the SoloID Authenticator app and the browser-based (eID) flows.

### Lockscreen 
The SoloID Authenticator app does not allow to be opened unless the device has an active lockscreen enabled.

### App shows logo and service name for flows
The SoloID Authenticator app always shows the logo and service name to the user for approve and OTP flows.

### App shows approvetext to user
The SoloID Authenticator app always shows the approvetext to the user (approve flows) when specified in the flow.

### App shows consent message for eID info handout
The SoloID Authenticator app always shows an inline consent message to the user when the service is requesting an eID identifier. This makes it possible for the user to see that the service will receive this information as part of the approval process.

### App shows eID binding initiation approve screen before starting eID flow binding
The SoloID Authenticator app will show an approve screen to the user explaining that a browserbased eID flow will be started and that the resulting eID will be paired with the AppID.

### Unlock for eID flows
The SoloID Authenticator app requires the user to unlock when starting an eID (binding) flow, for which the authenticated eID will be paired with the AppID from the SoloID Authenticator app.

### Local salt utilized for pincode
When the SoloID Authenticator utilizes a pincode instead of device unlock, a secure and random salt must be utilized pr. registration (AppID) stored as securely as possible locally on the device, s.t. the same pincodes never maps to the same pincode output from the SoloID Authenticator device. 
This is to ensure, that when two different registrations of SoloID Authenticator (unique AppIDs) have the users involved enter the same pincode, the actual pincode sent to the backend will never be the same, as they have been salted with different salts.

### Timeout lock in shared mode
Ensure short timeout lock in shared mode. This ensures that if a shared mode SoloID Authenticator has a limited window of oppotunity for misuse by another user after unlock.

### Android integrity token requests from Google
The Android App will only request an integrity token from Google in the following cases: 
* Registration of device (new AppID)
* When requested in Authentication header flow
