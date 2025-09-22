# DevOps Engineering – Intensive 3-Month Program

#### Introduction

This comprehensive 3-month DevOps program is designed to equip you with the essential skills to excel in cloud and DevOps roles. The curriculum provides in-depth, hands-on experience with core DevOps practices, including Infrastructure as Code (IaC), CI/CD, containerization, and orchestration. Focusing on a practical, project-based approach, you will master key technologies such as GCP, Docker, Kubernetes, Jenkins, GitHub Actions, and Terraform. The program simulates real-world challenges through industry-grade projects, preparing you to design, build, and manage scalable, resilient, and automated cloud infrastructure.

#### Course Duration: 3 Months

#### Learning Approach:

- **Hands-on Labs:** Practical labs for each technology to reinforce concepts.
- **Industry Practices:** IaC, GitOps, CI/CD automation, and DevSecOps principles.
- **Live Project:** A capstone project implementing a full CI/CD pipeline on GCP.
- **Assessments:** Weekly quizzes and individual assignments to track progres.

---

# DevOps Engineering Syllabus

## Module 1: DevOps Culture, Linux & Source Code Management

### Class 1: Introduction to DevOps & Cloud Fundamentals

- DevOps Culture, Principles (CAMS), and Methodologies
    
- Overview of CI/CD, IaC, and Monitoring
    
- Introduction to Cloud Computing (IaaS, PaaS, SaaS)
    
- Google Cloud Platform (GCP) Core Services Overview (Compute Engine, GCS, VPC)
    
- Hands-on: Setting up a GCP account and using the gcloud CLI
    

### Class 2: Linux Fundamentals for DevOps

- Linux Filesystem Hierarchy and Navigation
    
- Core Commands: File Manipulation, Text Processing (grep, sed, awk)
    
- User and Permission Management (chmod, chown)
    
- Process Management and System Monitoring (ps, top, systemctl)
    
- Hands-on: Managing a Linux VM on GCP Compute Engine
    

### Class 3: Shell Scripting with Bash

- Bash Scripting Basics (Variables, Control Structures, Functions)
    
- Automating System Administration Tasks
    
- Scripting for Environment Setup and Application Deployment
    
- Error Handling and Debugging in Scripts
    
- Practice: Write a script to automate application setup and backup
    

### Class 4: Version Control with Git & GitHub

- Git Fundamentals (init, add, commit, push, pull)
    
- Branching and Merging Strategies (Git Flow, GitHub Flow)
    
- Resolving Merge Conflicts
    
- Collaborating on GitHub (Pull Requests, Code Reviews)
    
- Hands-on: Managing a collaborative project using Git and GitHub
    

### Class 5: Networking Fundamentals

- Core Concepts: TCP/IP, DNS, HTTP/HTTPS, Firewalls
    
- Virtual Private Cloud (VPC) in GCP
    
- Subnets, Firewall Rules, and Cloud DNS
    
- Load Balancing and Cloud NAT
    
- Hands-on: Designing and implementing a custom VPC network in GCP
    

---

## Module 2: Containerization with Docker

### Class 1: Introduction to Containers & Docker

- Containers vs. Virtual Machines
    
- Docker Architecture (Engine, Client, Registry)
    
- Core Docker Commands (run, ps, images, rm, rmi)
    
- Managing Docker Containers and Images
    
- Hands-on: Running and managing your first Docker containers
    

### Class 2: Building Docker Images with Dockerfile

- Dockerfile Instructions (FROM, RUN, COPY, CMD, ENTRYPOINT)
    
- Best Practices for Writing Dockerfiles (Multi-stage builds, layer caching)
    
- Building and Tagging Images for Different Environments
    
- Hands-on: Containerizing a simple Java/Node.js application
    

### Class 3: Docker Networking & Storage

- Docker Networking Models (Bridge, Host, Overlay)
    
- Managing Persistent Data with Docker Volumes
    
- Bind Mounts vs. Volumes
    
- Hands-on: Setting up communication between containers and persisting data
    

### Class 4: Docker Compose for Multi-Container Applications

- Introduction to Docker Compose
    
