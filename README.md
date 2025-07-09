# Docker Compose Test Project

## Description

This is a simple Node.js Express application demonstrating a basic API with PostgreSQL as the database, orchestrated using Docker Compose.

## Features

-   **Node.js Express API**: A lightweight web server handling API requests.
-   **PostgreSQL Database**: A relational database for storing application data.
-   **Docker Compose**: For easy setup and management of the application and database services.
-   **Basic CRUD Operations**: Endpoints for creating, reading, and setting up a `schools` table.

## Technologies Used

-   Node.js
-   Express.js
-   PostgreSQL
-   Docker
-   Docker Compose

## Setup Instructions

To get this project up and running on your local machine, follow these steps:

1.  **Clone the repository**:

    ```bash
    git clone https://github.com/your-username/docker-compose-test.git
    cd docker-compose-test
    ```

2.  **Start the services using Docker Compose**:

    This command will build the Node.js application image (if not already built) and start both the Node.js app and PostgreSQL database containers.

    ```bash
    docker compose up -d --build
    ```

    -   The Node.js application will be accessible on `http://localhost:13000`.
    -   The PostgreSQL database will be accessible on port `5433` on your host machine.

3.  **Initialize the database (create the `schools` table)**:

    Once the services are running, you need to create the necessary table in the database. Run the following command:

    ```bash
    curl http://localhost:13000/setup
    ```

    You should see a response like: `{"message":"Successfully created table"}`

## API Endpoints

The application exposes the following API endpoints:

-   **`GET /`**
    -   **Description**: Retrieves all records from the `schools` table.
    -   **Response**: `{"children":[]}` (or an array of school objects if data exists)
    -   **Example**:
        ```bash
        curl http://localhost:13000/
        ```

-   **`POST /`**
    -   **Description**: Adds a new school record to the `schools` table.
    -   **Request Body**: JSON object with `name` and `location` fields.
        ```json
        {
          "name": "Example School",
          "location": "Example City"
        }
        ```
    -   **Response**: `{"message":"Successfully added child"}`
    -   **Example**:
        ```bash
        curl -X POST -H "Content-Type: application/json" -d '{"name":"My School","location":"My City"}' http://localhost:13000/
        ```

-   **`GET /setup`**
    -   **Description**: Creates the `schools` table if it does not already exist. This endpoint is idempotent and can be run multiple times without error.
    -   **Response**: `{"message":"Successfully created table"}`
    -   **Example**:
        ```bash
        curl http://localhost:13000/setup
        ```

## Running Tests

This project includes a `test.rest` file with example API requests. While IDE extensions (like "REST Client" for VS Code) are ideal for running these, you can also manually test the endpoints using `curl` as shown in the API Endpoints section above.

```bash
# Example of using curl for GET request
curl http://localhost:13000/

# Example of using curl for POST request
curl -X POST -H "Content-Type: application/json" -d '{"name":"Test School","location":"Test Location"}' http://localhost:13000/
```

---

Feel free to contribute or report issues!