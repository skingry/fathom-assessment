# Coolkit

This repository contains the and deployment configurations for the Coolkit service. It includes containerization via Docker and a deployment manifests for Kubernetes.

## Table of Contents

- [Overview](#overview)
- [Architecture](#architecture)
- [Containerization](#containerization)
- [Kubernetes Deployment](#kubernetes-deployment)
- [Maintenance](#maintenance)
- [Observability](#observability)
- [License](#license)

## Overview

The Coolkit service is designed to output a simple HTML formatted page with an image. It has been containerized for ease of deployment.

## Architecture

The application follows a microservices architecture, consisting of the following components:

- **Web Server**: \[Does the web stuff\]
- **Readiness Endpoint**: \[Provides an endpoint for Kubernetes to use to determine the readiness of the web service\]
- **Metrics Endpoint**: \[Provides and endpoint to provide theorhetical Prometheus metrics\]

## Containerization

The application is containerized using Docker. The `Dockerfile` located in the `container` directory defines the build instructions.

### Building the Docker Image

To build the Docker image:

```
docker build -t coolkit:latest .
```

### Running the Container Locally

To run the container locally:

```
docker run -p 8080:8080 -p 2345:2345 coolkit:latest
```

## Kubernetes Deployment

Deployment manifests are provided in the `deployment/` directory. These include:

- `deployment.yaml`: Kubernetes Deployment manifest
- `service.yaml`: Kubernetes Service manifest

In addition in the root directory, there is an autoscaling manifest:

- `scaledobject-metrics-api.yaml`: Configures the Horizontal Pod Autoscaler (HPA) via Keda.sh based on the output of a custom metrics api endpoint

### Deploying to Kubernetes

To deploy the application to the Kubernetes cluster via ArgoCD:

```
kubectl apply -f application.yaml
kubectl apply -f scaledobject-metrics-api.yaml
```

### Scaling

The application utilizes HPA via Keda.sh to scale pods based on values from a custom metrics endpoint. Ensure that the metrics server is deployed in the cluster to enable this functionality.

## Maintenance

Regular maintenance tasks include:

- **Updating Dependencies**: Monitor and update application dependencies to patch vulnerabilities and improve performance.
- **Monitoring Resource Usage**: Use Kubernetes dashboards or CLI tools to monitor CPU and memory usage.