- Writing `docker-compose.yml` files
    
- Orchestrating a multi-service application (e.g., web app with a database)
    
- Managing the application lifecycle with `docker-compose up`, `down`, `logs`
    
- Hands-on: Deploying a full-stack application using Docker Compose
    

### Class 5: Container Registries & Security

- Pushing and Pulling Images from Docker Hub
    
- Google Artifact Registry for private container images
    
- Scanning images for vulnerabilities
    
- Best Practices for Securing Docker environments
    
- Hands-on: Setting up Artifact Registry and managing private images
    

---

## Module 3: Container Orchestration with Kubernetes on GKE

### Class 1: Introduction to Kubernetes & GKE

- Kubernetes Architecture (Control Plane, Worker Nodes)
    
- Introduction to Google Kubernetes Engine (GKE)
    
- `kubectl`: The Kubernetes CLI
    
- Deploying your first application on a GKE cluster
    
- Hands-on: Creating a GKE cluster and deploying a simple service
    

### Class 2: Kubernetes Core Concepts: Pods, Deployments & Services

- Understanding Pods: The smallest deployable units
    
- Managing Application Lifecycle with Deployments (Scaling, Rolling Updates)
    
- Exposing Applications with Services (ClusterIP, NodePort, LoadBalancer)
    
- Hands-on: Deploying, scaling, and updating a stateless application
    

### Class 3: Configuration & Secrets Management

- Managing application configuration with ConfigMaps
    
- Handling sensitive data with Secrets
    
- Injecting configuration and secrets into Pods (environment variables, volumes)
    
- Hands-on: Externalizing configuration for a microservice
    

### Class 4: Storage and Stateful Applications

- Persistent Storage in Kubernetes (PersistentVolumes, PersistentVolumeClaims)
    
- Understanding StorageClasses in GKE
    
- Deploying stateful applications (e.g., databases) with StatefulSets
    
- Hands-on: Deploying a PostgreSQL database on GKE with persistent storage
    

### Class 5: Ingress & Helm for Application Management

- Managing external access to services with Ingress
    
- Using Helm as a package manager for Kubernetes
    
- Finding and deploying applications using Helm charts
    
- Creating your own Helm chart
    
- Hands-on: Exposing multiple services via a single IP using Ingress and deploying a complex app with Helm
    

---

## Module 4: CI/CD Pipelines with Jenkins & GitHub Actions

### Class 1: CI/CD Principles & Jenkins Introduction

- Core Concepts of Continuous Integration & Continuous Delivery/Deployment
    
- Jenkins Architecture (Controller, Agents)
    
- Setting up and configuring a Jenkins server on GCP
    
- Creating your first Freestyle Jenkins job
    
- Hands-on: Building and testing a Java application with Jenkins
    

### Class 2: Building Pipelines with Jenkinsfile

- Introduction to Pipeline as Code
    
- Declarative vs. Scripted Pipeline syntax
    
- Building a CI pipeline: Checkout, Build, Test, and Package
    
- Using Shared Libraries to manage reusable code
    
- Hands-on: Creating a `Jenkinsfile` to automate the CI process for a project
    

### Class 3: Continuous Deployment with Jenkins

- Integrating Jenkins with Docker and Kubernetes
    
- Building Docker images within a Jenkins pipeline
    
- Deploying applications to GKE from Jenkins
    
- Managing credentials and secrets securely in Jenkins
    
- Hands-on: Creating a full CI/CD pipeline that deploys a containerized app to GKE
    

### Class 4: Introduction to GitHub Actions

- Core Concepts: Workflows, Events, Jobs, Steps, Actions
    
- Building a CI workflow with GitHub Actions
    
- Using pre-built Actions from the Marketplace
    
- Managing secrets and environments
    
- Hands-on: Creating a GitHub Actions workflow to build and test an application
    

### Class 5: Continuous Deployment with GitHub Actions

- Authenticating GitHub Actions with GCP
    
- Building and pushing Docker images to Google Artifact Registry
    
- Deploying to GKE using GitHub Actions
    
- Comparing Jenkins and GitHub Actions: Use cases and trade-offs
    
