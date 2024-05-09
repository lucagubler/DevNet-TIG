# DevNet-TIG
This project is made to help you study for the Cisco Certified DevNet Expert certificate. It creates a working TIG (Telegraf, InfluxDB and Grafana) stack so you can get some experience using these tools. You can also create certificates to grpc-tls subscriptions.

I built this TIG stack to go along with my [DevNet Expert E-Learning](https://devnet-academy.com). There you will learn everything to become a Cisco Certified DevNet Expert.


## Features
### Telegraf
Telegraf is a server agent that collects and reports metrics using plugins. It works seamlessly with InfluxDB in this stack.

### InfluxDB
InfluxDB is a powerful time-series database used to store and query large volumes of data, which is commonly required for network monitoring and IoT scenarios.

### Grafana
Grafana provides helpful dashboards for visualization. These dashboards are interactive and user-friendly. In this setup, Grafana is connected to InfluxDB, enabling real-time analytics and monitoring of data.

## TLS Certificates
Follow these steps to create TLS certificates
```sh
# Make sure that you create certificates inside the telegraf/ directory
cd telegraf

# Edit csr.conf and add the FQDN and IP of the server where TIG is running

# Create the CA key
openssl genrsa -out ca.key 2048

# Create the telegraf key
openssl genrsa -out telegraf.key 2048

# Create the CA certificate
openssl req -x509 -new -key ca.key -sha256 -days 3650 -out ca.crt -nodes

# Create the telegraf CSR
openssl req -out telegraf.csr -key telegraf.key -new -config csr.conf

# Sign the telegraf certificate with the CA
openssl x509 -req -in telegraf.csr -CA ca.crt -CAkey ca.key -CAcreateserial -out telegraf.crt -days 3650 -extensions v3_req -extfile csr.conf

# Make sure that the telegraf key has correct permissions
chmod 644 telegraf.key
```

Follow these steps to configure a trustpoint on IOS-XE
```
conf t
crypto pki trustpoint devnetacademy
  enrollment terminal
  chain-validation stop
  revocation-check none
  exit
crypto pki certificate devnetacademy
  ! Paste content of ca.crt
```

Edit `docker-compose.yml` to add the telegraf certificates and to listen on port 57100 (just uncomment the lines).

Edit `telegraf/telegraf.conf` to listen on port 57100 and configure TLS certificates (just uncomment the lines).

## Usage
1. Run `docker-compose up`
2. Login to Grafana `http://localhost:3000`
    - Username: expert
    - Password: 1234QWer!
