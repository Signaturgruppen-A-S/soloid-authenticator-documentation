---
title: PostMan demo example
layout: home
nav_order: 3
---

# API Demo PostMan example

## Getting started 
First you need one or more installed and ready SoloID Authenticator (PP) apps installed on either iOS or Android. 
Start at the [SoloID Authenticator online demo for the PP environment](https://demo-pp.soloid.dk), follow the install instructions and play around with it to get comfortably with the SoloID Authenticator and some of the basic usecases.

Then when ready, import the PostMan collection using the [PostMan](https://www.postman.com/) application and follow these steps: 

1) Import the [Demo PostMan collection](https://raw.githubusercontent.com/Signaturgruppen-A-S/soloid-authenticator-documentation/main/postman/SoloID%20API%20PP%20Demo.postman_collection.json).
2) Run the "Get service token for SoloID Authenticator API" API in order to retrive a valid API token, setup this token as the bearer header for the collection
3) Run the "/api/sp/v2/flow appid (specific AppID)" API, specify an AppID from an installed PP SoloID Authenticator app, this will trigger a flow and push message directly to the targeted SoloID Authenticator App
> **_NOTE:_**  PP App Urls: [Android](https://appdistribution.firebase.dev/i/07887ac4154f4cae) and [iOS](https://testflight.apple.com/join/Vwc72iPI)
4) Run the "/api/sp/v2/flow/:flowId" API in order to fetch the result from the authentication

## pure back-channel vs. iframed SoloID Authenticator flow
