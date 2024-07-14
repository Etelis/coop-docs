
---
title: Build and Deploy Game
layout: page
parent: Game
nav_order: 1
---

# Build and Deploy

This document explains the process of building and deploying the Coop-Game to Google Cloud Platform (GCP) App Engine using GitHub Actions. The process is automated and triggered by pushing changes to the `main` branch of the repository.

## Overview

The GitHub Actions workflow performs several steps to ensure that the application is built and deployed seamlessly to App Engine.

1. **Checkout Code**: Retrieves the latest code from the repository to ensure the workflow works with the most recent version.
2. **Set Up JDK 11**: Configures Java Development Kit version 11, which is necessary for building the application.
3. **Authenticate to Google Cloud**: Uses a service account key stored in GitHub Secrets to authenticate to GCP securely.
4. **Install Android SDK and Tools**: Installs the Android SDK and necessary tools required for building the Android application.
5. **Set Up `local.properties`**: Configures the Android SDK directory so that the build process knows where to find the SDK.
6. **Grant Execute Permissions for `gradlew`**: Ensures the Gradle wrapper script is executable, allowing it to be run during the build process.
7. **Build with Gradle**: Uses Gradle to build the application, skipping tests to speed up the process.
8. **Set GCP Project**: Configures the GCP project using the project ID stored in GitHub Secrets.
9. **Deploy to App Engine**: Deploys the application to GCP App Engine using the specified configuration in `app.yaml`.

## Prerequisites

Before using this workflow, ensure you have the following:
- A GCP project with App Engine enabled.
- A service account key with necessary permissions (stored as `GCP_SA_KEY` in GitHub Secrets).
- The GCP project ID (stored as `GCP_PROJECT_ID` in GitHub Secrets).

## Setting Up GitHub Secrets

To set up the necessary GitHub Secrets:
1. Go to your GitHub repository.
2. Click on `Settings`.
3. Click on `Secrets` in the left sidebar.
4. Click on `New repository secret` and add the following secrets:
   - `GCP_SA_KEY`: Your GCP service account key in JSON format.
   - `GCP_PROJECT_ID`: Your GCP project ID.

## Deployment Workflow Explanation

### Step-by-Step Breakdown

1. **Checkout Code**:
   The workflow uses the `actions/checkout@v2` action to checkout the repository code. This ensures that the latest code from the `main` branch is available for the subsequent steps.

2. **Set Up JDK 11**:
   The `actions/setup-java@v2` action sets up JDK 11, specifying the distribution as 'adopt'. This is necessary for compiling and running Java applications.

3. **Authenticate to Google Cloud**:
   The `google-github-actions/auth@v0` action authenticates to Google Cloud using a service account key. The key is stored securely in GitHub Secrets and accessed via `${{ secrets.GCP_SA_KEY }}`.

4. **Install Android SDK and Tools**:
   This step installs the Android SDK and command-line tools required for building Android applications. It involves downloading the tools, setting up the SDK directory, and accepting the necessary licenses.

5. **Set Up `local.properties`**:
   The `local.properties` file is configured to point to the Android SDK directory. This is crucial for ensuring that the build process can locate the SDK.

6. **Grant Execute Permissions for `gradlew`**:
   The `chmod +x ./gradlew` command makes the Gradle wrapper script executable. This allows the workflow to run the script for building the application.

7. **Build with Gradle**:
   The `./gradlew clean assemble -x test --build-cache --quiet` command builds the application using Gradle. The `-x test` flag skips the tests, `--build-cache` enables the build cache, and `--quiet` reduces the amount of output.

8. **Set GCP Project**:
   The `gcloud config set project ${{ secrets.GCP_PROJECT_ID }}` command sets the GCP project to the one specified in the GitHub Secrets.

9. **Deploy to App Engine**:
   The `gcloud app deploy app.yaml --quiet` command deploys the application to GCP App Engine using the configuration specified in the `app.yaml` file.

## app.yaml Configuration

The `app.yaml` file defines the configuration for deploying the application to Google App Engine. Below is an example `app.yaml` file and an explanation of its contents:

```yaml
runtime: java11
env: standard

handlers:
- url: /.*
  script: auto

instance_class: F2

automatic_scaling:
  min_instances: 0
  max_instances: 5
  target_cpu_utilization: 0.6
  target_throughput_utilization: 0.6
```

### Explanation of `app.yaml`

- **runtime: java11**: Specifies that the application will run using Java 11.
- **env: standard**: Indicates that the application will use the standard App Engine environment.
- **handlers**: Defines the URL routing and handling. In this example, all URLs (`url: /.*`) are routed to the default handler (`script: auto`).
- **instance_class: F2**: Specifies the instance class to be used. The F2 class provides more resources than the default F1 class.
- **automatic_scaling**: Configures automatic scaling for the application.
  - **min_instances: 0**: The minimum number of instances to keep running.
  - **max_instances: 5**: The maximum number of instances to scale up to.
  - **target_cpu_utilization: 0.6**: Target CPU utilization for scaling decisions.
  - **target_throughput_utilization: 0.6**: Target throughput utilization for scaling decisions.

### Handling a New Repository

When introducing a new repository, ensure the `app.yaml` file is correctly configured and added to the root of the repository. The deployment process will automatically pick up this file and apply the specified configurations. Ensure that the new repository has the necessary GitHub Secrets (`GCP_SA_KEY` and `GCP_PROJECT_ID`) set up for authentication and deployment to GCP.

## Running the Workflow

To run the workflow, simply push changes to the `main` branch of the repository. The GitHub Actions workflow will automatically trigger and perform the steps outlined above.
