---
title: Backchannel and iframe
layout: home
nav_order: 40
---


## Pure back-channel vs. iframed SoloID Authenticator flow
The PostMan examples includes an example that initiates a new SoloID flow without specifying an AppID and thus initiates a flow that is not bound to a specific set of devices. In order for a device to successfully hook into this flow, the device will have to either scan the corresponding SoloID Authenticator QR code or the user will have to click the appswitch button, both dynamically created inside the SoloID Authenticator flow iframe.

The [SoloID Authenticator online demo for the PP environment](https://demo-pp.soloid.dk) demonstrates the usage of the iframe, which is the default behavior for SoloID flows, as this will align the expected UX.

The [quick iframe HTML example](https://raw.githubusercontent.com/Signaturgruppen-A-S/soloid-authenticator-documentation/main/iframe-example/soloid-authenticator-iframe-example.html) demonstrates the bare minimum for setting up the SoloID Authenticator iframe. Start a flow and insert the generated flowId into the HTML and run the HTML file in your browser to see it in action. 

### QR code and App Switch without iframe
The SoloID Authenticator API includes the following API, which enables services to retrieve a QR code and an app switch URL, that can be utilized to setup the SoloID Authenticator QR code for the specific flow (FlowID) or enable app switch directly to the SoloID Authenticator app using Universal Links  or App Links.

```
POST /api/sp/v2/qrAppSwitchUrl
```

