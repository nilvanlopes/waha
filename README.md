# WAHA - WhatsApp HTTP API

This project sets up the [WAHA (WhatsApp HTTP API)](https://waha.devlike.pro/) using Docker. WAHA allows you to interact with WhatsApp through an HTTP API.

## Prerequisites

- Docker
- Docker Compose

## Setup

1.  **Clone the repository or download the files.**
2.  **Review the existing `.env` file:**

3.  **Adjust your `.env` file if needed:**

    Open the `.env` file and fill in the required environment variables, such as `WAHA_API_KEY`, `WAHA_DASHBOARD_USERNAME`, and `WAHA_DASHBOARD_PASSWORD`. You can generate strong random values for these.

4.  **Review the `docker-compose.yml` file:**

    The `docker-compose.yml` file is configured to use the variables from your `.env` file. You can customize the services and volumes as needed.

## Usage

1.  **Start the services:**

    ```bash
    make deploy-waha
    ```

    Or, if you're not using the repository Makefile:

    ```bash
    docker compose up -d
    ```

2.  **Access the WAHA Dashboard:**

    Open your browser and navigate to `http://waha.localnetwork:8181` on the LAN or `http://localhost:3000` if you are testing the container directly. You should see the WAHA dashboard.

3.  **Access the Swagger UI:**

    The Swagger UI for the WhatsApp API is available at `http://localhost:3000/swagger`.

## Configuration

The main configuration is done through the `.env` file. Here are some of the key variables:

-   `WAHA_API_KEY`: Your API key for securing the WAHA API.
-   `WAHA_DASHBOARD_USERNAME`: Username for the WAHA dashboard.
-   `WAHA_DASHBOARD_PASSWORD`: Password for the WAHA dashboard.
-   `WHATSAPP_DEFAULT_ENGINE`: The WhatsApp engine to use (e.g., `WEBJS`, `GOWS`).
-   `WAHA_BASE_URL`: The base URL for the API.
-   `WHATSAPP_HOOK_URL`: The URL for webhook notifications.

For more detailed configuration options, please refer to the [official WAHA documentation](https://waha.devlike.pro/docs/how-to/config/).

## Stopping the services

To stop the services, run:

```bash
docker-compose down
```

## Data Persistence

-   **Sessions:** Session data is stored in the `sessions` directory, mounted as a volume.
-   **Media:** Media files are stored in the `media` directory, mounted as a volume.

## Notes for this repository

-   The stack is designed to join the external `n8n` network used by the other services in this monorepo and the external `traefik-local` network for LAN-only access.
-   The root `make deploy` target already creates the `n8n` and `traefik-local` networks before deploying `waha`.
