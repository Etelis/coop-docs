---
title: checkWebsiteStatus
layout: page
parent: Functions
grand_parent: Backend
---

# checkWebsiteStatus Function

The `checkWebsiteStatus` function is designed to check the status of a website based on data stored in MongoDB. It handles HTTP GET requests and returns the status of the website.

## URL to Activate

To activate the function, send a GET request to the following URL:
[https://europe-central2-co-op-world-game.cloudfunctions.net/checkWebsiteStatus](https://europe-central2-co-op-world-game.cloudfunctions.net/checkWebsiteStatus)

## Input

The function does not require a specific payload. It relies on environment variables for configuration.

## Output

The function returns a response indicating the status of the website:

- **Success (200 OK)**: `{"status": "ON"}` or `{"status": "OFF"}` or `{"status": "status_error"}`
- **Error (500 Internal Server Error)**: `"An error occurred: <error_message>"` or `"Server selection timeout error: <error_message>"`

## Functions

- **initialize_mongodb()**: Initializes the MongoDB client and connects to the database.
- **fetch_website_status(client, collection)**: Fetches the website status from MongoDB.
- **check_website_status(request)**: Main function to handle the request and return the website status.

## Example Request

```bash
curl -X GET \
  https://europe-central2-co-op-world-game.cloudfunctions.net/checkWebsiteStatus
```