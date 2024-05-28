---
title: One-time password
layout: home
nav_order: 2
parent: Flow types
---

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
