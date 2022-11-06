# Meetings endpoint

The Agenda application lets you manage your meetings - both external and internal - with ease. You can use the `/meetings` endpoint to retrieve a list of meetings, create a new meeting, retrieve details of a specific meeting, update a specific meeting, or delete a specific meeting.  

## Getting started

The endpoints used in this guide are part of the Ensemble Agenda APIs. Before continuing, please review the [getting started guide](./getting-started.md) for important information that you need to know in order to successfully make calls to the API, including required headers and how to read example APIs.

## List meetings

You can retrieve a list of all the meetings for your company by making a GET request to the `/meetings` endpoint.

### API format

The `/meetings` endpoint supports several query parameters to help filter your results. While these parameters are optional, their use is **strongly** recommended to help reduce expensive overhead. Making a call to this endpoint without any parameters will retrieve **all** meetings available for your company. Multiple parameters can be included, separated by ampersands (`&`).

```http
GET /meetings
GET /meetings?source-id={SOURCE_ID}
GET /meetings?source-name={SOURCE_NAME}
GET /meetings?source-category={SOURCE_CATEGORY}
GET /meetings?team-id={TEAM_ID}
GET /meetings?team-name={TEAM_NAME}
GET /meetings?limit={LIMIT}
GET /meetings?page={PAGE}
```

| Parameter | Description |
| --------- | ----------- |
| `{SOURCE_ID}` | The ID of the source that you want to filter by. |
| `{SOURCE_NAME}` | The name of the source that you want to filter by. |
| `{SOURCE_CATEGORY}` | The category of source you want to filter by. This value can either be `virtual` or `in-person`. |
| `{TEAM_ID}` | The ID of the team that you want to filter for. |
| `{TEAM_NAME}` | The name of the team that you want to filter for. | 
| `{LIMIT}` | Specifies the number of meetings returned. | 
| `{PAGE}` | Specifies the offset of the pages of meetings returned. |

### Request

The following request will retrieve the last two meetings for the Agenda Documentation team.

```shell
curl -X GET https://api.ensemble.com/agenda/meetings?limit=2&team-id=7 \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'Client-ID: {API_KEY}'
```

### Response

A successful response returns HTTP status 200 with a list of meetings, based on the query parameter(s) provided in the request path.

```json
{
    "records": [
        {
            "id": 369,
            "source": {
                "name": "Solis",
                "category": "in-person",
                "id": 8
            },
            "invitees": [
                {
                    "name": "Stephen Chan",
                    "email": "stephenc@ensemble.com",
                    "external": false,
                    "status": "accepted",
                    "team": 7,
                    "id": 13
                },
                {
                    "name": "Pierre Noble",
                    "email": "pierren@ensemble.com",
                    "external": false,
                    "status": "accepted",
                    "team": 7,
                    "id": 35
                },
                {
                    "name":"Kyouko Sakura",
                    "email": "kyoukos@ensemble.com",
                    "external": false,
                    "status": "accepted",
                    "team": 7,
                    "id": 40
                },               
                {
                    "name":"Dmitry Podkolzin",
                    "email": "dmitryp@ensemble.com",
                    "external": false,
                    "status": "accepted",
                    "team": 7,
                    "id": 79
                },
                {
                    "name":"Jessica Smith",
                    "email": "jessicas@ensemble.com",
                    "external": false,
                    "status": "accepted",
                    "team": 7,
                    "id": 133
                }
            ],
            "name": "Standup",
            "description": "Daily standup for the Agenda Documentation team. Use this meeting to discuss wins, challenges, and other documentation-related topics.",
            "createdAt": 1641289072,
            "updatedAt": 1641289072,
            "createdBy": 35,
            "updatedBy": 35,
            "meetingTime": 1667556000,
            "series": true
        },
        {
            "id": 365,
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
                    "email": "stephenc@ensemble.com",
                    "external": false,
                    "status": "accepted",
                    "team": 7,
                    "id": 13
                },
                {
                    "name": "Pierre Noble",
                    "email": "pierren@ensemble.com",
                    "external": false,
                    "status": "accepted",
                    "team": 7,
                    "id": 35
                },
                {
                    "name":"Kyouko Sakura",
                    "email": "kyoukos@ensemble.com",
                    "external": false,
                    "status": "accepted",
                    "team": 7,
                    "id": 40
                },               
                {
                    "name":"Dmitry Podkolzin",
                    "email": "dmitryp@ensemble.com",
                    "external": false,
                    "status": "accepted",
                    "team": 7,
                    "id": 79
                },
                {
                    "name":"Jessica Smith",
                    "email": "jessicas@ensemble.com",
                    "external": false,
                    "status": "accepted",
                    "team": 7,
                    "id": 133
                },                    
                {
                    "name": "Chris Hawthorne",
                    "email": "chrish@dahliacorp.com",
                    "external": true,
                    "status": "accepted"
                },
                {
                    "name": "Ada Bottas",
                    "email": "adab@dahliacorp.com",
                    "external": true,
                    "status": "pending"
                },
                {
                    "name": "Conrad Lee",
                    "email": "conradl@ensemble.com",
                    "external": false,
                    "status": "declined",
                    "id": 95
                }
            ],
            "name": "Sync up",
            "description": "A sync up with the Dahlia Corporation to discuss the Agenda implementation.",
            "createdAt": 1667302643,
            "updatedAt": 1667302643,
            "createdBy": 35,
            "meetingTime": 1667489400,
            "series": false
        }
    ],
    "page": 1
}
```

