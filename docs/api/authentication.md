# Authenticating and using the Agenda APIs

This document provides a step-by-step guide on authenticating with the Agenda application so you can use the Agenda APIs. By following this guide, you will have generated the following credentials for your user account:

- `{ACCESS_TOKEN}`
- `{API_KEY}`

## Prerequisites

Before following the instructions in this guide, you **must** have an Agenda account. 

Additionally, you must have created an application and retrieved your `clientId` and `clientSecret` values from the application dashboard.

## Authorize application

To gain access to the Agenda APIs, you will first need to request authorization from the Agenda application.

You can request application authorization by visiting the following URL:

```http
https://api.agenda.com/oauth/v2/authorize?client_id={CLIENT_ID}
```

| Property | Description | 
| -------- | ----------- |
| `{CLIENT_ID}` | The client ID value from your application's dashboard. |

The Agenda UI will appear, asking you to authorize usage of the application. Select **Accept**, and you will be redirected to a page that displays a code. This code is your temporary authorization code, which will expire after ten minutes.

## Receive access token

Now that you have your temporary authorization code, you will need to exchange this temporary code for an access token.

You can request an access token by visiting the following URL:

### Request

The following request generates a new `{ACCESS_TOKEN}` based on the credentials provided in the payload. This endpoint only accepts form data as its payload, and therefore it must be given a `Content-Type` header of `multipart/form-data`.

```shell
curl -X POST https://api.agenda.com/oauth/v2/token \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={CLIENT_ID}' \
  -F 'client_secret={CLIENT_SECRET}' \
  -F 'grant_type=authorization_code' \
  -F 'code={TEMPORARY_CODE}'
```

| Property | Description | 
| -------- | ----------- |
| `{CLIENT_ID}` | The client ID value that you obtained from your application's dashboard. |
| `{CLIENT_SECRET}` | The client secret value that you obtained from your application's dashboard. |
| `{TEMPORARY_CODE}` | The temporary authorization code that you received in the previous step. |

### Response

If the authorization was valid, a response containing your access token will be sent. 

```json
{
    "access_token": "{ACCESS_TOKEN}",
    "token_type": "bearer"
}
```

| Property | Description | 
| -------- | ----------- |
|  `{ACCESS_TOKEN}` | The access token. This token is used to access the APIs. |

## Next steps

By following this guide, you have gathered and successfully tested your access credentials for the Agenda APIs. 
