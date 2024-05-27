---
title: registerUser
layout: page
parent: Functions
grand_parent: Backend
---

# registerUser Function

The `registerUser` function is designed to update user registration data in MongoDB. It handles HTTP POST requests and updates the registration information for a specified user.

## URL to Activate

To activate the function, send a POST request to the following URL:
[https://europe-central2-co-op-world-game.cloudfunctions.net/registerUser](https://europe-central2-co-op-world-game.cloudfunctions.net/registerUser)

## Input

The function expects a JSON payload with the user registration data. Below is an example of the expected input:

```json
{
    "user_id": "12345",
    "human_gender": "male",
    "virtual_gender": "female",
    "registration_time": "2023-05-27T12:00:00Z"
}
```

## Output

The function returns a response indicating the success or failure of the operation:

- **Success (200 OK)**: `"User registration data updated successfully."`
- **No Update (404 Not Found)**: `"No such user or no update needed."`
- **Error (500 Internal Server Error)**: `"An error occurred: <error_message>"` or `"MongoDB connection error"`

## Functions

- **initialize_mongodb()**: Initializes the MongoDB client and connects to the database.
- **update_registration_data(collection, registration_data)**: Updates the user registration data in MongoDB.
- **enqueue_to_topic(cloud_function_identifier, request, error_received)**: Enqueues failed operations to a Pub/Sub topic for retry.
- **create_cors_response(status_code=200, body='')**: Creates a response with CORS headers.

## Example Request

```bash
curl -X POST \
  https://europe-central2-co-op-world-game.cloudfunctions.net/registerUser \
  -H 'Content-Type: application/json' \
  -d '{
        "user_id": "12345",
        "human_gender": "male",
        "virtual_gender": "female",
        "registration_time": "2023-05-27T12:00:00Z"
      }'
```