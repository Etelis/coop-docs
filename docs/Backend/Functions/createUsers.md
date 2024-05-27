---
title: createUsers
layout: page
parent: Functions
grand_parent: Backend
---

# createUsers Function

The `createUsers` function is designed to create multiple user records in MongoDB. It handles HTTP POST requests and generates a specified number of unique user records.

## URL to Activate

To activate the function, send a POST request to the following URL:
[https://europe-central2-co-op-world-game.cloudfunctions.net/createUsers](https://europe-central2-co-op-world-game.cloudfunctions.net/createUsers)

## Input

The function expects the following query parameters:

- `experimenter` (required): Name of the experimenter.
- `language` (optional): Language of the users, default is "Hebrew".
- `grade` (optional): Grade of the users, default is "N/A".
- `num` (optional): Number of users to create, default is 50 (maximum is 100).

Example request:

```
POST /createUsers?experimenter=JohnDoe&language=English&grade=10&num=20
```

## Output

The function returns a response indicating the success or failure of the operation:

- **Success (200 OK)**: A list of generated user IDs.
- **Error (400 Bad Request)**: `"Experimenter name was not provided. No codes were generated."`
- **Error (500 Internal Server Error)**: `"MongoDB connection error"` or other relevant error messages.

## Functions

- **initialize_mongodb()**: Initializes the MongoDB client and connects to the database.
- **create_users(collection, experimenter, language, grade, num_users)**: Creates multiple user records in MongoDB.
- **enqueue_to_topic(cloud_function_identifier, request, error_received)**: Enqueues failed operations to a Pub/Sub topic for retry.
- **log_details(request, function_name, status_code, error=None)**: Logs details of each request and error.
- **create_cors_response(status_code=200, body='')**: Creates a response with CORS headers.

## Example Request

```bash
curl -X POST \
  'https://europe-central2-co-op-world-game.cloudfunctions.net/createUsers?experimenter=JohnDoe&language=English&grade=10&num=20'
```
