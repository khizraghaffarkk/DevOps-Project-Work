# Task 1: Sending Formula 1 Car Data to Cloud with Eclipse Kuksa

## Overview
This project involves sending data from the `f1demo2val` application to the Kuksa Server, and subsequently from the server to the `val2mqtt` application. The `val2mqtt` application publishes the received data as MQTT messages to the Mosquitto broker.

## Architecture
The system consists of the following components:
- **f1demo2val**: Application that sends Formula 1 car data to the Kuksa Server.
- **Kuksa Server**: Acts as the intermediary that receives data from `f1demo2val`.
- **val2mqtt**: Application that retrieves data from the Kuksa Server and publishes it to the Mosquitto broker.

## Getting Started

### Prerequisites
- Docker
- Docker Compose
- Mosquitto MQTT broker

### Building Docker Images

1. Build the Docker image for `f1demo2val`:
   ```bash
   docker build -t docker-registry.rahti.csc.fi/finalprojecttask1/f1demo2val:1.0 -f Dockerfile .
   ```
2. Push the image to the CSC Rahti account:
   ```bash
   docker push docker-registry.rahti.csc.fi/finalprojecttask1/f1demo2val:1.0
   ```
3. Build the Docker image for val2mqtt:
   ```bash
   docker build -t docker-registry.rahti.csc.fi/finalprojecttask1/val2mqtt:1.0 -f Dockerfile .
   ```
4. Push the image to the CSC Rahti account:
   ```bash
   docker push docker-registry.rahti.csc.fi/finalprojecttask1/val2mqtt:1.0
    ```
## Running the Applications
Use the provided docker-compose.yml file to start the services:
```bash
docker-compose up
```
## Checking Messages on Kuksa Server
You can check the messages received on the Kuksa Server by running the command:
```bash
mosquitto_sub -t "khghaffa23/#" --cafile ca.crt --insecure --host mqtt.khghaffa23.rahtiapp.fi --port 443 -v
```















mosquitto_sub -h mqtt.khghaffa23.rahtiapp.fi -p 443 --cafile ca.crt -t "khghaffa23/#"

mosquitto_sub -h mqtt.khghaffa23.rahtiapp.fi -p 443 --cafile D:\check\test\pwtask1\val2mqtt\ca.crt -t "khghaffa23/#"
