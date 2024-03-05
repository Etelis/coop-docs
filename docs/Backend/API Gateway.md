---
title: API Gateway
layout: page
parent: Backend
---

## API Gateway in Co-Op World Game Development

An API Gateway acts as the main entry point for clients to access various services within the Co-Op World Game application. It efficiently routes incoming HTTP requests to the appropriate Cloud Functions or other backend services, providing a streamlined approach to managing and securing access to the game's functionalities.

### Configuring API Gateway

The configuration of the API Gateway is done through YAML files, which specify the routes, methods, and backend services for the APIs. This setup allows for a clear and manageable way to direct traffic to the correct endpoints and services based on the incoming requests.

### Existing API Gateways

The Co-Op World Game utilizes two main API Gateways:

#### CoOpGameAPI

- **Managed Service URL**: `https://coop-game-api-cors-v2-a3hddi81.ew.gateway.dev`
- **Creation Date**: 12/09/2023

#### UserUtilitiesAPI

- **Managed Service URL**: `https://usersutilsapi-a3hddi81.ew.gateway.dev`
- **Creation Date**: 12/09/2023

### CoOpGameAPI Endpoints

The CoOpGameAPI provides endpoints for managing game records, levels, and user registrations:

- `POST /Games`: Adds game records.
- `POST /Levels`: Adds level records.
- `POST /RegisterUser`: Registers a new user.
- `POST /Users`: Adds new user records.
- `GET /GetUser`: Fetches user information.
- `GET /GetWebsiteStatus`: Retrieves the current status of the website.

### UserUtilitiesAPI Endpoints

The UserUtilitiesAPI is designed for user management and utility functions:

- `GET /GetExperimenter`: Fetches experimenter information.
- `POST /CreateUsers`: Creates multiple user records.
- `POST /ResetUser`: Resets user data.

### Accessing API Gateway

To access the APIs, use the managed service URLs provided during the API Gateway creation process. This URL serves as the primary endpoint for interacting with the respective API functionalities.

### Example Configuration File for UserUtilitiesAPI

The YAML configuration file for the UserUtilitiesAPI outlines the paths, methods, and backend addresses for the API. Key elements include:

- **host**: Specifies the API Gateway URL.
- **paths**: Defines available routes and their configurations.
  - **get**: Describes the HTTP method for the route.
  - **x-google-backend**: Points to the backend address.
  - **parameters**: Lists input parameters for the endpoint.
  - **responses**: Describes expected responses from the API.

```yaml
swagger: '2.0'
info:
  version: '1.0'
  title: 'UserUtilitiesAPI'
host: 'user-utils-api.apigateway.co-op-world-game.cloud.goog'
schemes:
  - 'https'
paths:
  /getuser:
    summary: 'Fetch user information based on user_id'
    operationId: 'fetchUserInfo'
    x-google-backend:
      address: 'https://europe-centra12-co-op-world-game.cloudfunctions.net/fetchUserInfo'
    parameters:
      - name: 'user_id'
        in: 'query'
        description: 'The ID of the user to fetch.'
        required: true
        type: 'string'
    responses:
      200:
        description: 'Successful operation'
