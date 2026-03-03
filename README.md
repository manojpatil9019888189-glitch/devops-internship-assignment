Lemici DevOps Internship Assignment

Task 1 – Repository Setup Using SSH

The repository was created on GitHub and configured using SSH authentication.

SSH keys were generated locally using ssh-keygen.

The public key was added to GitHub under SSH & GPG Keys.

The repository was cloned using the SSH URL.

Git operations (clone, pull, push) work without username/password, confirming successful SSH configuration.

Task 2 – Difference Between git fetch and git pull
git fetch

Downloads new data (commits, branches, files) from the remote repository.

Does NOT modify the current working branch.

Updates only the remote tracking branch (e.g., origin/main).

Provides more control because changes can be reviewed before merging.

Does not cause merge conflicts directly.

Used when you want to safely inspect changes before integrating them.

git pull

Downloads changes AND immediately merges them into the current branch.

Automatically updates the local branch.

Provides less control since integration happens immediately.

Can cause merge conflicts if local and remote changes differ.

Used when you want to quickly synchronize your branch.

Task 3 – How to Resolve a Git Merge Conflict (Example Scenario)

A merge conflict occurs when two branches modify the same line in a file differently.

Example:

Two feature branches modify the same configuration value.

The first branch merges successfully.

When merging the second branch, Git cannot automatically decide which change to keep.

Git pauses the merge and marks the conflict using conflict markers.

To resolve:

Open the conflicted file.

Review the conflicting sections.

Decide which changes to keep (or combine them).

Remove conflict markers.

Stage and commit the resolved file.

Task 4 – Practical Demonstration of Merge Conflict

A merge conflict was intentionally simulated.

A configuration file (config.yaml) was created in the main branch.

Two branches (feature-A and feature-B) were created.

In feature-A, a value such as log_level was changed to debug.

In feature-B, the same value was changed to error.

After merging feature-A, merging feature-B caused a conflict because the same line was modified differently.

The file was manually reviewed, conflict markers were removed, and a final meaningful value was selected.
The resolved file was staged and committed with the message:

"Resolved merge conflict in config.yaml"

This demonstrated practical conflict resolution using Git.

Part 2: Docker & Containerization
Task 1 – Dummy Python Web Application

A simple Flask-based Python web application was created.

The application:

Exposes / endpoint returning:

"DevOps Internship Assignment Working!"

Runs on port 5000.

Binds to 0.0.0.0 to allow external access from the container.

Dockerfile

The application was containerized using a Dockerfile.

Key points:

Base image: python:3.9-slim

Working directory: /app

Application files copied into container

Flask installed using pip

Port 5000 exposed

Application started using:

python app.py
Task 2 – Difference Between Dockerfile, Image, and Container

Dockerfile: A text file containing instructions to build a Docker image.

Docker Image: A packaged, read-only template created from a Dockerfile.

Docker Container: A running instance of a Docker image.

Reducing Docker Image Size

To optimize image size:

Used python:3.9-slim base image.

Installed only required dependencies.

Avoided unnecessary files.

Used layer caching efficiently.

Task 3 – Running the Application Locally

Steps performed:

Built Docker image:

docker build -t devops-app .

Ran container:

docker run -p 5000:5000 devops-app

Verified in browser:

http://localhost:5000

The application successfully displayed the expected message.

Part 3: Kubernetes (EKS Basics)
Task 1 – Difference Between Pod, Deployment, and Service
Pod

Smallest deployable unit in Kubernetes.

Encapsulates one or more containers.

Represents a single instance of an application.

Deployment

Manages ReplicaSets and Pods.

Ensures desired number of replicas.

Supports rolling updates and rollbacks.

Service

Exposes a group of Pods.

Provides stable IP and DNS.

Load balances traffic.

Why Use EKS Instead of Self-Managed Kubernetes?

Amazon EKS removes the operational overhead of managing the control plane.

AWS manages:

API server

etcd

High availability

Upgrades and patches

This allows teams to focus on deploying and scaling applications rather than managing infrastructure.

Task 2 – Kubernetes YAML Files

Two separate YAML files were created:

deployment.yaml

service.yaml

Deployment:

2 replicas

Container image: devops-app

Port 5000 exposed

Service:

Type: LoadBalancer

Maps port 80 → 5000

These YAML files are provided as configuration and were not deployed to a live cluster as per assignment requirements.

Part 4: CI/CD Pipeline

A GitHub Actions workflow was implemented in:

.github/workflows/config.yaml
Pipeline triggers:

On every push to the main branch.

Pipeline steps:

Checkout source code

Build Docker image

Run basic test (simulated)

Simulate Docker image push

The GitHub Actions pipeline executed successfully and showed a green status.

Deploying to Kubernetes (Extension)

To extend this pipeline for Kubernetes deployment:

Authenticate with EKS cluster

Push Docker image to DockerHub or ECR

Run:

kubectl apply -f deployment.yaml
kubectl apply -f service.yaml

Verify rollout status

Part 5: Monitoring & Logs
Task 1 – Metrics vs Logs vs Traces
Metrics

Numerical values over time.
Examples:

CPU usage

Memory usage

Request rate

Used for performance monitoring and alerting.

Logs

Detailed event records.
Examples:

Error messages

Application startup logs

Used for debugging and issue investigation.

Traces

Track request flow across services.
Useful in microservices architecture to measure latency and bottlenecks.

Task 2 – Debugging a Crashing Kubernetes Pod

Steps:

Check pod status:

kubectl get pods

Describe pod:

kubectl describe pod <pod-name>

Check logs:

kubectl logs <pod-name>

Check resource usage:

kubectl top pod

Exec into container (if running):

kubectl exec -it <pod-name> -- /bin/sh
Task 3 – Monitoring Tools for AWS EKS

Recommended tools:

Prometheus – Metrics collection

Grafana – Dashboard visualization

AWS CloudWatch – Native logging and monitoring

ELK Stack – Centralized logging

These tools together provide full visibility into cluster health and application performance.

Part 6: Problem Solving Scenario

To set up a new microservice in AWS EKS:

1. Source Code Management

Code hosted on GitHub.

Feature branches used.

Main branch protected.

2. Containerization

Create Dockerfile.

Build and test locally.

Push image to DockerHub or ECR.

3. CI/CD Automation

Pipeline configured to:

Build image

Run tests

Push image

Deploy to EKS

4. Deployment to EKS

Use deployment.yaml and service.yaml

Ensure rolling updates for zero downtime

5. Logging & Monitoring

Logs written to stdout/stderr

Collected via CloudWatch or ELK

Metrics monitored via Prometheus & Grafana

This ensures automated deployments, scalability, reliability, and visibility.