| Property | Description |
| -------- | ----------- |
| `id` | The ID of the meeting. |
| `source` | An object that contains details about the meeting's location. |
| `source.name` | The name of the source. |
| `source.category` | The category of the source. This value can either be `virtual` for online meetings or `in-person` for in-person meetings. |
| `source.type` | The type of the source. Possible values include `zoom`, `teams`, `slack`, and `skype`. This value is **only** returned for meetings in the `virtual` category. 
| `source.url` | The URL for the source. This value is **only** returned for meetings in the `virtual` category.
| `source.id` | The ID of the source. |
| `invitees` | An array of people invited to the meeting. |
| `invitees.name` | The name of the person invited. |
| `invitees.email` | The email of the person invited. |
| `invitees.external` | A boolean value that shows whether or not the person belongs to the company. |
| `invitees.status` | The status of the person invited to the meeting. This value can be `accepted`, `pending`, or `declined`. |
| `invitees.team` | If applicable, the ID of the team the invitee belongs to. This value is only returned for non-external invitees and if the entire team is invited to the meeting. |
| `invitees.id` | The ID of the person invited. This value is only returned for non-external invitees. |
| `name` | The name of the meeting. |
| `description` | A description of the meeting. |
| `createdAt` | The date and time that the meeting was created. This is represented as a UNIX epoch timestamp. |
| `updatedAt` | The date and time that the meeting was last updated. This is represented as a UNIX epoch timestamp. |
| `createdBy` | The ID of the person who created the meeting. |
| `updatedBy` | The ID of the person who last updated the meeting. |
| `meetingTime` | The date and time that the meeting will take place. This is represented as UNIX epoch timestamp. |
| `series` | A boolean value that shows if the meeting is part of a series. |

## Create a meeting

You can create a meeting for your company by making a POST request to the `/meetings` endpoint.

### API format

```http
POST /meetings
```

### Request

```shell
curl -X POST https://api.ensemble.com/agenda/meetings \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'Client-ID: {API_KEY}' \
-d '{
    "source": 9,
    "invitees": [
        "conradl@ensemble.com", "chrish@dahliacorp.com", "adab@dahliacorp.com"
    ]
    "team": 7,
    "name": "Documentation enhancements",
    "description: "A meeting to discuss enhancements to the Agenda documentation.",
    "meetingTime": 1668078000
}'
```

| Property | Description |
| -------- | ----------- |
| `source` | The ID of the source that you want to use for the meeting. |
| `invitees` | An array of email addresses that correspond with the people you want to invite to the meeting. If `team` is not provided, this value is required. Otherwise, this value is optional. |
| `team` | The ID of the team you want to invite to the meeting. If `invitees` is not provided, this value is required. Otherwise, this value is optional. |
| `name` | The name of the meeting you want to create. |
| `description` | A description of the meeting you want to create. |
| `meetingTime` | The date and time for the meeting. This is represented as a UNIX epoch timestamp.

### Response

