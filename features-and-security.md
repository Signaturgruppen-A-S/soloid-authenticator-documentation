---
title: Features and security
layout: home
nav_order: 5
---

# Features and security overview
{: .no_toc }

The SoloID Authenticator is a general purpose multifactor authentication app targeting iOS and Android, with additional specialized functionality built around the provided functionality of the Signaturgruppen Broker with support for strong eIDs such as, but not limited to, MitID.

The SoloID Authenticator setup comprises a robust backend infrastructure and dedicated iOS and Android SoloID Authenticator apps. The backend is hosted within a highly secure, dual-datacenter configuration shared with the Signaturgruppen Broker (MitID). This setup undergoes continuous security audits, certifications, and monitoring to ensure compliance with national security standards and service level agreements (SLAs).

The SoloID Authenticator app is meticulously engineered to support various authentication models and use cases, meeting stringent security requirements such as those outlined by NIST and the Danish NSIS.

## Table of contents
{: .no_toc .text-delta }

- TOC
{:toc}

## Features
* Step-up single factor (approve flow)
* Authentication two factor (approve flow)
* OTP one-time-password
* Back-channel initiated OpenID Connect flows using Signaturgruppen Broker
* Secure context message to end users
* Channel binding
* Push notications
* Shared device multiuser mode
* National eID usage (e.g. danish MitID)
* Appswitch flexibility and usage
* Device list restriction

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