- Hands-on: Building a complete CD pipeline using GitHub Actions to deploy to GKE
    

---

## Module 5: Infrastructure as Code (IaC) & Monitoring

### Class 1: Infrastructure as Code with Terraform

- Introduction to IaC and its benefits
    
- Terraform Core Concepts (Providers, Resources, State, Variables)
    
- Writing your first Terraform configuration to manage GCP resources
    
- Hands-on: Provisioning a VPC and a Compute Engine instance with Terraform
    

### Class 2: Managing Complex Infrastructure with Terraform

- Terraform Modules for reusability
    
- Managing environments with Workspaces
    
- Remote State Management with Google Cloud Storage
    
- Hands-on: Creating a reusable Terraform module to deploy a GKE cluster
    

### Class 3: Monitoring & Logging with Google Cloud's Operations Suite

- Introduction to Monitoring, Logging, and Alerting
    
- Cloud Monitoring: Metrics, Dashboards, and Uptime Checks
    
- Cloud Logging: Collecting and analyzing logs from GKE and other services
    
- Setting up alerting policies for critical services
    
- Hands-on: Creating a monitoring dashboard and an alert for a GKE application
    

### Class 4: Open-Source Monitoring with Prometheus & Grafana

- Introduction to Prometheus architecture (Scraping, Time-Series Database)
    
- Instrumenting applications for Prometheus metrics
    
- Visualizing metrics with Grafana dashboards
    
- Hands-on: Deploying Prometheus and Grafana on GKE to monitor a microservice
    

### Class 5: DevSecOps & Security Best Practices

- Introduction to DevSecOps: Shifting security left
    
- Automated Security Testing in CI/CD (SAST, DAST, SCA)
    
- Securing Docker images and Kubernetes clusters
    
- Identity and Access Management (IAM) best practices in GCP
    
- Workshop: Integrating security scanning into a CI/CD pipeline
    

---
## Module 6: Performance Testing & Optimization

### Class 1: Fundamentals of Performance Testing

- **Concepts:** Introduction to performance, load, stress, spike, and soak testing.
    
- **Metrics:** Defining key performance indicators (KPIs) like latency, throughput, error rate, and resource utilization.
    
- **Methodology:** Understanding the performance testing lifecycle in a DevOps environment.
    
- **Hands-on:** Analyzing performance requirements for a sample application and defining test objectives.
    

### Class 2: Load Testing with Apache JMeter

- **Introduction:** Setting up JMeter and understanding its core elements (Thread Group, Samplers, Listeners).
    
- **Test Plan Creation:** Building a test plan to simulate user load on a web application's APIs.
    
- **Execution & Analysis:** Running tests and interpreting results using JMeter's built-in reporting tools.
    
- **Practice:** Create and run a basic load test against a sample API.
    

### Class 3: Modern Load Testing with k6/Locust

- **Introduction:** Overview of k6 and its benefits (developer-friendly, scriptable in JavaScript).
    
- **Scripting Tests:** Writing k6 scripts to define virtual users, scenarios, and thresholds.
    
- **Cloud Execution:** Running distributed load tests using k6 Cloud.
    
- **Hands-on:** Write a k6 script to test the performance of a microservice and analyze the results.
    

### Class 4: Integrating Performance Tests into CI/CD

- **Automation:** Triggering performance tests automatically in a Jenkins or GitHub Actions pipeline.
    
- **Quality Gates:** Defining pass/fail criteria (performance budgets) to prevent performance regressions.
    
- **Trend Analysis:** Storing and visualizing performance test results over time to track trends.
    
- **Hands-on:** Add a k6 performance test stage to your existing CI/CD pipeline that fails the build if performance degrades.
    

### Class 5: Performance Monitoring & Bottleneck Analysis

- **Correlation:** Analyzing application and infrastructure metrics (CPU, memory, DB queries) during a load test.
    
- **Tooling:** Using Prometheus and Grafana to monitor system behavior under load.
    
- **Profiling:** Introduction to application profiling techniques to identify code-level bottlenecks.
    
- **Workshop:** Run a load test while monitoring a live Grafana dashboard to identify and diagnose a performance issue.

