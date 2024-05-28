---
title: Device modes
layout: home
nav_order: 6
---

# Device modes

SoloID Authenticator supports two modes of operation
* Standard (default)
* Shared

The default behavior is to allow the user to utilize the Android or iOS built-in lockscreen to safeguard a hardware backed cryptographic key used by SoloID Authenticator. 
It is also an option to share the same SoloID Authenticator app between multiple users, which will disable the use of the built-in lockscreen and instead utilize a per-user server-side validated pincode. 

For both modes of operation a unique AppID is generated pr. app-instance, which for Shared Mode is pr. user. Each user has their own unique AppID pr. device they are using and each of these are built as stand-alone SoloID Authenticator devices.

## Standard Mode

## Shared Mode

<img src="images/shared_mode1.jpg" alt="Shared Mode" width="250">

