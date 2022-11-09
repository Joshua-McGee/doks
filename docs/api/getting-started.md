# Getting started with Agenda APIs

The Ensemble Agenda application is developed with an "API-first" mindset. With the Agenda APIs, you can programmatically perform basic CRUD (Create, Read, Update, Delete) operations against all the various endpoints.

The APIs for the Agenda application all share the same set of authentication headers and use similar syntaxes for their CRUD operations. The following guide outlines the necessary steps for getting started with the Agenda APIs.

## Authentication and headers

In order to authenticate and make calls with the Agenda APIs, you will need to complete the [authentication tutorial](./authentication.md). Once you have completed the tutorial, you will be able to use the following headers:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `Client-ID: {API_KEY}`

### Content-Type header

All requests with a payload in the request body (such as POST and PATCH calls) must include a `Content-Type` header. Accepted values are specific to each API endpoint. 

## Reading sample API calls {#sample-api}

Request formats vary depending on the Agenda API being used. The best way to learn how to structure your API calls is by following along with the examples provided in the documentation for the particular Agenda endpoint you are using.

The documentation for Agenda shows example API calls in two different ways. First, the call is presented in its **API format**, a template representation showing only the operation (GET, POST, PUT, PATCH, DELETE) and the endpoint being used (for example, `/meetings`). Some templates also show the location of variables to help illustrate how a call should be formulated, such as `GET /{VARIABLE}/meetings/{ANOTHER_VARIABLE}`.

The calls are then shown as cURL commands in a **Request**, which includes the necessary headers and full "base path" needed to successfully interact with the API. The base path should be pre-pended to all endpoints. For example, the aforementioned `/meetings` endpoint becomes `https://api.agenda.com/meetings`. You will see the API format / request pattern throughout the documentation, and are expected to use the complete path shown in the example request when making your own calls to the Agenda APIs.

### Example API request

The following is an example API request that demonstrates the format you will encounter in the documentation.

**API format**

The API format shows the operation (GET) and the endpoint being used. Variables are indicated by curly braces (in this case, `{MEETING_ID}`).

```http
GET /meetings/{MEETING_ID}
```

**Request**

In this example request, the variables from the API format are given actual values in the request path. Additionally, all required headers are shown as either sample header values or variables where sensitive information (such as security tokens and access IDs) should be included.

```shell
curl -X GET https://api.agenda.com/meetings/387 \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'Client-ID: {API_KEY}'
```

**Response**

The response illustrates what you would expect to receive following a successful call to the API, based on the request that was sent. Occasionally the response is truncated for space, meaning that you may see more information or additional information to that which is displayed in the sample.

```json
{
    "id": 387,
    "source": {
        "name": "Pierre's Zoom",
        "category": "virtual",
        "id": 9,
        "url": "{ZOOM_LINK}",
        "type": "zoom"
    },
    "invitees":
    [
        {
            "name": "Stephen Chan",
            "email": "stephenc@agenda.com",
            "external": false,
            "status": "pending",
            "team": 7,
            "id": 13
        },
        {
            "name": "Pierre Noble",
            "email": "pierren@agenda.com",
            "external": false,
            "status": "pending",
            "team": 7,
            "id": 35
        },
        {
            "name":"Kyouko Sakura",
            "email": "kyoukos@agenda.com",
            "external": false,
            "status": "pending",
            "team": 7,
            "id": 40
        },               
        {
            "name":"Dmitry Podkolzin",
            "email": "dmitryp@agenda.com",
            "external": false,
            "status": "pending",
            "team": 7,
            "id": 79
        },
        {
            "name":"Jessica Smith",
            "email": "jessicas@agenda.com",
            "external": false,
            "status": "pending",
            "team": 7,
            "id": 133
        },                    
        {
            "name": "Chris Hawthorne",
            "email": "chrish@dahliacorp.com",
            "external": true,
            "status": "pending"
        },
        {
            "name": "Ada Bottas",
            "email": "adab@dahliacorp.com",
            "external": true,
            "status": "pending"
        },
        {
            "name": "Conrad Lee",
            "email": "conradl@agenda.com",
            "external": false,
            "status": "pending",
            "id": 95
        }
    ],
    "name": "Documentation enhancements",
    "description": "A meeting to discuss enhancements to the Agenda documentation.",
    "createdAt": 1667810258,
    "updatedAt": 1667810258,
    "meetingTime": 1668078000,
    "createdBy": 35,
    "series": false
}
```

## Next steps

This document gave instructions on how to use the Agenda APIs, including the required headers and an example API call. To learn more about the different APIs within the Agenda application, please read the [API overview guide](./overview.md).