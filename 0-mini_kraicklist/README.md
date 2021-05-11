# Mini Kraicklist

In this exercise we will learn how to create simple REST API using Go.

We are trying to create API for imaginary classified ads website called Kraicklist (pun of Craigslist). The idea is user could post new ads & get latest ads from it.

Please check upcoming sections for details of API design.

Your tasks:

1. Implement the server API using Go & MySQL
2. Containerize your server API using Docker
3. Create deployment template using Docker Compose which include the deployment script for your server & MySQL server

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

[Back to Top](#mini-kraicklist)

---

## Get Latest Ads

GET: `/ads`

This API is used for getting maximum `5` latest ads from database.

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
                "created_at": 1581931121
            }
        ]
    }
}
```

[Back to Top](#mini-kraicklist)

---
