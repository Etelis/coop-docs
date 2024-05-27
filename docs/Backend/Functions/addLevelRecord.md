---
title: addLevelRecord
layout: page
parent: Functions
grand_parent: Backend
---

# addLevelRecord Function

The `addLevelRecord` function is designed to add level records to the database. It handles HTTP POST requests and ensures the data is properly stored in MongoDB, updating user information accordingly.

## URL to Activate

To activate the function, send a POST request to the following URL:
[https://europe-central2-co-op-world-game.cloudfunctions.net/addLevelRecord](https://europe-central2-co-op-world-game.cloudfunctions.net/addLevelRecord)

## Input

The function expects a JSON payload with the level data. Below is an example of the expected input:

```json
{
    "user_id": "12345",
    "level_num": 10,
    "scores": {
        "human_player_score": 1500,
        "ai_player_score": 1400
    },
    "new_record": true,
    "timestamp": "2023-05-27T12:00:00Z"
}
```

## Output

The function returns a response indicating the success or failure of the operation:

- **Success (200 OK)**: `"Data updated successfully."` or `"Level Data saved successfully."`
- **Error (500 Internal Server Error)**: `"Error writing to database"` or other relevant error messages.

## Functions

- **initialize_mongodb()**: Initializes the MongoDB client and connects to the database.
- **update_user_doc_level_completion(collection_users, level_data)**: Updates the user document with level completion information.
- **insert_new_level(collection_levels, level_data)**: Inserts the level data into the MongoDB collection.
- **enqueue_to_topic(cloud_function_identifier, request, error_received)**: Enqueues failed operations to a Pub/Sub topic for retry.
- **log_details(request, function_name, status_code, error=None)**: Logs details of each request and error.
- **create_cors_response(status_code=200, body='')**: Creates a response with CORS headers.

## Example Request

```bash
curl -X POST \
  https://europe-central2-co-op-world-game.cloudfunctions.net/addLevelRecord \
  -H 'Content-Type: application/json' \
  -d '{
        "user_id": "12345",
        "level_num": 10,
        "scores": {
            "human_player_score": 1500,
            "ai_player_score": 1400
        },
        "new_record": true,
        "timestamp": "2023-05-27T12:00:00Z"
      }'
```