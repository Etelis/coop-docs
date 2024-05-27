---
title: Prerequisites
layout: page
nav_order: 2
parent: Backend
---

## IAM Roles for Google Cloud Platform (GCP)

To ensure a seamless backend development and operation experience for the Co-Op World Game, specific IAM roles must be assigned within Google Cloud Platform (GCP). These roles enable various capabilities ranging from deploying functions to accessing monitoring data. Below is a detailed list of the necessary roles categorized by their respective services.

### Cloud Functions

- **roles/cloudfunctions.developer**: Necessary for deploying and updating Cloud Functions.
- **roles/cloudfunctions.invoker**: Allows for invoking deployed functions.
- **roles/cloudfunctions.admin**: Grants full management capabilities over Cloud Functions.

### API Gateway

- **roles/apigateway.developer**: Required for creating and modifying API configurations.
- **roles/apigateway.admin**: Provides full administrative capabilities over the API Gateway.

### Monitoring

- **roles/monitoring.viewer**: Offers read-only access to monitoring data, essential for oversight without modification rights.
- **roles/monitoring.editor**: Enables editing of monitoring settings, excluding access controls.

### Cloud Storage

- **roles/storage.objectAdmin**: Allows full control over objects within Cloud Storage, including uploading, deleting, and managing objects.
- **roles/storage.objectCreator**: Permits uploading objects to Cloud Storage, suitable for functions that generate and store data.

### IAM

- **roles/iam.serviceAccountAdmin**: Essential for managing service accounts within the project.
- **roles/iam.serviceAccountUser**: Enables running tasks as a service account, facilitating automated processes and integrations.

## MongoDB Permissions

For operations involving MongoDB, specific permissions are required to access and manage the database effectively. These permissions ensure secure and efficient data handling.

- **Read**: Assign the `read` role in the specific database for querying and retrieving data.
- **Write**: The `readWrite` role is needed for creating, modifying, and deleting data within a database.
- **Admin**: For administrative tasks, including managing database configurations and user permissions, assign either `dbAdmin` or `userAdmin` roles.

## Ensuring Proper Access

Before proceeding with backend development or maintenance tasks, verify that all necessary IAM roles and MongoDB permissions are correctly assigned to your GCP account and database users. This ensures that the development team has the required access to perform their duties efficiently while adhering to best practices for security and data integrity.
