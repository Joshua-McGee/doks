# Sources endpoint

Insert blurb describing what sources are.

## Getting started

The endpoints used in this guide are part of the Ensemble Agenda APIs. Before continuing, please review the [getting started guide](./getting-started.md) for important information that you need to know in order to successfully make calls to the API, including required headers and how to read example APIs.

## List sources

You can retrieve a list of all the sources for your company by making a GET request to the `/sources` endpoint.

### API format

The `/sources` endpoint supports several query parameters to help filter your results. While these parameters are optional, their usage is **strongly** recommended to help reduce expensive overhead. Making a call to this endpoint without any parameters will retrieve **all** sources available for your company. 

```http
GET /sources
GET /sources?category={CATEGORY}
GET /sources?type={TYPE}
GET /sources?limit={LIMIT}
GET /sources?page={PAGE}
```

| Parameter | Description |
| --------- | ----------- |
| `{CATEGORY}` | The category of source you want to filter by. This value can either be `virtual` or `in-person`. |
| `{TYPE}` | The type of source you want to filter by. This value 
is **only** used by `virtual` sources. Possible values include `zoom`, `slack`, `teams`, and `skype`. |
| `{LIMIT}` | Specifies the number of sources returned. | 
| `{PAGE}` | Specifies the offset of the pages of sources returned. |

### Request

The following request will retrieve the last two created sources for the company.

```shell
curl -X GET https://api.ensemble.com/sources?limit=2 \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'Client-ID: {API_KEY}'
```

### Response

A successful response returns HTTP status 200 with a list of sources based on the query parameter provided in the request path.

```json
{
    "records": [
        {
            "name": "Solis",
            "category": "in-person",
            "id": 8,
            "createdBy": 1,
            "createdAt": 1639498959,
            "updatedAt": 1639498959
        },
        {
            "name": "Pierre's Zoom",
            "category": "virtual",
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
| `category` | The category for the source. This value can either be `virtual` for online meetings or `in-person` for in-person meetings. | 
| `type` | The type for the source. Possible values include `zoom`, `teams`, `slack`, and `skype`. This value is **only** returned for sources in the `virtual` category. 
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

The following request will create a new in-person source for the company.

```shell
curl -X POST https://api.ensemble.com/agenda/sources \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'Client-ID: {API_KEY}' \
-d '{
    "name": "Astrum",
    "category": "in-person"
}'
```

The following request will create a new virtual source for the company.

```shell
curl -X POST https://api.ensemble.com/agenda/sources \
-H 'Content-Type: application/json' \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'Client-ID: {API_KEY}' \
-d '{
    "name": "Documentation team Zoom",
    "category": "virtual",
    "type": "zoom"
}'
```

### Response

A successful response returns HTTP status 200 with the newly created source.

```json

```

## Retrieve a specific source

## Update a source

## Delete a source

## Next steps

After reading this guide, you have a better understanding of how to list, create, update, and delete your sources. For more information on other available endpoints, please read the [API overview guide](./overview.md). To learn how to 