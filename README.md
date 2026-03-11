Production Kubernetes GitOps Platform on AWS

This project demonstrates how to build a production-style Kubernetes platform using Terraform, EKS, ArgoCD GitOps, and Prometheus/Grafana observability.

The platform automates infrastructure provisioning, application deployment, and monitoring in a fully cloud-native workflow.

Architecture Overview
Internet
   ↓
AWS Application Load Balancer
   ↓
Kubernetes Ingress
   ↓
Application Pods
   ↓
Prometheus Metrics
   ↓
Grafana Observability

Infrastructure provisioning and GitOps automation are handled by Terraform and ArgoCD.

Infrastructure Provisioning (Terraform)

Terraform provisions the AWS infrastructure including the VPC, subnets, security groups, and EKS cluster.

Container Image in Amazon ECR

The application container is built and pushed to Amazon ECR for deployment inside Kubernetes.

Kubernetes Ingress and Load Balancer

Traffic enters the cluster through an AWS Application Load Balancer managed by the Kubernetes AWS Load Balancer Controller.

GitOps Continuous Deployment (ArgoCD)

ArgoCD continuously monitors the Git repository and automatically synchronizes Kubernetes resources with the desired state.

Platform Observability (Grafana)

Prometheus collects metrics from the cluster and Grafana visualizes system health, enabling real-time monitoring of CPU, memory, and pod activity.

Simulated Deployment Failure

During testing, the nginx deployment was intentionally scaled beyond the cluster's scheduling capacity. This caused pods to enter a Pending state due to pod-per-node limits.

The issue was diagnosed using Kubernetes scheduling events and resolved by scaling the EKS node group to increase cluster capacity.

Incident details are documented in:

docs/incidents/simulated-deployment-failure.md
Technology Stack

Terraform
AWS EKS
Kubernetes
ArgoCD GitOps
Prometheus
Grafana
AWS Application Load Balancer