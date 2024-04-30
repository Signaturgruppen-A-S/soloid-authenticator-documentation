---
title: Getting started
layout: home
nav_order: 3
---

# Getting started

## Online demo playground 
First you need one or more installed and ready SoloID Authenticator (PP) apps installed on either iOS or Android. 
Start at the [SoloID Authenticator online demo for the PP environment](https://demo-pp.soloid.dk), follow the install instructions and play around with it to get comfortably with the SoloID Authenticator and some of the basic usecases.

## Demo service provider
The demo service provider is a free-to-use pre-registered SoloID Authenticator service provider usable in the PP environment.
Utilize the API client to setup and test your first integration to the SoloID Authenticator setup, free of charge and ready to go.

#### API client
```
client_id: 545ec4c7-92b0-475f-9aa9-3cb0fef90f0c
client_secret: qFxHPg6o7arP2nFhFO2c6vj/B1qDqASjfvdlaqGjKsxuOeLLq7sXNbhH3TzOd16E2jRseQkyykmpJtwZEvPBlg==
```

## PostMan examples
Then when ready, import the PostMan collection using the [PostMan](https://www.postman.com/) application and follow these steps: 

1) Import the [Demo PostMan collection](https://raw.githubusercontent.com/Signaturgruppen-A-S/soloid-authenticator-documentation/main/postman/SoloID%20API%20PP%20Demo.postman_collection.json).
2) Run the "Get service token for SoloID Authenticator API" API in order to retrive a valid API token, setup this token as the bearer header for the collection
3) Run the "/api/sp/v2/flow appid (specific AppID)" API, specify an AppID from an installed PP SoloID Authenticator app, this will trigger a flow and push message directly to the targeted SoloID Authenticator App
> **_NOTE:_**  PP App Urls: [Android](https://appdistribution.firebase.dev/i/07887ac4154f4cae) and [iOS](https://testflight.apple.com/join/Vwc72iPI)
4) Run the "/api/sp/v2/flow/:flowId" API in order to fetch the result from the authentication

## Pure back-channel vs. iframed SoloID Authenticator flow
The PostMan examples includes an example that initiates a new SoloID flow without specifying an AppID and thus initiates a flow that is not bound to a specific set of devices. In order for a device to successfully hook into this flow, the device will have to either scan the corresponding SoloID Authenticator QR code or the user will have to click the appswitch button, both dynamically created inside the SoloID Authenticator flow iframe.

The [SoloID Authenticator online demo for the PP environment](https://demo-pp.soloid.dk) demonstrates the usage of the iframe, which is the default behavior for SoloID flows, as this will align the expected UX.

The [quick iframe HTML example](https://raw.githubusercontent.com/Signaturgruppen-A-S/soloid-authenticator-documentation/main/iframe-example/soloid-authenticator-iframe-example.html) demonstrates the bare minimum for setting up the SoloID Authenticator iframe. Start a flow and insert the generated flowId into the HTML and run the HTML file in your browser to see it in action. 


