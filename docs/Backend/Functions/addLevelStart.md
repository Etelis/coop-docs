---
title: addLevelStart
layout: page
parent: Functions
---

# addLevelStart Function

The `addLevelStart` function is designed to record the start of a level. It handles HTTP POST requests and ensures the data is properly stored in MongoDB.

## URL to Activate

To activate the function, send a POST request to the following URL:
[https://europe-central2-co-op-world-game.cloudfunctions.net/addLevelStart](https://europe-central2-co-op-world-game.cloudfunctions.net/addLevelStart)

## Input

The function expects a JSON payload with the level start data. Below is an example of the expected input:

```json
{
    "user_id": "12345",
    "level_num": 5,
    "timestamp": "2023-05-27T12:00:00Z"
}
```

## Output

The function returns a response indicating the success or failure of the operation:

- **Success (200 OK)**: `"Data saved successfully."`
- **Error (500 Internal Server Error)**: `"Error writing to database"` or other relevant error messages.

## Functions

- **initialize_mongodb()**: Initializes the MongoDB client and connects to the database.
- **add_levels_start_record(collection, level_start_data)**: Inserts the level start data into the MongoDB collection.
- **enqueue_to_topic(cloud_function_identifier, request, error_received)**: Enqueues failed operations to a Pub/Sub topic for retry.
- **log_details(request, function_name, status_code, error=None)**: Logs details of each request and error.
- **create_cors_response(status_code=200, body='')**: Creates a response with CORS headers.

## Example Request

```bash
curl -X POST \
  https://europe-central2-co-op-world-game.cloudfunctions.net/addLevelStart \
  -H 'Content-Type: application/json' \
  -d '{
        "user_id": "12345",
        "level_num": 5,
        "timestamp": "2023-05-27T12:00:00Z"
      }'
```
