# Flask Monitoring

This repository contains a basic setup for monitoring a Flask application using Prometheus. The goal is to provide a starting point for integrating Prometheus with Flask to collect and visualize metrics.

## Table of Contents

- [Introduction](#introduction)
- [Features](#features)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [Prometheus Configuration](#prometheus-configuration)
- [Grafana Integration](#grafana-integration)
- [Contributing](#contributing)
- [License](#license)

## Introduction

Monitoring is an essential aspect of maintaining and scaling web applications. This project demonstrates how to set up basic monitoring for a Flask application using Prometheus, an open-source monitoring and alerting toolkit.

## Features

- Basic Flask application setup
- Integration with Prometheus for monitoring
- Pre-configured metrics endpoint for Prometheus scraping
- Instructions for setting up Prometheus and Grafana for visualization

## Prerequisites

Before you begin, ensure you have the following installed on your local machine:

- Python 3.6 or higher
- pip (Python package installer)
- Docker (optional, for running Prometheus and Grafana in containers)

## Installation

1. Clone the repository:

    ```bash
    git clone https://github.com/KARTHIKEYAN-KK/flask-monitoring.git
    cd flask-monitoring
    ```

2. Create a virtual environment and activate it:

    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows use `venv\Scripts\activate`
    ```

3. Install the required dependencies:

    ```bash
    pip install -r requirements.txt
    ```

## Usage

1. Start the Flask application:

    ```bash
    flask run
    ```

2. The application will be available at `http://127.0.0.1:5000/`.

3. The Prometheus metrics endpoint will be available at `http://127.0.0.1:5000/metrics`.

## Prometheus and Grafana Setup

1. Create a Prometheus configuration file `prometheus.yml` with the following content:

    ```yaml
    global:
      scrape_interval: 15s

    scrape_configs:
      - job_name: 'flask'
        static_configs:
          - targets: ['host.docker.internal:5000']
    ```

2. Create a `docker-compose.yml` file to set up Prometheus and Grafana using Docker:

    ```yaml
    version: '3.7'
    services:
      prometheus:
        image: prom/prometheus
        volumes:
          - ./prometheus.yml:/etc/prometheus/prometheus.yml
        ports:
          - "9090:9090"

      grafana:
        image: grafana/grafana-oss
        ports:
          - "3000:3000"
    ```

3. Start Prometheus and Grafana using Docker Compose:

    ```bash
    docker-compose up -d
    ```

4. Prometheus will be available at `http://localhost:9090/`.

5. Grafana will be available at `http://localhost:3000/`.

6. Add Prometheus as a data source in Grafana:
    - Open Grafana in your browser and log in (default credentials: admin/admin).
    - Go to Configuration > Data Sources > Add data source.
    - Select Prometheus.
    - Set the URL to `http://prometheus:9090`.
    - Click Save & Test.

7. Import a dashboard to visualize Flask metrics:
    - Go to Create > Import.
    - Enter the dashboard ID from the [Grafana dashboards library](https://grafana.com/grafana/dashboards) (e.g., 1860 for a general Node Exporter Full dashboard).
    - Click Load.
    - Select Prometheus as the data source and click Import.

## Contributing

Contributions are welcome! Please open an issue or submit a pull request for any improvements or bug fixes.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