---
## Assignments

### Assignment 1: Containerize a Full-Stack Application

- **Context:** Take an existing two-tier web application (e.g., React frontend, Spring Boot backend, PostgreSQL database).
    
- **Requirements:**
    
    - Write Dockerfiles for the frontend and backend services.
        
    - Create a `docker-compose.yml` file to orchestrate all three services.
        
    - Ensure the application is fully functional when launched with `docker-compose`.
        
    - Push the custom images to Google Artifact Registry.
        

### Assignment 2: Deploy Microservices on GKE with Terraform

- **Context:** Manage the deployment of a microservices application on GKE.
    
- **Requirements:**
    
    - Write Terraform code to provision a GKE cluster, a VPC, and a Cloud SQL database.
        
    - Write Kubernetes manifest files (Deployments, Services, ConfigMaps, Secrets, PV/PVC) for each microservice.
        
    - Deploy the application to the GKE cluster using `kubectl`.
        
    - Expose the application to the internet using an Ingress controller.
        

### Assignment 3: Build a Complete CI/CD Pipeline

- **Context:** Automate the entire lifecycle of a microservice from code commit to deployment.
    
- **Requirements:**
    
    - Choose either Jenkins or GitHub Actions.
        
    - Create a pipeline that triggers on a push to the `main` branch.
        
    - The pipeline must:
        
        1. Run unit and integration tests.
            
        2. Build a Docker image and push it to Artifact Registry.
            
        3. Deploy the new image to your GKE cluster with zero downtime (rolling update).
            
        4. Send a notification upon successful deployment.
            

---

## Live Project: CI/CD Automation for a Cloud-Native Application

### Tech Stack

- **Cloud:** Google Cloud Platform (GKE, Artifact Registry, Cloud SQL, Cloud Storage)
- **IaC:** Terraform
- **Containerization:** Docker, Docker Compose
- **Orchestration:** Kubernetes, Helm
- **CI/CD:** Jenkins or GitHub Actions
- **Monitoring:** Google Cloud's Operations Suite, Prometheus, Grafana

### Project Overview

Design and implement a robust, automated CI/CD pipeline for a multi-service, cloud-native application. The goal is to enable developers to deploy new features to production safely, quickly, and reliably with minimal manual intervention.

#### Pipeline Components & Features

1. **Infrastructure Provisioning:**
    
    - Use Terraform to define and provision all necessary GCP infrastructure (VPC, GKE Cluster, Cloud SQL, Artifact Registry).
        
    - Manage Terraform state remotely and securely.
        
2. **Continuous Integration (CI):**
    
    - The pipeline automatically triggers on every code commit.
        
    - Compile code, run unit tests, and perform static code analysis.
        
    - Build versioned Docker images for each microservice.
        
    - Push images to a private Google Artifact Registry.
        
3. **Continuous Deployment (CD):**
    
    - Implement GitOps principles for deployment.
        
    - Automatically deploy changes to a **staging** environment for verification.
        
    - Require manual approval to promote a release to the **production** environment.
        
    - Use Kubernetes rolling updates to ensure zero-downtime deployments.
        
4. **Monitoring and Alerting:**
    
    - Configure Google Cloud Monitoring to collect metrics from the GKE cluster.
        
    - Set up alerts for key indicators like high CPU/memory usage, high error rates, or service downtime.
        
    - Create a Grafana dashboard to visualize application and cluster health.
        

---

### Evaluation Criteria

1. **Architecture & Design (40%)**
    
    - Scalability and resilience of the infrastructure design.
        
    - Efficiency and reliability of the CI/CD pipeline architecture.
        
    - Clear separation of environments (staging, production).
        
2. **Technical Implementation (40%)**
    
    - Correct and effective use of Terraform, Docker, and Kubernetes.
        
    - Functionality and completeness of the CI/CD pipeline.
        
    - Implementation of monitoring and alerting.
        
3. **Automation & Best Practices (20%)**
    
    - Adherence to IaC and Pipeline-as-Code principles.
        
    - Implementation of security best practices (e.g., least privilege IAM).
        
    - Quality of documentation (README, code comments).