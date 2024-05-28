---
title: Approve flow
layout: home
nav_order: 1
parent: Flow types
---

## Approve flow

To initiate an approve flow, utilize the flow API endpoint

```
POST api/sp/v2/flow
```

Here as cURL towards the PP environment
```
curl --location 'https://pp.soloid.dk/api/sp/v2/flow' \
--header 'Content-Type: application/json' \
--header 'Accept: text/plain' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsImtpZCI6IjA...VB8szDy5V3H8usgIqDUHVBOeHh232Xn5PAAVQXJZ35qPJNg' \
--data '{
    "approveText": "Approve flow 😉"
}'
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

#### Approve flow type
The **approveFlowType** parameter specifies one of
* "StepUp": 1-factor authentication. Sends push notifications. No biometric unlock required in app, only swipe inside app.
* "Authenticate": 2-factor authentication: Does not send push notifications. Biometric unlock required in app, for each approval.

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

As cURL example towards PP
```
curl --location 'https://pp.soloid.dk/api/sp/v2/poll/<flowId>' \
--header 'Accept: text/plain' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIsIm...8szDy5V3H8usgIqDUHVBOeHh232Xn5PAAVQXJZ35qPJNg' \
```

This will enable to continuously poll the general state of a flow and is also used by the SoloID Authenticator iframe for checking the current flowstate.

The poll endpoint returns a result on the form
```
{
  "flowState": "Pending"
}
```
Where **flowState** is one of
```
[ Invalid, Pending, Approved, Rejected, Expired ]
```

When the flow is completed, the result can be retrieved by your backend calling the flow result API endpoint:

```
GET api/sp/v2/flow/[:flowId]
```

As cURL towards PP
```
curl --location 'https://pp.soloid.dk/api/sp/v2/flow/<flowId>' \
--header 'Accept: text/plain' \
--header 'Authorization: Bearer eyJhbGciOiJSUzI1NiIs...uCV9qVB8szDy5V3H8usgIqDUHVBOeHh232Xn5PAAVQXJZ35qPJNg' \
```

The result will contain the following structure:

```
{
  "flowId": "string",
  "flowState": flowState,
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
