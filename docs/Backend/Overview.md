---
title: Overview
layout: page
nav_order: 1
parent: Backend
---

## Purpose

This document is intended to serve as a comprehensive manual for the operation and maintenance of the Co-Op World Game API suite, crucial for supporting the game's backend functionalities. The suite is comprised of two main components: the UserUtilitiesAPI and the CoOpGameAPI. Together, these APIs facilitate the essential operations required for managing user data and game mechanics.

## Technologies Used

- **Language:** Python, chosen for its flexibility and efficiency in handling backend logic and serverless functions.
- **Serverless Functions:** Google Cloud Functions, providing scalable and event-driven computing resources.
- **API Gateway:** Google Cloud's API Gateway, acting as the front door for managing, securing, and monitoring access to the APIs.
- **Configuration:** Swagger 2.0, utilized for documenting the APIs in a language-agnostic format.

## UserUtilitiesAPI

The UserUtilitiesAPI is designed to handle operations related to user management and utility functions. It supports various endpoints for managing user information, registration, and status.

- **Host:** `https://usersutilsapi-a3hddi81.ew.gateway.dev`

### Endpoints:

- `/getuser`: Fetches user information based on `user_id`.
- `/getwebsitestatus`: Retrieves the current status of the website.
- `/getexperimenter`: Gathers experimenter information based on a specific code.
- `/Users`: Adds new user records to the database.
- `/RegisterUser`: Updates user registration data.
- `/ResetUser`: Resets user data to a default or initial state.
- `/CreateUsers`: Creates multiple user records in a single operation.

## CoOpGameAPI

The CoOpGameAPI focuses on game-specific functionalities such as managing game records and levels. It provides the necessary endpoints for adding and managing game-related data.

- **Host:** `https://gameapi-a3hddi81.ew.gateway.dev`

### Endpoints:

- `/Games`: Adds game records, encompassing various aspects of game data.
- `/Levels`: Adds level records, allowing for the structuring and management of different stages or levels within a game.

## Objective

The primary goal of this guide is to equip developers, administrators, and support staff with the knowledge required for the effective management, operation, and troubleshooting of the UserUtilitiesAPI and CoOpGameAPI. By understanding the structure, functionalities, and capabilities of these APIs, the team can ensure a smooth, efficient, and scalable backend infrastructure for the Co-Op World Game.
