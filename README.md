E-Commerce DevOps Project
Project Overview

This project demonstrates an end-to-end CI/CD pipeline implementation using Jenkins, Docker, and Kubernetes for deploying a React frontend and Node.js backend application.

The objective of this project is to automate application build, containerization, image push, and deployment processes using DevOps tools and practices.

Architecture
Developer → GitHub → Jenkins Pipeline → Docker Build → Docker Hub → Kubernetes Deployment

Tech Stack

Frontend: React.js

Backend: Node.js + Express

CI/CD Tool: Jenkins

Containerization: Docker

Orchestration: Kubernetes

Version Control: Git & GitHub

Container Registry: Docker Hub

OS: Ubuntu Linux

Project Structure

<img width="326" height="365" alt="Screenshot 2026-05-14 155340" src="https://github.com/user-attachments/assets/fc88c68b-ed2d-41de-b546-f8942e0d4022" />


Frontend Setup

Create React App

npx create-react-app frontend

Run Frontend

cd frontend

npm start


Frontend runs on:

http://localhost:3000

Frontend Dockerfile

FROM node:18

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm","start"]

Backend Setup

Create Backend Directory

mkdir backend

cd backend

Initialize Node Project

npm init -y

Install Express

npm install express

Create server.js

const express = require("express");

const app = express();

app.get("/", (req, res) => {
  res.send("Backend Running Successfully");
});

app.listen(5000, () => {
  console.log("Server running on port 5000");
});
Backend Dockerfile
FROM node:18

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 5000

CMD ["node","server.js"]

Docker Commands

Build Frontend Image

docker build -t ecommerce-frontend ./frontend

Run Frontend Container

docker run -d -p 3000:3000 ecommerce-frontend

Build Backend Image

docker build -t ecommerce-backend ./backend

Run Backend Container

docker run -d -p 5000:5000 ecommerce-backend

Push Images to Docker Hub

Login

docker login

Tag Images

docker tag ecommerce-frontend vaibhavsurase/frontend:v1


docker tag ecommerce-backend vaibhavsurase/backend:v1

Push Images

docker push vaibhavsurase/frontend:v1


docker push vaibhavsurase/backend:v1

Kubernetes Setup

Check Nodes

kubectl get nodes

Kubernetes Deployment Files

frontend-deployment.yaml

apiVersion: apps/v1

kind: Deployment

metadata:
  name: frontend-deployment

spec:
  replicas: 2

  selector:
    matchLabels:
      app: frontend

  template:
    metadata:
      labels:
        app: frontend

    spec:
      containers:
      - name: frontend
        image: vaibhavsurase/frontend:v1

        ports:
        - containerPort: 3000

frontend-service.yaml

apiVersion: v1
kind: Service

metadata:
  name: frontend-service

spec:
  type: NodePort

  selector:
    app: frontend

  ports:
  - port: 3000
    targetPort: 3000

backend-deployment.yaml

apiVersion: apps/v1

kind: Deployment

metadata:
  name: backend-deployment

spec:
  replicas: 2

  selector:
    matchLabels:
      app: backend

  template:
    metadata:
      labels:
        app: backend

    spec:
      containers:
      - name: backend
        image: vaibhavsurase/backend:v1

        ports:
        - containerPort: 5000

backend-service.yaml

apiVersion: v1
kind: Service

metadata:
  name: backend-service

spec:
  type: NodePort

  selector:
    app: backend

  ports:
  - port: 5000
    targetPort: 5000

Deploy Application to Kubernetes

Apply Kubernetes Files

kubectl apply -f k8s/

Verify Deployments

kubectl get deployments

Verify Pods

kubectl get pods

Verify Services

kubectl get svc

Jenkins Setup

Install Java

sudo apt update

sudo apt install openjdk-17-jdk -y

Install Jenkins

sudo apt install jenkins -y

Start Jenkins

sudo systemctl start jenkins


sudo systemctl enable jenkins

Check Jenkins Status

systemctl status jenkins

Jenkins Initial Password

sudo cat /var/lib/jenkins/secrets/initialAdminPassword

Access Jenkins:

http://localhost:8080

Jenkins Plugins

Install following plugins:

Docker Pipeline

Kubernetes

Git

NodeJS

Jenkins Pipeline

Jenkinsfile

pipeline {
    agent any

    stages {

        stage('Clone Code') {
            steps {
                git 'https://github.com/vaibhav-surase/ecommerce-devops-project.git'
            }
        }

        stage('Build Frontend Image') {
            steps {
                sh 'docker build -t vaibhavsurase/frontend:v1 frontend/'
            }
        }

        stage('Build Backend Image') {
            steps {
                sh 'docker build -t vaibhavsiurase/backend:v1 backend/'
            }
        }

        stage('Push Images') {
            steps {
                sh 'docker push vaibhavsurase/frontend:v1'
                sh 'docker push vaibhavsurase/backend:v1'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s/'
            }
        }
    }
}

GitHub Commands

Initialize Git

git init

Add Files

git add .

Commit Changes

git commit -m "Initial Commit"

Add Remote Repository

git remote add origin https://github.com/vaibhav-surase/ecommerce-devops-project.git

Push Code

git push -u origin main

Troubleshooting

Docker Logs

docker logs <container-id>

Kubernetes Logs

kubectl logs <pod-name>

Describe Pod

kubectl describe pod <pod-name>

Jenkins Logs

journalctl -u jenkins

Key Achievements

Automated CI/CD pipeline using Jenkins

Reduced manual deployment effort

Containerized frontend and backend applications

Implemented Kubernetes deployments and services

Improved deployment consistency and scalability

Performed troubleshooting using Docker and Kubernetes logs

Future Enhancements

Add Helm Charts

Implement Monitoring using Prometheus & Grafana

Add SonarQube for Code Quality

Configure Ingress Controller

Integrate ArgoCD for GitOps Deployment


Author

Vaibhav Surase

DevOps Engineer

CI/CD | Docker | Kubernetes | Jenkins | Linux | AWS
