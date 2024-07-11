---
title: POST_Retry_Worker
layout: page
parent: Functions
grand_parent: Backend
---

# POST_Retry_Worker Function

The `POST_Retry_Worker` function is designed to dequeue and retry POST requests for failed cloud functions. It handles HTTP POST requests and schedules the retries using Google Cloud Scheduler.

## URL to Activate

To activate the function, send a POST request to the following URL:
[https://europe-central2-co-op-world-game.cloudfunctions.net/POST_Retry_Worker](https://europe-central2-co-op-world-game.cloudfunctions.net/POST_Retry_Worker)

## Input

The function expects a JSON payload with the retry data. Below is an example of the expected input:

```json
{
    "cloudFunctionIdentifier": "addGameRecord",
    "request": {
        "url": "https://europe-central2-co-op-world-game.cloudfunctions.net/",
        "headers": {
            "Content-Type": "application/json"
        },
        "body": {
            "player_id": "12345",
            "score": 1000,
            "level": 5,
            "timestamp": "2023-05-27T12:00:00Z"
        }
    }
}
```

## Output

The function returns a response indicating the success or failure of the operation:

- **Success (200 OK)**: `"POST_Retry_Worker function executed."`
- **Error (400 Bad Request)**: `"Failed to parse message data."`
- **Error (500 Internal Server Error)**: `"Exception while scheduling retry."` or other relevant error messages.

## Functions

- **POST_Retry_Worker(request)**: Dequeues and retries POST requests, schedules retries using Google Cloud Scheduler.

## Example Request

```bash
curl -X POST   https://europe-central2-co-op-world-game.cloudfunctions.net/POST_Retry_Worker   -H 'Content-Type: application/json'   -d '{
        "cloudFunctionIdentifier": "addGameRecord",
        "request": {
            "url": "https://europe-central2-co-op-world-game.cloudfunctions.net/",
            "headers": {
                "Content-Type": "application/json"
            },
            "body": {
                "player_id": "12345",
                "score": 1000,
                "level": 5,
                "timestamp": "2023-05-27T12:00:00Z"
            }
        }
      }'
```