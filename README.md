# catalogue-service

This repository contains Kubernetes manifests for deploying a catalogue application using a Kubernetes Deployment and Service.
Catalogue Deployment and Service
###This repository contains Kubernetes manifests for deploying a catalogue application using a Kubernetes Deployment and Service.

Kubernetes Deployment
###The Kubernetes Deployment defines the catalogue application deployment with the following specifications:

apiVersion: apps/v1
kind: Deployment
metadata:
  name: catalogue-deployment
  labels: 
    app: catalogue-deployment
spec:
  selector:
    matchLabels:```
## Jenkins Pipeline
The Jenkins pipeline automates the following stages:

## Build

Builds the Docker image for the carts service.
Uses Docker commands to build the image with the specified tag.

## Run

Creates a Docker network for the build.
Runs the carts service in a detached mode with the Docker image.
Stops the running service and removes the Docker network.

## Push

Tags the Docker image for the carts service.
Logs in to Docker Hub using provided credentials.
Pushes the Docker image to the Docker Hub repository with both the specified tag and the "latest" tag.

## Deploy EKS

Configures AWS credentials and sets up AWS CLI.
Updates the Kubernetes configuration for Amazon EKS (kubeconfig).
Applies Kubernetes manifests located in the ./manifests directory to the specified namespace.
The AWS credentials, EKS cluster information, and Kubernetes configuration are retrieved from Jenkins credentials.

## Pipeline Environment Variables

The pipeline uses the following environment variables:
DOCKER_ID: Docker Hub username. DOCKER_IMAGE_CARTS: Docker image name for the carts service. DOCKER_TAG: Docker image tag, derived from the Jenkins build ID. BUILD_AGENT: Build agent information (empty for now). NAMESPACE: Kubernetes namespace, retrieved from Jenkins credentials. DOCKER_PASS: Docker Hub password, retrieved from Jenkins credentials. KUBECONFIG: Kubernetes configuration for Amazon EKS, retrieved from Jenkins credentials. AWSKEY, AWSSECRETKEY, AWSREGION, EKSCLUSTERNAME: AWS and EKS configuration details, retrieved from Jenkins credentials.

Configure the Jenkins pipeline with the required credentials and execute the pipeline.
