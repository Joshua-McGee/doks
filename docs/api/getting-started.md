# Getting started with Agenda APIs

The Ensemble Agenda application is developed with an "API-first" mindset. With the Agenda APIs, you can programmatically perform basic CRUD (Create, Read, Update, Delete) operations against all the various endpoints.

The APIs for the Agenda application all share the same set of authentication headers and use similar syntaxes for their CRUD operations. The following guide outlines the necessary steps for getting started with the Agenda APIs.

## Authentication and headers

In order to authenticate and make calls with the Agenda APIs, you will need to complete the [authentication tutorial](./authentication.md). Once you have completed the tutorial, you will be able to use the following headers:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `Client-ID: {API_KEY}`

### Content-Type header

All requests with a payload in the request body (such as POST and PATCH calls) must include a `Content-Type` header. Accepted values are specific to each API endpoint. 

## Reading sample API calls

