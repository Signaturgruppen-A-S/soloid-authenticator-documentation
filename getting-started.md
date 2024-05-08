---
title: Getting started
layout: home
nav_order: 3
---

# Getting started

## Online demo playground 
First you need one or more installed and ready SoloID Authenticator (PP) apps installed on either iOS or Android. 
Start at the [SoloID Authenticator online demo for the PP environment](https://demo-pp.soloid.dk), follow the install instructions and play around with it to get comfortable with the SoloID Authenticator and some of the basic usecases.

### Demo usecases
The SoloID Authenticator online demo demonstrates the most basic functionality of the SoloID Authenticator for the most basic usecases and settings.

* Login with QR code or app switch: Start by scanning the QR code or by clicking the app switch button (mobile devices) to login. Here any valid SoloID Authenticator device is usable and the online demo will login the selected device, letting the user see the SoloID Authenticator AppID and try out some of the other usecases.
* Step-up with push notifications: After a successfull login, the most basic usecase initiates a SoloID Authenticator flow targeting the specific AppID of the logged in device, sending out a push notification and letting the user approve the request by a simple swipe in the SoloID Authenticator app. This flow demonstrates the "1-factor" or "step-up" flow of SoloID Authenticator, which sends out a push notification and allows the user to approve as fluently and fast as posssible. Always showing the sender name and logo and optional a context specific text.
* Authentication (2-factor): This usecase demonstrates a SoloID flow where the service has requested a full 2-factor authentication with SoloID Authenticator. No push noticications are sent, so the user will have to open the SoloID Authenticator by themselves and upon approval in the app, the user will be prompted for biometric (face, finger, pin) unlock.
* MitID: This usecase demonstrates a usecase where the requesting service asks for the MitID UUID to be returned as part of the result. If the SoloID Authenticator device does not have a MitID registration bound to the device the user will be prompted to initiate a MitID registration inside the SoloID Authenticator app (only once pr. device, if successfull). Upon approval, the user will always be shown an implicit consent just above the approve slider, showing the user that the MitID UUID will be handed out to the requesting service.

## Demo service provider
The demo service provider is a free-to-use pre-registered SoloID Authenticator service provider usable in the PP environment.
Utilize the API client to setup and test your first integration to the SoloID Authenticator setup, free of charge and ready to go.

### API client
```
client_id: 545ec4c7-92b0-475f-9aa9-3cb0fef90f0c
client_secret: qFxHPg6o7arP2nFhFO2c6vj/B1qDqASjfvdlaqGjKsxuOeLLq7sXNbhH3TzOd16E2jRseQkyykmpJtwZEvPBlg==
```

## Accessing the API
In order to utilize the SoloID Authenticator API you first need a valid API client (client_id + client_secret). For your first run, try out the demo service provider API client (see above).
The client_id is mapped to one specific SoloID Authenticator service (name + logo), so it is the client_id used that decides which SoloID Authenticator service to make requests on behalf of.

> Contact Signaturgruppen when ready for a commercial agreement and for setting up your own SoloID Authenticator services.

All service (provider) APIs described at the Swagger definition page for the SoloID Authenticator API is authorized by standard OAuth2 bearer tokens issued by Signaturgruppen Broker. Start by fetching a bearer token with default 1-hour expiration time from the Signaturgruppen Broker token endpoint with the parameters from the following example request:

HTTP
```
POST /op/connect/token HTTP/1.1
Host: pp.netseidbroker.dk
Content-Type: application/x-www-form-urlencoded
Content-Length: xxx

grant_type=client_credentials&scope=privilege_api&client_id=<CLIENT_ID>&client_secret=<CLIENT_SECRET>
```

cURL
```
curl --location 'https://pp.netseidbroker.dk/op/connect/token' \
--header 'Content-Type: application/x-www-form-urlencoded' \
--data-urlencode 'grant_type=client_credentials' \
--data-urlencode 'scope=privilege_api' \
--data-urlencode 'client_id=<CLIENT_ID>' \
--data-urlencode 'client_secret=<CLIENT_SECRET>'
```

With the response
```
{
    "access_token": "eyJhb...xUyFop6w",
    "expires_in": 3600,
    "token_type": "Bearer",
    "scope": "privilege_api"
}
```
After retrieval of the bearer token (access_token), use this as a standard bearer authentication header token for all SoloID Authenticator API calls.

## PostMan examples
Then when ready, import the PostMan collection using the [PostMan](https://www.postman.com/) application and follow these steps: 

1. Import the [Demo PostMan collection](https://raw.githubusercontent.com/Signaturgruppen-A-S/soloid-authenticator-documentation/main/postman/SoloID%20API%20PP%20Demo.postman_collection.json).
2. Run the "Get service token for SoloID Authenticator API" API in order to retrive a valid API token, setup this token as the bearer header for the collection
3. Run the "/api/sp/v2/flow appid (specific AppID)" API, specify an AppID from an installed PP SoloID Authenticator app, this will trigger a flow and push message directly to the targeted SoloID Authenticator App
> **_NOTE:_**  PP App Urls: [Android](https://appdistribution.firebase.dev/i/07887ac4154f4cae) and [iOS](https://testflight.apple.com/join/Vwc72iPI)
4. Run the "/api/sp/v2/flow/:flowId" API in order to fetch the result from the authentication

These examples showcase how to initiate, poll and fetch the result of the most basic SoloID Authenticator flows and comes wired up with the demo service provider credentials.
