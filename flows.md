---
title: Flow types
layout: home
nav_order: 7
---

# Flow Types

## Overview
The SoloID Authenticator app support two primary flow types
* Approve flow
* Secure one-time password (OTP)

Each flow supports various security related options
* Authentication strength
* Registration strength
* Secure context message to end users
* Push notifications
* Channel binding for security and ease of use
* Device list restriction
* National eID usage (e.g. danish MitID)
* Appswitch flexibility and usage

## Secure one-time password (OTP)
SoloID Authenticator supports sending secure and randomly generated one-time password (OTP) to target devices. 

Initiate the flow by calling the following API

```
/api/sp/v2/otp
```

The API endpoint will take the following parameters:

| Parameter      | Description | Required / Optional |
| ----------- | ----------- | ----------- |
| deviceList      | Specifies one or more devices by AppIDs or by an unique eID identifier       | Required |
| otpContextText      | Text to show user in app. 130 characters length limit.       | Optional |

This will initiate and send a 8 digit secure and randomly generated OTP code to the target devices.

The result from the API call is on the following form:

```
{
  "otpId": "string",
  "otp": "string",
  "expires": "2024-05-01T13:44:22.256Z"
}
```

| Parameter      | Description | 
| ----------- | ----------- | 
| otpId      | ID of OTP       | 
| otp      | The generated OTP sent to the devices       | 
| expires      | The OTP timeout time. The OTP will remain visible on the receiving devices until this time.       | 
