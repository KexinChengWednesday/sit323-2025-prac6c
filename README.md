Task6.2c - Kubernetes Deployment and Service
Overview
This project demonstrates how to containerize a simple Node.js application with Docker, push the image to Docker Hub, and deploy it on a Kubernetes cluster using a Deployment and Service. The application is accessible via a forwarded local port.

Requirements:

Docker

Node.js & npm

Kubernetes (Minikube or Docker Desktop)

kubectl CLI

Docker Hub account

Project Structure: task6.1p/
├── app/ (Node.js application)
│ ├── Dockerfile (Docker build instructions)
│ ├── server.js (Main app file)
│ └── package.json (Dependencies)
├── kubernetes/
│ ├── deployment.yaml (Kubernetes Deployment)
│ └── service.yaml (Kubernetes Service)
└── README.md (Documentation)

Steps to Run:

Create the Repository:

cd sit323-2025-prac6c

Build and Push Docker Image:


docker build -t task6-app:v1 .
docker tag task6-app:v1 kexincheng/task6-app:v1
docker login
docker push kexincheng/task6-app:v1

Deploy to Kubernetes:


kubectl apply -f kubernetes/deployment.yaml
kubectl apply -f kubernetes/service.yaml

Verify:


kubectl get pods
kubectl get services

Access the App: If EXTERNAL-IP is pending, use port-forward:

kubectl port-forward service/task6-app-service 8888:80

Then visit:
http://localhost:8888

Notes:

Dockerfile builds the Node.js app

deployment.yaml creates a deployment with replicas

service.yaml exposes the app
