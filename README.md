# Three-Tier Voting Application – CI/CD with Jenkins & Kubernetes

This project demonstrates an end-to-end DevOps workflow using a microservices-based voting application. The application consists of multiple services including Vote, Worker, Result, Redis, and PostgreSQL, containerized with Docker and deployed on Kubernetes.

## Tech Stack

* Jenkins (Pipeline as Code)
* Docker
* Docker Hub
* Kubernetes (Docker Desktop)
* Git & GitHub
* Redis
* PostgreSQL

## CI/CD Pipeline Features

* Source code management using Git and GitHub
* Jenkins Pipeline as Code (Jenkinsfile)
* Automated Docker image builds
* Image versioning using Jenkins build numbers
* Automatic publishing to Docker Hub
* Kubernetes cluster validation
* Automated Kubernetes deployments
* Deployment rollout verification
* Continuous delivery of application updates

## Pipeline Flow

GitHub → Jenkins → Docker Build → Docker Hub → Kubernetes Deployment → Rollout Verification

## Learning Outcomes

This project was built to gain hands-on experience with modern DevOps practices including containerization, CI/CD automation, container registries, Kubernetes deployments, and Git-based development workflows.
