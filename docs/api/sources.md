# Sources endpoint

Insert blurb describing what sources are.

## Getting started

The endpoints used in this guide are part of the agenda Agenda APIs. Before continuing, please review the [getting started guide](./getting-started.md) for important information that you need to know in order to successfully make calls to the API, including required headers and how to read example APIs.

## List sources

You can retrieve a list of all the sources for your company by making a GET request to the `/sources` endpoint.

### API format

The `/sources` endpoint supports several query parameters to help filter your results. While these parameters are optional, their usage is **strongly** recommended to help reduce expensive overhead. Making a call to this endpoint without any parameters will retrieve **all** sources available for your company. 

```http
GET /sources
GET /sources?type={TYPE}
GET /sources?limit={LIMIT}
GET /sources?page={PAGE}
```

| Parameter | Description |
| --------- | ----------- |
| `{TYPE}` | The type of source you want to filter by. This value 
is **only** used by `virtual` sources. Possible values include `zoom`, `slack`, `teams`, and `skype`. |
| `{LIMIT}` | Specifies the number of sources returned per page. | 
| `{PAGE}` | Specifies the offset of the pages of sources returned. |

### Request

The following request will retrieve the last two created sources for the company.

```shell
curl -X GET https://api.agenda.com/sources?limit=2 \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'Client-ID: {API_KEY}'
```

### Response

A successful response returns HTTP status 200 with a list of sources based on the query parameter provided in the request path.

```json
{
    "records": [
        {
            "name": "Teams meeting",
            "id": 8,
            "url": "{TEAMS_LINK}",
            "type": "teams",
            "createdBy": 35,
            "createdAt": 1639498959,
            "updatedAt": 1639498959
        },
        {
            "name": "Pierre's Zoom",
            "id": 9,
            "url": "{ZOOM_LINK}",
            "type": "zoom",
            "createdBy": 35,
            "createdAt": 16394999567,
            "updatedAt": 16394999567
        }
    ]
}
```

| Property | Description |
| -------- | ----------- |
| `name` | The name of the source. |
| `type` | The type for the source. Possible values include `zoom`, `teams`, `slack`, and `skype`. |
| `createdBy` | The ID of the user who created the source. |
| `createdAt` | The date and time that the source was created. This is represented as a UNIX epoch timestamp. |
| `updatedAt` | The date and time that the source was updated. This is represented as a UNIX epoch timestamp. |
| `url` | The URL that can be used for the source. This value is **only** returned for sources in the `virtual` category. |

## Create a source

You can create a source for your company by making a POST request to the `/sources` endpoint.

### API format

```http
POST /sources
```

### Request

The following request will create a new source for the company.

```shell
curl -X POST https://api.agenda.com/sources \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'Client-ID: {API_KEY}' \
-d '{
    "name": "Documentation team Zoom",
    "type": "zoom"
}'
```

### Response

A successful response returns HTTP status 200 with the newly created source.

```json
{
    "name": "Documentation team Zoom",
    "id": 13,
    "url": "{ZOOM_URL}",
    "type": "zoom",
    "createdAt": 1668046477,
    "updatedAt": 1668046477
}
```

## Retrieve a specific source

You can retrieve a specific source for your company by making a GET request to the `/sources` endpoint and providing the ID of the source you want to retrieve in the request path.

### API format

```http
GET /sources/{SOURCE_ID}
```

| Parameter | Description |
| --------- | ----------- |
| `{SOURCE_ID}` | The `id` of the source you want to retrieve.

### Request

```shell
curl -X GET https://api.agenda.com/sources/13 \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'Client-ID: {API_KEY}'
```

### Response

A successful response returns HTTP status 200 with information about the requested source.

```json
{
    "name": "Documentation team Zoom",
    "id": 13,
    "url": "{ZOOM_URL}",
    "type": "zoom",
    "createdAt": 1668046477,
    "updatedAt": 1668046477
}
```

## Update a source

You can update a specific source for your company by making a PATCH request to the `/sources` endpoint and providing the ID of the source you want to update in the request path.

### API format

```http
PATCH /sources/{SOURCE_ID}
```

| Parameter | Description |
| --------- | ----------- |
| `{SOURCE_ID}` | The `id` of the source you want to update.

### Request

The following request updates the source name from "Documentation team Zoom" to "Documentation Team Standup Zoom".

```shell
curl -X PATCH https://api.agenda.com/sources/13 \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'Client-ID: {API_KEY}' \
-d '{
    "name": "Documentation Team Standup Zoom"
}'
```

### Response

A successful response returns HTTP status 200 with details about your newly updated source.

```json
{
    "name": "Documentation Team Standup Zoom",
    "id": 13,
    "url": "{ZOOM_URL}",
    "type": "zoom",
    "createdAt": 1668046477,
    "updatedAt": 1668047781
}
```

## Delete a source

You can delete a specific source for your company by making a DELETE request to the `/sources` endpoint and providing the ID of the source you want to delete in the request path.

### API format

```http
DELETE /sources/{SOURCE_ID}
```

| Parameter | Description |
| --------- | ----------- |
| `{SOURCE_ID}` | The `id` of the source you want to delete.

### Request

```shell
curl -X DELETE https://api.agenda.com/sources/13 \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'Client-ID: {API_KEY}'
```

### Response

A successful response returns HTTP status 204 (No Content) and a blank body.

## Next steps

After reading this guide, you have a better understanding of how to list, create, update, and delete your sources. For more information on other available endpoints, please read the [API overview guide](./overview.md). To learn how to 