A successful response returns HTTP status 201 with details about your newly created meeting.

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
            "email": "stephenc@ensemble.com",
            "external": false,
            "status": "pending",
            "team": 7,
            "id": 13
        },
        {
            "name": "Pierre Noble",
            "email": "pierren@ensemble.com",
            "external": false,
            "status": "pending",
            "team": 7,
            "id": 35
        },
        {
            "name":"Kyouko Sakura",
            "email": "kyoukos@ensemble.com",
            "external": false,
            "status": "pending",
            "team": 7,
            "id": 40
        },               
        {
            "name":"Dmitry Podkolzin",
            "email": "dmitryp@ensemble.com",
            "external": false,
            "status": "pending",
            "team": 7,
            "id": 79
        },
        {
            "name":"Jessica Smith",
            "email": "jessicas@ensemble.com",
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
            "email": "conradl@ensemble.com",
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

| Parameters | Description |
| ---------- | ----------- |
| `id` | The ID of the meeting. This field is automatically generated. |
| `source` | The information about the source. This field is automatically expanded upon, based on the ID provided. |
| `createdBy` | The ID of the user who created the meeting. This field is automatically generated, based on the user who sent the audience creation request. |
| `series` | A boolean value that shows if the meeting is part of a series. If not provided within the request body, it will automatically be set as `false`. |

## Retrieve a specific meeting

You can retrieve a specific meeting for your company by making a GET request to the `/meetings` endpoint and providing the ID of the meeting you want to retrieve in the request path.

### API format

```http
GET /meetings/{MEETING_ID}
```

| Parameter | Description |
| --------- | ----------- |
| `{MEETING_ID}` | The `id` of the meeting you want to retrieve.

### Request

```shell
curl -X GET https://api.ensemble.com/agenda/meetings/387 \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'Client-ID: {API_KEY}'
```

### Response

A successful response returns HTTP status 200 with information about the requested meeting.

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
            "email": "stephenc@ensemble.com",
            "external": false,
            "status": "pending",
            "team": 7,
            "id": 13
        },
        {
            "name": "Pierre Noble",
            "email": "pierren@ensemble.com",
            "external": false,
            "status": "pending",
            "team": 7,
            "id": 35
        },
        {
            "name":"Kyouko Sakura",
            "email": "kyoukos@ensemble.com",
            "external": false,
            "status": "pending",
            "team": 7,
            "id": 40
        },               
        {
            "name":"Dmitry Podkolzin",
            "email": "dmitryp@ensemble.com",
            "external": false,
            "status": "pending",
            "team": 7,
            "id": 79
        },
        {
            "name":"Jessica Smith",
            "email": "jessicas@ensemble.com",
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
            "email": "conradl@ensemble.com",
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

## Update a meeting

You can update a specific meeting for your company by making a PATCH request to the `/meetings` endpoint and providing the ID of the meeting you want to update in the request path.

### API format

```http
PATCH /meetings/{MEETING_ID}
```

| Parameter | Description |
| --------- | ----------- |
| `{MEETING_ID}` | The `id` of the meeting you want to update.

### Request

The following request updates the meeting time from November 10th, 11:00AM to November 10th, 11:30AM.

```shell
curl -X PATCH https://api.ensemble.com/agenda/meetings/387 \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'Client-ID: {API_KEY}' \
-d '{
    "meetingTime": 1668079800
}'
```

### Response

A successful response returns HTTP status 200 with details about your newly updated meeting. Please note how the `meetingTime` value has changed from `1668078000` to `1668079800`.

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
            "email": "stephenc@ensemble.com",
            "external": false,
            "status": "pending",
            "team": 7,
            "id": 13
        },
        {
            "name": "Pierre Noble",
            "email": "pierren@ensemble.com",
            "external": false,
            "status": "pending",
            "team": 7,
            "id": 35
        },
        {
            "name":"Kyouko Sakura",
            "email": "kyoukos@ensemble.com",
            "external": false,
            "status": "pending",
            "team": 7,
            "id": 40
        },               
        {
            "name":"Dmitry Podkolzin",
            "email": "dmitryp@ensemble.com",
            "external": false,
            "status": "pending",
            "team": 7,
            "id": 79
        },
        {
            "name":"Jessica Smith",
            "email": "jessicas@ensemble.com",
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
            "email": "conradl@ensemble.com",
            "external": false,
            "status": "pending",
            "id": 95
        }
    ],
    "name": "Documentation enhancements",
    "description": "A meeting to discuss enhancements to the Agenda documentation.",
    "createdAt": 1667810258,
    "updatedAt": 1667810258,
    "meetingTime": 1668079800,
    "createdBy": 35,
    "series": false
}
```

## Delete a meeting

You can retrieve a specific meeting for your company by making a DELETE request to the `/meetings` endpoint and providing the ID of the meeting you want to delete in the request path.

### API format

```http
DELETE /meetings/{MEETING_ID}
```

| Parameter | Description |
| --------- | ----------- |
| `{MEETING_ID}` | The `id` of the meeting you want to delete.

### Request

```shell
curl -X DELETE https://api.ensemble.com/agenda/meetings/387 \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'Client-ID: {API_KEY}'
```

### Response

A successful response returns HTTP status 204 (No Content) and a blank body.

## Next steps

After reading this guide, you have a better understanding of how to list, create, update, and delete your meetings. For more information on other available endpoints, please read the [API overview guide](./overview.md). To learn how to manage meetings within the UI, please read the [meetings UI guide](#).