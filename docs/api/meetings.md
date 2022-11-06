# Meetings endpoint

Insert blurb describing what meetings are.

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
GET /meetings?source-type={SOURCE_TYPE}
GET /meetings?team-id={TEAM_ID}
GET /meetings?team-name={TEAM_NAME}
GET /meetings?limit={LIMIT}
GET /meetings?page={PAGE}
```

| Parameter | Description |
| --------- | ----------- |
| `{SOURCE_ID}` | The ID of the source that you want to filter by. |
| `{SOURCE_NAME}` | The name of the source that you want to filter by. |
| `{SOURCE_TYPE}` | The type of source you want to filter by. This value can either be `virtual` or `in-person`. |
| `{TEAM_ID}` | The ID of the team that you want to filter for. |
| `{TEAM_NAME}` | The name of the team that you want to filter for. | 
| `{LIMIT}` | Specifies the number of meetings returned. | 
| `{PAGE}` | Specifies the offset of the pages of meetings returned. |

### Request

The following request will retrieve the last five virtual meetings for the Agenda Documentation team.

```shell
curl -X GET https://api.ensemble.com/agenda/meetings?limit=2&source-type=virtual&team-name=agenda-documentation \
-H 'Authorization: Bearer {ACCESS_TOKEN}'
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
                "name": "Microsoft Teams",
                "type": "virtual",
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
                    "name": "Peter Noble",
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
                "name": "Zoom",
                "type": "virtual",
                "id": 9
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
                    "name": "Peter Noble",
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
| `source.type` | The type of the source. This value can either be `virtual` for online meetings or `in-person` for in-person meetings. |
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

## Create a meetings

## Retrieve a specific meeting

## Update a meeting

## Delete a meeting

## Next steps

After reading this guide, you have a better understanding of how to list, create, update, and delete your meetings. For more information on other available endpoints, please read the [API overview guide](./overview.md). To learn how to 