# Google Online Boutique Microservices Deployment on Kubernetes

This project deploys the Google Online Boutique microservices demo (an e-commerce application) on a Kubernetes (K8s) cluster. The application has been structured to provide two different approaches for deploying microservices on Kubernetes:

1. **Single YAML Configuration Deployment**: Deploy all microservices using a single configuration file located in the `kubernetes-manifests` folder.
2. **Helm Deployment**: Deploy microservices using Helm charts with templated configurations for flexibility and reusability. Helm deployments are managed with Helmfile, making it easy for others to customize and deploy with their values.

![Screenshot 2024-11-02 162757](https://github.com/user-attachments/assets/031aa0e7-fd37-4f60-a00e-874f6b4e1028)

## Project Structure

```plaintext
.
├── charts
│   ├── frontend                # Helm chart for the frontend service
│   ├── microservice-helm       # Helm chart template for generic microservices
│   ├── redis                   # Helm chart for Redis
├── config.yaml                 # Single YAML configuration file for deploying all microservices
├── helmfile.yaml               # Helmfile to manage and deploy all services via Helm
├── kubernetes-manifests        # Kubernetes YAML files for single deployment approach
│   ├── adservice.yaml
│   ├── cartservice.yaml
│   └── ...                     # Other service manifests
├── prometheus                  # Prometheus configuration for monitoring and alerting
│   ├── alert-manager-configuration.yaml
│   ├── alert-rules.yaml
│   └── ...                     # Additional Prometheus configurations
├── values                      # Custom values files for Helm deployments of each service
│   ├── ad-service-values.yaml
│   ├── cart-service-values.yaml
│   └── ...                     # Other service-specific values
└── README.md                   # Project documentation
```
## 1. Single YAML Configuration Deployment
To deploy all microservices using a single configuration YAML, use the files in the kubernetes-manifests folder. These files contain standard Kubernetes manifests for each microservice. This approach can be useful for deploying the entire application quickly without Helm.

To deploy all services at once:
####
    kubectl apply -f config.yaml

## 2. Helm Deployment with Helmfile
Helm charts for more flexible deployments, with templates for common configurations and specific setups for services like frontend and redis. Each service can be customized via values files located in the `values` directory.

The helmfile.yaml file for deploy the entire microservice architecture with a single command, enabling easy customization of values by others.
* **Prerequisite**: Install `helmfile` from [github](https://github.com/helmfile/helmfile)
####
    helmfile sync
## 3. Prometheus Monitoring Setup
The prometheus directory includes configurations for setting up Prometheus to monitor the microservices and handle alerting:

PrometheusRule: Custom rules to monitor metrics such as resource usage.
AlertmanagerConfig: Configuration to send alerts via email or other channels.
To deploy the Prometheus stack (using Helm charts):

####
    kubectl apply -f prometheus/alert-rules.yaml
    kubectl apply -f prometheus/alert-manager-configuration.yaml
## How to Customize and Deploy
##### 1. Custom Values: Modify files in the values folder to override default values for each service.
##### 2. Helm Chart Templates: Edit templates in charts to change the structure or configuration of deployments.
##### 3. Monitoring and Alerting: Customize Prometheus rules and Alertmanager configurations for more granular alerting.
