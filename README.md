# NASA_APOD_DATA 🚀

This project houses the code and configuration for an ETL (Extract, Transform, Load) pipeline designed to fetch NASA's Astronomy Picture of the Day (APOD) data and store it in a PostgreSQL database. The pipeline is orchestrated using Apache Airflow, ensuring seamless data flow and scheduling. Additionally, the setup is containerized with Docker and includes Kubernetes configurations for scalable deployment.

## Table of Contents

- [Features](#features) ✨
- [Prerequisites](#prerequisites) 🛠️
- [Installation](#installation) 💻
- [Configuration](#configuration) ⚙️
- [Usage](#usage) 🔧
- [Testing](#testing) 🧪
- [Deployment](#deployment) 📦
- [Contributing](#contributing) 🤝

## Features ✨

- Fetches daily APOD data from NASA's API. 🌠
- Transforms the data into a structured format. 📊
- Loads the data into a PostgreSQL database. 🗄️
- Scheduled to run daily using Apache Airflow. ⏰
- Dockerized for easy deployment. 🐳
- Kubernetes deployment configuration for scalability. ☸️

## Prerequisites 🛠️

Before you begin, ensure you have the following installed:

- Docker
- Docker Compose
- Kubernetes (optional, for deployment)
- Python 3.x
- Apache Airflow
- Astronomer

## Installation 💻

1. Clone the repository:

```bash
git clone https://github.com/snehaapratap/NASA_APOD_DATA.git
cd NASA_APOD_DATA
```

2. Build the Docker image:

```bash
docker build -t snehaapratap/nasa-apod-k8s .
```

## Configuration ⚙️

1. **Airflow Connections**:
   - Create a connection in Airflow for the NASA API with the following details:
     - Conn Id: `nasa_api`
     - Conn Type: `HTTP`
     - Host: `https://api.nasa.gov/`
     - Extra: `{"api_key": "YOUR_NASA_API_KEY"}`

   - Create a connection in Airflow for the PostgreSQL database with the following details:
     - Conn Id: `my_postgres_connection`
     - Conn Type: `Postgres`
     - Host: `postgres_db`
     - Schema: `postgres`
     - Login: `postgres`
     - Password: `postgres`
     - Port: `5432`

2. **Environment Variables**:
   - Ensure the following environment variables are set:
     - `AIRFLOW_HOME`: Path to your Airflow home directory.

## Usage 🔧

1. Start the PostgreSQL service:

```bash
docker-compose up -d postgres
```

2. Initialize the Airflow database using astronomer:

```bash
astro dev init
```

3. Start the Airflow web server :

```bash
astro dev start

```

4. Access the Airflow UI at `http://localhost:8080` and trigger the `nasa_apod_postgres` DAG.

## Testing 🧪

To run the tests, use the following command:

```bash
pytest tests/
```

## Deployment 📦

To deploy the application on Kubernetes, follow these steps:

1. Create the namespace:

```bash
kubectl apply -f k8s/namespace.yml
```

2. Deploy the application:

```bash
kubectl apply -f k8s/deployment.yml
kubectl apply -f k8s/service.yml
```

## Contributing 🤝

Contributions are welcome! Please open an issue or submit a pull request.
