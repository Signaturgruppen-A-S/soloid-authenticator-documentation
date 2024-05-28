---
title: UX behavior
layout: home
nav_order: 12
---

## UX and app behavior
This section describes the specific details for the UX handling of the SoloID Authenticator app and the browser-based (eID) flows.

### Android and iOS built-in lockscreen 
SoloID Authenticator requires either an active Android or iOS lockscreen when running the device in Standard Mode on Android and iOS. All other variants of SoloID Authenticator will be protected by a server-side validated pincode instead. 

If the device lockscreen becomes disabled or removed on the device, the SoloID Authenticator will deny the user to use the app.

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

