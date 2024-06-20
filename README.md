# Aware BSF Setup
The Breaching Simulation Framework uses Docker Compose to set up a multi-container application. It includes three services: an API, a front-end, and a MongoDB database. Docker Compose will help set up with ease. You can follow the instructions to [Installation](#installation).

## Table of Contents
- [Services](#services)
  - [API Services](#api-service)
  - [Front-End Service](#front-end-service)
  - [MongoDB Service](#mongodb-service)
  - [Volumes](#volumes)
- [Installation](#installation)
- [Usage](#usage)

## Services
### API Service

- **Image**: `mvdijk01/phalerum-api:v1.0.0`
- **Container Name**: `phalerum-api`
- **Ports**: `3000:3000`
- **Environment Variables**:
  - `HOST`
  - `PORT`
  - `BASE_URL`
  - `URL`
  - `MAIL_HOST`
  - `MAIL_PORT`
  - `MAIL_FROM`
  - `MONGODB_CONNECTION_STRING`
  - `ENC_KEY`
  - `NODE_ENV`
- **Volumes**: `phalerum-api:/app`

### Front-End Service

- **Image**: `mvdijk01/phalerum-front-end:v1.0.1`
- **Container Name**: `phalerum-front-end`
- **Ports**: `9000:9000`
- **Environment Variables**:
  - `VITE_API_BASE_URL`
  - `VITE_GRAFANA_URL`
  - `VITE_DEFAULT_DASHBOARD_GRAFANA_ID`
- **Volumes**: `phalerum-front-end:/app`

### MongoDB Service

- **Image**: `mongo:latest`
- **Container Name**: `phalerum-mongodb`
- **Ports**: `27017:27017`
- **Environment Variables**:
  - `MONGO_INITDB_ROOT_USERNAME`
  - `MONGO_INITDB_ROOT_PASSWORD`
  - `MONGO_INITDB_DATABASE`
  - `MONGO_USER`
  - `MONGO_USER_PASSWORD`
- **Volumes**:
  - `mongo-data:/data/db`
  - `./init-mongo.js:/docker-entrypoint-initdb.d/init-mongo.js:ro`

## Volumes

- `mongo-data`
- `phalerum-api`
- `phalerum-front-end`

## Installation

1. Clone the repository:
   ```sh
   git clone https://github.com/your-repo/bsf-setup.git
   cd bsf-setup
2. Create a .env file in the root directory and populate it with the necessary environment variables:
   
 - `API_HOST=your_api_host`
 - `API_PORT=your_api_port`
 - `API_BASE_URL=your_api_base_url`
 - `REFERER_URL=your_referer_url`
 - `MAIL_HOST=your_mail_host`
 - `MAIL_PORT=your_mail_port`
 - `MAIL_FROM=your_mail_from`
 - `MONGODB_CONNECTION_STRING=your_mongodb_connection_string`
 - `ENC_KEY=your_enc_key`
 - `NODE_ENV=your_node_env`
 - `VITE_API_BASE_URL=your_vite_api_base_url`
 - `VITE_GRAFANA_URL=your_vite_grafana_url`
 - `VITE_DEFAULT_DASHBOARD_GRAFANA_ID=your_vite_default_dashboard_grafana_id`
 - `MONGO_INITDB_ROOT_USERNAME=your_mongo_root_username`
 - `MONGO_INITDB_ROOT_PASSWORD=your_mongo_root_password`
 - `MONGO_INITDB_DATABASE=your_mongo_database`
 - `MONGO_USER=your_mongo_user`
 - `MONGO_USER_PASSWORD=your_mongo_user_password`

3. Run Docker Compose:
  docker-compose up -d

## Usage
After running docker-compose up -d, the services will be available on the following ports:

API: `http://localhost:3000`
Front-End: `http://localhost:9000`
MongoDB: `mongodb://localhost:27017`

## Grafana Information
We have used an embedded Grafana dashboard inside the front-end application for easy visualisations. To achieve this yourself you can setup Grafana or use an already delopyed Grafana instance and copy the embedded dashboard URL and add it as a environment variable.
