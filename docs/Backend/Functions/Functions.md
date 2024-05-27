---
title: Functions
layout: default
parent: Backend
has_children: true
---

# Cloud Functions Guide for Co-Op World Game Development

Cloud Functions provide a scalable, efficient, and serverless way to execute backend code for the Co-Op World Game. This guide covers the setup, usage, and testing of Cloud Functions, specifically tailored for game development tasks.

## Introduction to Cloud Functions

Cloud Functions are single-purpose, serverless functions that run in the cloud in response to events. This serverless execution model is ideal for dynamic and scalable backend services, such as those required in game development.

## Setting Up Cloud Functions

### Step 1: Enabling Cloud Functions API

To begin, you must enable the Cloud Functions API in your Google Cloud project:

1. Access the [Google Cloud Console](https://console.cloud.google.com/).
2. Select or create a project for your Cloud Functions.
3. Navigate to **APIs & Services** and click on **+ ENABLE APIS AND SERVICES**.
4. Search for and enable the **Cloud Functions API**.

### Step 2: Creating and Deploying Functions

Creating a Cloud Function involves the following steps:

1. In the main menu, navigate to **Compute > Cloud Functions**.
2. Click on **CREATE FUNCTION**.
3. Configure your function with the following settings:
   - **Name**: A unique identifier.
   - **Memory Allocated**: Select based on the requirements.
   - **Trigger**: Choose the invocation method (e.g., HTTP, Cloud Pub/Sub).
   - **Runtime**: Select the programming language, such as Python.

### Step 3: Function Configuration

Configure your function with necessary runtime environment variables, including details for MongoDB connections and any other specific settings needed for operation.

### Step 4: Implementing a Fallback Mechanism

Develop a fallback mechanism using `enqueue_to_topic()` function to handle failures, ensuring messages are retried using a function like `POST_Retry_Worker`.

## Common Functions and Initialization

### MongoDB Initialization

Use the `initialize_mongodb()` function to set up a connection to MongoDB, properly handling any connection issues and ensuring the client and collection are ready for operations.

\`\`\`python
# Initialize MongoDB client
def initialize_mongodb():
    try:
        # Environment variables
        MONGO_CONNECTION = os.environ.get('MONGO_CONNECTION')
        MONGO_DB_NAME = os.environ.get('MONGO_DB_NAME')
        MONGO_COLLECTION_NAME = os.environ.get('MONGO_COLLECTION_NAME')

        client = MongoClient(MONGO_CONNECTION, serverSelectionTimeoutMS=5000)
        client.server_info()
        db = client[MONGO_DB_NAME]
        collection = db[MONGO_COLLECTION_NAME]
        return client, collection
    except Exception as err:
        return None, err
\`\`\`

### Fallback Mechanism: Enqueue to Topic

`enqueue_to_topic()` ensures failed operations are queued for retry, maintaining data integrity and operational reliability.

\`\`\`python
# Function to enqueue message to Topic
def enqueue_to_topic(cloud_function_identifier, request, error_received):
    # Initialize Pub/Sub Publisher with environment variables
    topic_id = os.environ.get('PUBSUB_TOPIC_ID')
    project_id = os.environ.get('GCP_PROJECT_ID')  # Get project ID from environment variable
    publisher = pubsub_v1.PublisherClient()
    topic_path = f"projects/{project_id}/topics/{topic_id}"

    message_data = {
        "cloudFunctionIdentifier": cloud_function_identifier,
        "request": {
            "headers": dict(request.headers),
            "body": request.get_data(as_text=True),
            "method": request.method,
            "url": request.url,
        },
        "errorReceived": str(error_received)
    }
    
    message_data_str = json.dumps(message_data)
    publisher.publish(topic_path, message_data_str.encode("utf-8"))
\`\`\`
