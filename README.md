# DevNet-TIG
This project is made to help you study for the Cisco Certified DevNet Expert certificate. It creates a working TIG (Telegraf, InfluxDB and Grafana) stack so you can get some experience using these tools.

## Features
### Telegraf
Telegraf is a server agent that collects and reports metrics using plugins. It works seamlessly with InfluxDB in this stack.

### InfluxDB
InfluxDB is a powerful time-series database used to store and query large volumes of data, which is commonly required for network monitoring and IoT scenarios.

### Grafana
Grafana provides helpful dashboards for visualization. These dashboards are interactive and user-friendly. In this setup, Grafana is connected to InfluxDB, enabling real-time analytics and monitoring of data.

## Usage
1. Run `docker-compose up`
2. Login to Grafana `http://localhost:3000`
    - Username: expert
    - Password: 1234QWer!
