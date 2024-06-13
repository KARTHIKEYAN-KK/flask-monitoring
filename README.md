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

## Prometheus Configuration

1. Download and install Prometheus from the [official website](https://prometheus.io/download/).

2. Create a configuration file `prometheus.yml` with the following content:

    ```yaml
    global:
      scrape_interval: 15s

    scrape_configs:
      - job_name: 'flask'
        static_configs:
          - targets: ['127.0.0.1:5000']
    ```

3. Start Prometheus with the configuration file:

    ```bash
    prometheus --config.file=prometheus.yml
    ```

## Grafana Integration

1. Download and install Grafana from the [official website](https://grafana.com/grafana/download).

2. Start Grafana:

    ```bash
    grafana-server
    ```

3. Open Grafana in your browser at `http://localhost:3000/`.

4. Add Prometheus as a data source:
    - Go to Configuration > Data Sources > Add data source
    - Select Prometheus
    - Set the URL to `http://localhost:9090`
    - Click Save & Test

5. Import a dashboard to visualize Flask metrics:
    - Go to Create > Import
    - Enter the dashboard ID from the [Grafana dashboards library](https://grafana.com/grafana/dashboards) (e.g., 1860 for a general Node Exporter Full dashboard)
    - Click Load
    - Select Prometheus as the data source and click Import

## Contributing

Contributions are welcome! Please open an issue or submit a pull request for any improvements or bug fixes.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
