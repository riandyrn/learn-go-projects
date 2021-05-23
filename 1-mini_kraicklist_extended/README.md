# Mini Kraicklist Extended

In this exercise we will try to extend the capability of Mini Kraicklist API server from previous exercise.

In this exercise we will also now includes following APIs:

- [Update Ad](#update-ad)
- [Delete Ad](#delete-ad)
- [Get Ad Statistics](#get-ad-statistics)

Beside including above APIs, we will also modify [Get Latest Ads](#get-latest-ads) to:

- accept limit value from query parameter
- return latest updated ads instead newly created ads

Please check below sections for complete new API design.

Your tasks:

1. Implement new API design
2. Separate components in your code to packages (e.g `Storage` should be on `storage` package not `main`)
3. Create test files for each components

---

## Post New Ad

POST: `/ads`

This API is used for posting new ad.

**Request Body:**

- `title`, String => title of the ad
- `body`, String => body of the ad contains descriptions
- `tags`, Array of String, _optional_ => related tags for the ad if any

**Sample Request:**

```json
GET: /ads
Content-Type: application/json

{
    "title": "Porsche Carrera GT 2016 for Sale",
    "body": "Clean body & great engine!",
    "tags": [
        "car",
        "porsche",
        "porsche 2016"
    ]
}
```

**Success Response:**

```json
HTTP/1.1 200 OK
Content-Type: application/json

{
    "success": true,
    "data": {
        "id": 1282323,
        "title": "Porsche Carrera GT 2016 for Sale",
        "body": "Clean body & great engine!",
        "tags": [
            "car",
            "porsche",
            "porsche 2016"
        ],
        "created_at": 1581931121
    }
}
```

**Error Responses:**

- Bad Request

    ```json
    HTTP/1.1 400 Bad Request
    Content-Type: application/json

    {
        "success": false,
        "err": "ERR_BAD_REQUEST",
        "message": "field `title` cannot be empty"
    }
    ```

[Back to Top](#mini-kraicklist-extended)

---

## Get Latest Ads

GET: `/ads?limit=<limit>`

This API is used for getting latest ads from database.

If `limit` value is not specified, by default the value is `5`.

**Sample Request:**

```json
GET: /ads?limit=10
```

**Success Response:**

```json
HTTP/1.1 200 OK
Content-Type: application/json

{
    "success": true,
    "data": {
        "ads": [
            {
                "id": 1282323,
                "title": "Porsche Carrera GT 2016 for Sale",
                "body": "Clean body & great engine!",
                "tags": [
                    "car",
                    "porsche",
                    "porsche 2016"
                ],
                "created_at": 1581931121,
                "updated_at": 1581931121
            }
        ]
    }
}
```

**Error Responses:**

No specific error responses

[Back to Top](#mini-kraicklist-extended)

---

## Update Ad

PUT: `/ads/<ad_id>`

This API is used for updating ad.

**Request Body:**

- `title`, String, _optional_ => updated title of the ad
- `body`, String, _optional_ => updated body of the ad
- `tags`, Array of String, _optional_ => updated related tags for the ad

**Sample Request:**

```json
PUT: /ads/1282323
Content-Type: application/json

{
    "title": "Porsche Carrera GT 2016 & 2017 for Sale!",
    "body": "Both of them have clean body & great engine!",
    "tags": [
        "car",
        "porsche",
        "porsche 2016",
        "porsche 2017"
    ]
}
```

**Success Response:**

```json
HTTP/1.1 200 OK
Content-Type: application/json

{
    "success": true,
    "data": {
        "id": 1282323,
        "title": "Porsche Carrera GT 2016 & 2017 for Sale!",
        "body": "Both of them have clean body & great engine!",
        "tags": [
            "car",
            "porsche",
            "porsche 2016",
            "porsche 2017"
        ],
        "updated_at": 1582000607
    }
}
```

**Error Responses:**

- Bad Request

    ```json
    HTTP/1.1 400 Bad Request
    Content-Type: application/json

    {
        "success": false,
        "err": "ERR_BAD_REQUEST",
        "message": "at least one parameter must be specified"
    }
    ```

- Not Found

    ```json
    HTTP/1.1 404 Not Found
    Content-Type: application/json

    {
        "success": false,
        "err": "ERR_NOT_FOUND",
        "message": "data is not found"
    }
    ```

[Back to Top](#mini-kraicklist-extended)

---

## Delete Ad

DELETE: `/ads/<ad_id>`

This API is used for deleting ad. The ad will be literally deleted from database.

**Sample Request:**

```json
DELETE /ads/1282323
```

**Success Response:**

```json
HTTP/1.1 200 OK
Content-Type: application/json

{
    "success": true,
    "data": {
        "id": 1282323
    }
}
```

**Error Responses:**

- Not Found

    ```json
    HTTP/1.1 404 Not Found
    Content-Type: application/json

    {
        "success": true,
        "err": "ERR_NOT_FOUND",
        "message": "data is not found"
    }
    ```

[Back to Top](#mini-kraicklist-extended)

---

## Get Ad Statistics

GET: `/stats`

This API is used for fetching ads statistic. Currently we will only show total ads in statistic.

**Sample Request:**

```json
GET /stats
```

**Success Response:**

```json
HTTP/1.1 200 OK
Content-Type: application/json

{
    "success": true,
    "data": {
        "stats": {
            "total_ads": 1
        }
    }
}
```

**Error Responses:**

No specific error response

[Back to Top](#mini-kraicklist-extended)

---
