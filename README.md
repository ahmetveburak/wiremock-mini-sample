
- **docker-compose.yml**: Configuration file for Docker Compose to set up the WireMock service.
- **Makefile**: Contains commands to manage the Docker containers.
- **mappings/**: Directory containing the API mappings for WireMock.
- **responses/**: Directory containing the JSON response files for the API mappings.

## Getting Started

### Prerequisites

- Docker
- Docker Compose

### Setup

1. Clone the repository:
    ```sh
    git clone <repository-url>
    cd <repository-directory>
    ```

2. Start the WireMock server:
    ```sh
    make up
    ```

3. Check the logs (optional):
    ```sh
    make logs
    ```

4. Stop the WireMock server:
    ```sh
    make down
    ```

5. Restart the WireMock server:
    ```sh
    make restart
    ```

### API Endpoints

The following endpoints are available for testing:

- **POST /service-1/api/validate**
  - Response: `responses/service-1/validate.json`
  - Status: 200

- **POST /service-1/api/validate-body**
  - Response: `responses/service-1/validate.json`
  - Status: 200

- **POST /service-2/api/create**
  - Response: `responses/service-2/create.json`
  - Status: 201

### Example Requests

You can test the endpoints using `curl`:

```sh
curl -X POST http://localhost:8080/service-1/api/validate
curl -X POST http://localhost:8080/service-1/api/validate-body
curl -X POST http://localhost:8080/service-2/api/create

# Body validation - Require "data" field
curl -X POST http://localhost:8080/service-1/api/validate -d '{"data": "John Doe"}'
# Error - Missing body
curl -X POST http://localhost:8080/service-1/api/validate

# Accepts any request body
curl -X POST http://localhost:8080/service-2/api/create -d '{"name": "John Doe"}' 
```