---
title: PDF Generator
layout: page
parent: Addons
---

# PDF Generator Cloud Function

## Introduction

This repository contains the source code and configuration for the `PDFGenerator` cloud function. This function is designed to generate PDFs based on input data, leveraging various cloud services for data storage, messaging, and deployment. The function is written in Python and is deployed on Google Cloud Functions.

## Cloud Function Configuration

The `main.py` script defines the core functionality of the PDFGenerator function, while `requirements.txt` lists the necessary Python dependencies.

### Highlights:

- **Runtime**: Python 3.9
- **Trigger**: HTTP trigger allowing all HTTP requests
- **Environment Variables**: Configured to use specific MongoDB connection details, Pub/Sub topic, and Google Cloud Project ID.

## Environment Variables

The function uses several environment variables to configure its connections and other settings:

- **MONGO_CONNECTION**: Connection string for MongoDB.
- **MONGO_DB_NAME**: Database name in MongoDB.
- **MONGO_COLLECTION_NAME**: Collection name in MongoDB.
- **PUBSUB_TOPIC_ID**: ID of the Pub/Sub topic for messaging.
- **GCP_PROJECT_ID**: Google Cloud Project ID.

## Continuous Integration and Deployment (CI/CD) with GitHub Actions

GitHub Actions automates the CI/CD process for testing, building, and deploying the function to Google Cloud Functions.

### Workflow Overview:

- **On Push to Main Branch**: Activates the workflow when changes are pushed to the `main` branch.
- **Setup Python Environment**: Configures the Python environment and installs dependencies.
- **Authenticate with Google Cloud**: Uses service account credentials to authenticate with Google Cloud.
- **Deploy to Google Cloud Functions**: Deploys the function using the `gcloud` command-line tool.

### Key GitHub Actions Used:

- `actions/checkout@v2`: Checks out the code for the GitHub repository.
- `actions/setup-python@v2`: Prepares the Python environment.
- `google-github-actions/auth@v0.4.0`: Authenticates with Google Cloud using a service account key.
- `google-github-actions/setup-gcloud@v0.2.1`: Sets up the Google Cloud SDK.
- Custom steps for deploying the function to Google Cloud Functions.

### Example Workflow File (deploy.yml)

```yaml
name: Deploy to Google Cloud Functions

on:
  push:
    branches:
      - main

jobs:
  build-and-deploy:
    name: Build and Deploy to Google Cloud Functions
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repo
        uses: actions/checkout@v2

      - name: Setup Python
        uses: actions/setup-python@v2
        with:
          python-version: '3.x'

      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt

      - name: Setup GCloud Auth
        uses: google-github-actions/auth@v0.4.0
        with:
          credentials_json: ${{ secrets.GCP_SA_KEY }}

      - name: Set up Cloud SDK
        uses: google-github-actions/setup-gcloud@v0.2.1
        with:
          version: 'latest'
          export_default_credentials: true
        env:
          GOOGLE_APPLICATION_CREDENTIALS: ${{ secrets.GCP_SA_KEY }}

      - name: Deploy to Cloud Functions
        run: |
          gcloud functions deploy PDFGenerator             --runtime python39             --trigger-http             --allow-unauthenticated             --set-env-vars MONGO_CONNECTION=${{ secrets.MONGO_CONNECTION }},MONGO_DB_NAME=${{ secrets.MONGO_DB_NAME }},MONGO_COLLECTION_NAME=${{ secrets.MONGO_COLLECTION_NAME }},PUBSUB_TOPIC_ID=${{ secrets.PUBSUB_TOPIC_ID }},GCP_PROJECT_ID=${{ secrets.GCP_PROJECT_ID }}
```

## Setting Up the Repository

To get started with this repository:

1. **Clone the Repository:**

   ```bash
   git clone <your-repository-url>
   cd <repository-name>
   ```

2. **Initialize the Git Repository:**

   ```bash
   git init
   git remote add origin <your-repository-url>
   ```

3. **Create .github/workflows Directory:**

   ```bash
   mkdir -p .github/workflows
   ```

4. **Add the Workflow File:**

   Create a file named `deploy.yml` in the `.github/workflows` directory with the content provided above.

5. **Add All Files to the Repository:**

   ```bash
   git add .
   git commit -m "Initial commit with cloud function and deployment workflow"
   git push -u origin main
   ```

## Adding Repository Secrets

You will need to add the following secrets to your GitHub repository settings:

- `GCP_SA_KEY`: Service account key in JSON format
- `MONGO_CONNECTION`
- `MONGO_DB_NAME`
- `MONGO_COLLECTION_NAME`
- `PUBSUB_TOPIC_ID`
- `GCP_PROJECT_ID`

This setup ensures that your cloud function is deployed to Google Cloud Functions with the specified environment variables each time you push to the main branch.
