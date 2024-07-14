---
title: Prolific Survey For Evaluating
layout: page
parent: Addons
---

# Co-op Game Prolific Survey React Application

## Introduction

This repository hosts the React frontend for the Prolific Survey component of the Co-op Game project. The application is designed to streamline the survey process, gathering crucial data for gaming research. It leverages modern web technologies to ensure a responsive and user-friendly experience.

[GitHub Repository](https://github.com/ChenRozenshtein/Coop-Game-Prolific-Survey)


You can access the Prolific Survey platform [here](https://prolific-survey-template-xpdmwwgl7a-lm.a.run.app/)

## Docker Configuration

The Dockerfile configures the environment required to run the application inside a Docker container, utilizing a lightweight Node.js version 14 (slim version) as its base.

### Highlights:

- **Base Image**: Uses `node:14-slim` for a minimal footprint.
- **Working Directory**: Sets `/usr/src/app` as the primary workspace.
- **Application Files**: Copies the entire application into the container.
- **Dependency Management**: Installs `serve` globally to serve static files.
- **Port Configuration**: The application is set to run on port `4200`, ensuring it's ready for web traffic.

## Deploying with Docker to Google Cloud Platform (GCP)

To deploy the Co-op Game Prolific Survey React Application, follow these Docker commands:

1. **Build the Docker Image**

   ```bash
   docker build -t coopgame-prolific-react .
   ```

2. **Tag the Image for GCP Artifact Registry**
   Replace `<project-id>` and `<repo-name>` with your GCP Project ID and Artifact Registry repository name.

   ```bash
   docker tag coopgame-prolific-react:latest europe-docker.pkg.dev/<project-id>/<repo-name>/prolific-survey:latest
   ```

3. **Push the Image to GCP Artifact Registry**
   Authenticate Docker with GCP and push the image.

   ```bash
   gcloud auth configure-docker europe-docker.pkg.dev
   docker push europe-docker.pkg.dev/<project-id>/<repo-name>/prolific-survey:latest
   ```

## Continuous Integration and Deployment (CI/CD) with GitHub Actions

This repository employs GitHub Actions for CI/CD, automating the process of testing, building, and deploying the application.

### Workflow Overview:

- **On Push to Main Branch**: Triggers the workflow when changes are pushed to the `main` branch.
- **Build Step**: Installs dependencies and creates a production build of the React application.
- **Dockerize and Push**: Builds a Docker image from the Dockerfile, tags it, and pushes it to Google Cloud Artifact Registry.
- **Deploy to Cloud Run**: Utilizes the pushed Docker image to deploy the application to Google Cloud Run, ensuring it's accessible over the internet.

### Key GitHub Actions Used:

- `actions/checkout@v2`: Checks out the repository code.
- `actions/setup-node@v2`: Sets up Node.js environment.
- `google-github-actions/setup-gcloud@v0.2.1`: Configures the Google Cloud environment.
- Custom steps for building and deploying the Docker image.

This CI/CD pipeline simplifies the development workflow, allowing for rapid iterations and ensuring that the deployment process is consistent and error-free.
