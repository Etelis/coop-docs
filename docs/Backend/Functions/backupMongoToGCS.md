---
title: backupMongoToGCS
layout: page
parent: Functions
---

# backupMongoToGCS Function

The `backupMongoToGCS` function is designed to back up MongoDB collections to Google Cloud Storage (GCS). It handles HTTP requests and exports the data from MongoDB, saving it as JSON files in a specified GCS bucket.

## URL to Activate

To activate the function, send a request to the following URL:
[https://europe-central2-co-op-world-game.cloudfunctions.net/backupMongoToGCS](https://europe-central2-co-op-world-game.cloudfunctions.net/backupMongoToGCS)

## Input

The function does not require a specific payload. It relies on environment variables for configuration.

## Output

The function returns a response indicating the success or failure of the operation:

- **Success (200 OK)**: `"Backup completed successfully"`
- **Error (500 Internal Server Error)**: `"An error occurred: <error_message>"` or `"Backup bucket name is not set in environment variables"`

## Functions

- **backup_mongo_to_gcs(request)**: Main function to handle the backup process.
- **validate_bucket_name(bucket_name)**: Ensures the bucket name is provided.
- **connect_to_mongo(mongo_conn_str, mongo_db_name)**: Establishes a connection to MongoDB.
- **export_data_to_gcs(storage_client, bucket_name, collections)**: Exports data from MongoDB collections to GCS.

## Example Request

```bash
curl -X POST \
  https://europe-central2-co-op-world-game.cloudfunctions.net/backupMongoToGCS
```
