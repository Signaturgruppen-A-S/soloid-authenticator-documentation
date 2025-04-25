---
title: Device requirements
layout: home
nav_order: 6
---
# Device requirements

## 📱 Android System Requirements (Play Integrity API)

Our application utilizes the [Google Play Integrity API](https://developer.android.com/google/play/integrity), which requires all devices to meet the following minimum criteria to function properly:

### ✅ Minimum Requirements

- **Android Version**:  
  Devices must be running **Android 8.0 (Oreo)** and above.
  
- **Google Play Services**:  
  Devices must have **Google Play services installed and up-to-date**.

- **Google Play Store**:  
  Devices must have the **official Google Play Store** installed and enabled.

- **Device Certification**:  
  Devices must be **Google Play Protect certified**.  
  This ensures the device is not rooted or running an uncertified/custom version of Android.

### 🚫 Unsupported Devices

- Devices without **Google Play Services** (e.g., some custom ROMs or devices sold without Google licensing).
- Devices that are **rooted**, **tampered**, or **emulated**.
- Devices that fail **Play Integrity API checks** (e.g., due to Play Protect certification failure).

## 🍏 iOS System Requirements (Security & Integrity Attestation)

Our iOS application performs device-level **security and integrity checks** during startup, including verification using **Secure Enclave attestation** where supported. To ensure full compatibility and security, devices must meet the following requirements:

### ✅ Minimum Requirements

- **iOS Version**:  
  Devices must be running **iOS 14.0 or later**.  
  > ℹ️ Secure Enclave attestation is supported on devices with a Secure Enclave chip and iOS 14+.

- **Hardware Requirements**:  
  Devices must have a **Secure Enclave** (e.g., A7 chip or newer).  
  This enables attestation of cryptographic operations and key material isolation.

- **Jailbreak Status**:  
  Devices **must not be jailbroken**.  
  Tampered systems or environments that fail security checks will not be allowed to proceed.

- **Device Integrity**:  
  The app performs runtime checks to verify system integrity and signs of tampering, including:
  - Secure Enclave key validation
  - OS trust chain validation
  - Debugging/tracing detection

### 🚫 Unsupported Devices

- Devices running **iOS versions earlier than 14.0**
- Devices **without Secure Enclave hardware** (e.g., older than iPhone 5s)
- **Jailbroken** or otherwise modified devices
- Devices that fail **integrity or security attestation checks**
