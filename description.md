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

## Initiate flow

### Initiate approve / swipe flow type
To initiate an approve flow, utilize the flow API endpoint
```
POST api/sp/v2/flow
```
The flow API endpoint will take the following parameters:

| Parameter      | Description | Default |
| ----------- | ----------- | ----------- |
| deviceList      | Specifies one or more devices by AppIDs or by an unique eID identifier       | null |
| approveFlowType      | One of ["StepUp", "Authenticate"]       | "StepUp" |
| requestedIdp      | If set, must be a supported IDP like "MitID"       | "None" |
| approveText      | Text to show user in app. 130 characters length limit.       | null |
| channelBindingOption      | Specifies channel-binding behavior. One of ["None", "Required"]       | "None" |
| appSwitchUrlOnCompleted      | Specifies an URL for which the SoloID Authenticator should redirect the user when the flow has completed       | null |

#### Approve text
The **approveText** parameter is highly recommended to utilize for each SoloID Authenticator flow and will enable the service to present a short and specific context specific text to the approving user, helping to improve user awareness and improve flow security.

#### RequestedIdp
The **requestedIdp** parameter enables the service to initiate a SoloID Authenticator flow requiring the user to have the specified eID bound to the approving SoloID Authenticator device. On success, return the eID global identifier to the service.

The binding of the requested IDP to the device is handled automatically by the SoloID Authenticator and will only trigger for devices for which no previous binding for the requested IDP has been done. 
The user will have control on whether to accept the binding and is will be presented with an inline consent when approving to hand-out the specific eID identifier to the requesting service.

#### Channel-binding options
SoloID Authenticator supports the requirement for channel-binding for approve flows. This requirement will enforce that the approving device either scan a SoloID Authenticator flow QR code with the in-app QR scanner or that the app is initiated with a specific appswitch containing the channel-binding identifier for the flow. This increases the probability that the approving app is near (QR) or on the same device (appswitch) as the browser/app/screen used to display the QR or from which the appswitch was initiated.

### Poll result
A CORS and JavaScript enabled polling enpoint is available at
```
GET /api/sp/v2/poll/[:flowId]
```
This will enable to continuously poll the general state of a flow and is also used by the SoloID Authenticator iframe for checking the current flowstate.
When the flow is completed, the result can be retrieved by your backend calling the flow result API endpoint:

```
GET api/sp/v2/flow/[:flowId]
```
The result will contain the following structure:

```
{
  "flowId": "string",
  "flowState": "Invalid",
  "appId": "string",
  "idp": "string",
  "idpIdentityId": "string"
}
```

| Parameter      | Description | In result (Always, Optional) |
| ----------- | ----------- | ----------- |
| flowId      | FlowID of flow       | Always |
| flowState      | [ Invalid, Pending, Approved, Rejected, Expired ]       | Always |
| appId      | SoloID Authenticator device AppID       | Always |
| idp      | IDP identifier, if requested       | Optional |
| idpIdentityId      | IDP ID identifier, if idp is set       | Optional |
