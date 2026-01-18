# Learning Educates

[![Educates](https://img.shields.io/badge/Educates-2.x-blue)](https://educates.dev/)
[![Azure AKS](https://img.shields.io/badge/Azure-AKS-0078D4)](https://azure.microsoft.com/en-us/services/kubernetes-service/)
[![License](https://img.shields.io/badge/License-Apache%202.0-green)](LICENSE)

> **Comprehensive learning repository for Educates Training Platform - an open-source platform for hosting interactive workshop environments in Kubernetes.**

This repository documents the journey of learning and implementing Educates on Azure Kubernetes Service (AKS) to create hands-on training workshops for cloud-native applications, with a specific focus on teaching the [Agility Game](https://github.com/agility-game/) microservices architecture.

## 📋 Table of Contents

- [Overview](#overview)
- [What is Educates?](#what-is-educates)
- [Repository Structure](#repository-structure)
- [Prerequisites](#prerequisites)
- [Quick Start](#quick-start)
- [Installation Guides](#installation-guides)
  - [Azure AKS Setup](#azure-aks-setup)
  - [Educates Installation](#educates-installation)
- [Workshop Development](#workshop-development)
- [Agility Game Integration](#agility-game-integration)
- [Learning Resources](#learning-resources)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

## 🎯 Overview

**Project Goals:**

1. Master the Educates Training Platform for creating interactive Kubernetes workshops
1. Deploy Educates on Azure Kubernetes Service (AKS)
1. Develop workshops for teaching microservices architecture using Agility Game
1. Create reusable workshop templates for cloud-native development training

**Use Cases:**

- Teaching Kubernetes fundamentals
- Demonstrating microservices deployment patterns
- Interactive coding workshops
- Product demonstrations
- Developer onboarding programs

## 🚀 What is Educates?

[Educates](https://educates.dev/) is an open-source training platform designed to provide hands-on, interactive workshop environments running on Kubernetes. Originally developed at VMware and now community-maintained, it offers:

**Key Features:**

- **Interactive Terminals**: Built-in terminal access for each workshop session
- **Code Editors**: Integrated web-based editors for hands-on coding
- **Dashboard Views**: Custom dashboards for monitoring applications
- **Markdown/AsciiDoc Support**: Rich workshop instruction formatting
- **Clickable Commands**: Execute commands directly from instructions
- **Multi-Namespace Support**: Isolated environments per user
- **Resource Quotas**: Control resource consumption per session
- **Virtual Clusters**: Optional full cluster admin access via vcluster

**Architecture:**

```
┌─────────────────────────────────────────────────────────┐
│                    Educates Platform                     │
├─────────────────────────────────────────────────────────┤
│                                                          │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐       │
│  │ Workshop 1 │  │ Workshop 2 │  │ Workshop N │       │
│  └────────────┘  └────────────┘  └────────────┘       │
│         │               │               │              │
│  ┌──────▼───────────────▼───────────────▼──────┐      │
│  │         Training Portal Manager             │      │
│  └──────────────────────────────────────────────┘      │
│         │                                               │
│  ┌──────▼──────────────────────────────────────┐      │
│  │      Session Manager (Operator)             │      │
│  └──────────────────────────────────────────────┘      │
│                                                          │
└─────────────────────────────────────────────────────────┘
                        │
        ┌───────────────┴───────────────┐
        │                                │
┌───────▼────────┐              ┌───────▼────────┐
│ Kubernetes API │              │  Ingress/DNS   │
└────────────────┘              └────────────────┘
```

## 📁 Repository Structure

```
learning-educates/
├── README.md                          # This file
├── docs/                              # Documentation
│   ├── 01-introduction/
│   │   ├── what-is-educates.md
│   │   ├── architecture.md
│   │   └── use-cases.md
│   ├── 02-setup/
│   │   ├── azure-aks-setup.md        # AKS cluster creation
│   │   ├── educates-installation.md  # Installing Educates
│   │   ├── dns-configuration.md      # DNS and ingress setup
│   │   └── troubleshooting.md
│   ├── 03-workshop-development/
│   │   ├── workshop-structure.md
│   │   ├── custom-resources.md
│   │   ├── content-creation.md
│   │   └── best-practices.md
│   ├── 04-advanced-topics/
│   │   ├── virtual-clusters.md
│   │   ├── custom-images.md
│   │   ├── resource-management.md
│   │   └── security-policies.md
│   └── 05-agility-game/
│       ├── overview.md
│       ├── microservices-architecture.md
│       ├── workshop-design.md
│       └── deployment-patterns.md
├── examples/                          # Example configurations
│   ├── aks-config/
│   │   ├── cluster-config.yaml
│   │   ├── terraform/
│   │   └── bicep/
│   ├── educates-config/
│   │   ├── values.yaml
│   │   └── infrastructure-providers/
│   └── workshops/
│       ├── kubernetes-basics/
│       ├── microservices-101/
│       └── agility-game-deployment/
├── workshops/                         # Workshop content
│   ├── template-workshop/            # Workshop template
│   ├── agility-game-intro/           # Intro to Agility Game
│   ├── space-selector-deployment/    # Deploy space-selector
│   └── microservices-complete/       # Full microservices workshop
├── scripts/                           # Automation scripts
│   ├── setup/
│   │   ├── create-aks-cluster.sh
│   │   ├── install-educates.sh
│   │   └── configure-dns.sh
│   ├── workshop-tools/
│   │   ├── create-workshop.sh
│   │   ├── publish-workshop.sh
│   │   └── test-workshop.sh
│   └── utilities/
│       ├── cleanup.sh
│       └── backup-workshops.sh
├── infrastructure/                    # Infrastructure as Code
│   ├── terraform/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── modules/
│   └── bicep/
│       ├── main.bicep
│       └── modules/
└── notebooks/                         # Jupyter notebooks for learning
    ├── educates-basics.ipynb
    ├── workshop-development.ipynb
    └── aks-integration.ipynb
```

## 📋 Prerequisites

### Required Tools

|Tool        |Version|Purpose                             |
|------------|-------|------------------------------------|
|Azure CLI   |2.77.0+|Azure resource management           |
|kubectl     |1.28+  |Kubernetes cluster management       |
|Educates CLI|2.x    |Educates installation and management|
|Docker      |20.10+ |Container image building            |
|Git         |2.x    |Version control                     |
|jq          |1.6+   |JSON processing                     |

### Azure Requirements

- **Azure Subscription**: Active subscription with quota for:
  - Virtual Machines (4+ vCPUs minimum)
  - Public IP addresses
  - Load Balancers
- **Permissions**: Contributor or Owner role on subscription
- **Resource Providers**: Registered:
  - `Microsoft.ContainerService`
  - `Microsoft.Network`
  - `Microsoft.Compute`

### Knowledge Prerequisites

- **Kubernetes**: Basic understanding of pods, services, deployments
- **Azure**: Familiarity with Azure portal and CLI
- **YAML**: Ability to read and edit YAML configurations
- **Networking**: Basic DNS and ingress concepts
- **Markdown**: For workshop content creation

### Install Required Tools

**macOS (Homebrew):**

```bash
# Azure CLI
brew install azure-cli

# kubectl
brew install kubectl

# Educates CLI
brew install educates

# Docker Desktop
brew install --cask docker

# Additional tools
brew install jq git
```

**Linux (Ubuntu/Debian):**

```bash
# Azure CLI
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash

# kubectl
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl

# Educates CLI
curl -Lo /tmp/educates-linux-amd64.tar.gz \
  "https://github.com/educates/educates-training-platform/releases/latest/download/educates-linux-amd64.tar.gz"
tar xvfz /tmp/educates-linux-amd64.tar.gz -C /usr/local/bin educates

# Docker
sudo apt-get update
sudo apt-get install docker.io

# Additional tools
sudo apt-get install jq git
```

**Windows (PowerShell):**

```powershell
# Azure CLI
Invoke-WebRequest -Uri https://aka.ms/installazurecliwindows -OutFile .\AzureCLI.msi
Start-Process msiexec.exe -Wait -ArgumentList '/I AzureCLI.msi /quiet'

# kubectl
Install-Script -Name install-kubectl -Scope CurrentUser -Force
install-kubectl.ps1

# Educates CLI (download from releases)
# https://github.com/educates/educates-training-platform/releases

# Docker Desktop for Windows
# Download from https://www.docker.com/products/docker-desktop

# Chocolatey for additional tools
choco install jq git
```

## 🚀 Quick Start

### 1. Clone Repository

```bash
git clone https://github.com/vanHeemstraSystems/learning-educates.git
cd learning-educates
```

### 2. Set Up Azure AKS Cluster

```bash
# Set environment variables
export RESOURCE_GROUP="educates-rg"
export LOCATION="westeurope"
export CLUSTER_NAME="educates-aks"
export NODE_COUNT=3
export NODE_SIZE="Standard_D4s_v3"

# Login to Azure
az login

# Create resource group
az group create --name $RESOURCE_GROUP --location $LOCATION

# Create AKS cluster
az aks create \
  --resource-group $RESOURCE_GROUP \
  --name $CLUSTER_NAME \
  --node-count $NODE_COUNT \
  --node-vm-size $NODE_SIZE \
  --enable-managed-identity \
  --generate-ssh-keys \
  --network-plugin azure \
  --network-policy azure

# Get credentials
az aks get-credentials --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME
```

### 3. Install Educates

```bash
# Create Educates configuration
cat > educates-config.yaml << 'YAML'
clusterInfrastructure:
  provider: custom  # Use 'custom' for AKS

clusterIngress:
  domain: "educates.your-domain.com"  # Replace with your domain

clusterSecurity:
  policyEngine: kyverno

workshopSecurity:
  rulesEngine: kyverno
YAML

# Install Educates using the CLI
educates admin cluster install --config educates-config.yaml

# Verify installation
kubectl get pods -n educates
```

### 4. Deploy Your First Workshop

```bash
# Navigate to workshop template
cd workshops/template-workshop

# Deploy workshop
kubectl apply -f workshop-definition.yaml

# Create training portal
kubectl apply -f training-portal.yaml

# Get portal URL
kubectl get trainingportal
```

## 📚 Installation Guides

### Azure AKS Setup

For detailed AKS cluster setup, see <docs/02-setup/azure-aks-setup.md>

**Key Configuration Options:**

1. **Network Configuration**
- Azure CNI for pod networking
- Network policies for security
- Public/Private cluster options
1. **Node Pool Configuration**
- System node pool (for cluster services)
- User node pool (for workshops)
- Auto-scaling configuration
1. **Security & Identity**
- Managed Identity
- Azure AD integration
- RBAC configuration
1. **Monitoring & Logging**
- Azure Monitor integration
- Container Insights
- Log Analytics workspace

**Example Terraform Configuration:**

```hcl
# See infrastructure/terraform/main.tf for complete example
resource "azurerm_kubernetes_cluster" "educates" {
  name                = "educates-aks"
  location            = azurerm_resource_group.educates.location
  resource_group_name = azurerm_resource_group.educates.name
  dns_prefix          = "educates"

  default_node_pool {
    name       = "system"
    node_count = 2
    vm_size    = "Standard_D2s_v3"
  }

  identity {
    type = "SystemAssigned"
  }

  network_profile {
    network_plugin = "azure"
    network_policy = "azure"
  }
}
```

### Educates Installation

For step-by-step Educates installation, see <docs/02-setup/educates-installation.md>

**Installation Methods:**

1. **Using Educates CLI** (Recommended)
   
   ```bash
   educates admin cluster install --config config.yaml
   ```
1. **Using kapp-controller**
   
   ```bash
   kubectl apply -f https://github.com/educates/educates-training-platform/releases/latest/download/educates-installer.yaml
   ```

**Configuration for Azure AKS:**

```yaml
# educates-config.yaml
clusterInfrastructure:
  provider: custom
  domain: "educates.yourdomain.com"

clusterIngress:
  domain: "*.educates.yourdomain.com"
  tlsCertificateRef:
    namespace: "educates-secrets"
    name: "educates-tls"

clusterSecurity:
  policyEngine: kyverno

workshopSecurity:
  rulesEngine: kyverno

imageRegistry:
  host: "your-acr.azurecr.io"
  namespace: "educates"

storage:
  class: "managed-premium"
  group: 2000
  user: 1001
```

## 🎓 Workshop Development

### Workshop Structure

Every Educates workshop consists of:

```
workshop-name/
├── workshop.yaml              # Workshop definition (metadata, resources)
├── resources/                 # Kubernetes resources to deploy
│   ├── deployment.yaml
│   ├── service.yaml
│   └── configmap.yaml
├── exercises/                 # Workshop content
│   ├── 01-introduction.md
│   ├── 02-setup.md
│   ├── 03-deployment.md
│   └── 04-conclusion.md
├── workshop/                  # Additional workshop files
│   ├── setup.d/              # Setup scripts
│   ├── profile.d/            # Environment setup
│   └── content/              # Static content (images, etc.)
└── README.md                 # Workshop documentation
```

### Creating a Workshop

```bash
# Use the provided script
./scripts/workshop-tools/create-workshop.sh my-new-workshop

# Or manually using Educates CLI
educates create-workshop my-new-workshop
```

### Workshop Definition Example

```yaml
# workshop.yaml
apiVersion: training.educates.dev/v1beta1
kind: Workshop
metadata:
  name: agility-game-deployment
spec:
  title: "Deploy Agility Game Microservices"
  description: "Learn to deploy microservices on Kubernetes"
  vendor: "vanHeemstraSystems"
  difficulty: intermediate
  duration: 60m
  url: https://github.com/vanHeemstraSystems/learning-educates
  
  workshop:
    image: ghcr.io/educates/jdk17-environment:main
  
  session:
    namespaces:
      budget: medium
      limits:
        min:
          cpu: 1
          memory: 1Gi
        max:
          cpu: 2
          memory: 4Gi
    
    applications:
      terminal:
        enabled: true
        layout: split
      editor:
        enabled: true
      console:
        enabled: true
        vendor: kubernetes
  
  environment:
    objects:
    - apiVersion: v1
      kind: Namespace
      metadata:
        name: $(session_namespace)-apps
```

## 🎮 Agility Game Integration

### Overview

The [Agility Game](https://github.com/agility-game/) is a microservices-based application designed for teaching project management and software development methodologies. This repository focuses on creating Educates workshops to teach deploying and managing these microservices.

### Space Selector Microservice

**space-selector** is a web application component of the Agility Game that handles space/room selection functionality.

**Workshop Integration Plan:**

1. **Workshop 1: Introduction to Space Selector**
- Overview of microservice architecture
- Understanding the space-selector component
- Local development setup
1. **Workshop 2: Containerization**
- Creating Dockerfile for space-selector
- Building container images
- Pushing to Azure Container Registry
1. **Workshop 3: Kubernetes Deployment**
- Creating Kubernetes manifests
- Deploying to AKS
- Exposing via ingress
1. **Workshop 4: Advanced Patterns**
- ConfigMaps and Secrets
- Health checks and monitoring
- Scaling strategies

### Example Workshop: Deploy Space Selector

```markdown
# Deploy Space Selector to Kubernetes

## Introduction

In this workshop, you'll learn how to deploy the space-selector microservice
from the Agility Game to your Kubernetes cluster.

## Prerequisites

- Basic understanding of Docker
- Familiarity with Kubernetes concepts
- Access to Azure Container Registry

## Step 1: Review the Application

Let's examine the space-selector application:

```execute
cat /opt/agility-game/space-selector/package.json
```

## Step 2: Build Container Image

Build the Docker image:

```execute
docker build -t $REGISTRY_HOST/space-selector:v1.0 .
```

## Step 3: Push to Registry

Push the image to Azure Container Registry:

```execute
docker push $REGISTRY_HOST/space-selector:v1.0
```

## Step 4: Deploy to Kubernetes

Apply the deployment manifest:

```execute
kubectl apply -f deployment.yaml
```

Verify the deployment:

```execute
kubectl get pods -n $(session_namespace)
```

## Step 5: Access the Application

The application is now accessible at:

https://space-selector-$(session_namespace).$(ingress_domain)

## Conclusion

You’ve successfully deployed a microservice to Kubernetes!

```
### Agility Game Workshop Series

Planned workshop progression:

1. **agility-game-intro**: Introduction to Agility Game and microservices
2. **space-selector-deployment**: Deploy space-selector (as shown above)
3. **service-mesh-basics**: Implement service mesh for microservice communication
4. **observability**: Add monitoring and logging
5. **ci-cd-pipeline**: Automated deployment pipeline
6. **microservices-complete**: Full Agility Game deployment

## 📚 Learning Resources

### Official Documentation
- [Educates Documentation](https://docs.educates.dev/)
- [Educates GitHub](https://github.com/educates/educates-training-platform)
- [Azure AKS Documentation](https://learn.microsoft.com/en-us/azure/aks/)

### Tutorials & Guides
- [Getting Started with Educates](docs/01-introduction/what-is-educates.md)
- [Workshop Development Guide](docs/03-workshop-development/workshop-structure.md)
- [Best Practices](docs/03-workshop-development/best-practices.md)

### Community
- [Educates Community](https://educates.dev/)
- [GitHub Discussions](https://github.com/educates/educates-training-platform/discussions)
- [Kubernetes Slack](https://kubernetes.slack.com/) - #educates channel

### Example Workshops
- [Official Educates Samples](https://github.com/educates/educates-training-platform/tree/main/samples)
- [Lab Kubernetes Tutorial](https://github.com/educates/lab-k8s-fundamentals)

## 🔧 Troubleshooting

### Common Issues

#### Issue: Pods not starting

**Symptoms:**
```

kubectl get pods -n educates
NAME                               READY   STATUS             RESTARTS   AGE
session-manager-xxx                0/1     ImagePullBackOff   0          2m

```
**Solution:**
1. Check image pull secrets
2. Verify Azure Container Registry authentication
3. Check node resources

```bash
kubectl describe pod session-manager-xxx -n educates
kubectl top nodes
```

#### Issue: Workshop sessions not accessible

**Symptoms:**

- Training portal shows workshops but sessions fail to create
- DNS resolution errors

**Solution:**

1. Verify DNS configuration
1. Check ingress controller
1. Validate certificate configuration

```bash
# Check ingress
kubectl get ingress -A

# Check DNS
nslookup educates.yourdomain.com

# Check certificates
kubectl get certificate -n educates
```

#### Issue: AKS cluster quota exceeded

**Symptoms:**

```
Error: (QuotaExceeded) Operation could not be completed as it results in exceeding approved Total Regional Cores quota.
```

**Solution:**

```bash
# Check current quota
az vm list-usage --location westeurope -o table

# Request quota increase
az support tickets create --title "AKS quota increase" ...
```

For more troubleshooting tips, see <docs/02-setup/troubleshooting.md>

## 🤝 Contributing

Contributions are welcome! Please see <CONTRIBUTING.md> for guidelines.

### How to Contribute

1. Fork the repository
1. Create a feature branch (`git checkout -b feature/amazing-workshop`)
1. Commit your changes (`git commit -m 'Add amazing workshop'`)
1. Push to the branch (`git push origin feature/amazing-workshop`)
1. Open a Pull Request

### Development Workflow

```bash
# Clone your fork
git clone https://github.com/YOUR_USERNAME/learning-educates.git

# Add upstream remote
git remote add upstream https://github.com/vanHeemstraSystems/learning-educates.git

# Create feature branch
git checkout -b feature/my-feature

# Make changes and test
./scripts/workshop-tools/test-workshop.sh my-workshop

# Commit and push
git add .
git commit -m "Description of changes"
git push origin feature/my-feature
```

## 📝 License

This project is licensed under the Apache License 2.0 - see the <LICENSE> file for details.

Educates is also licensed under Apache License 2.0 - see [Educates License](https://github.com/educates/educates-training-platform/blob/main/LICENSE).

## 🙏 Acknowledgments

- [Educates Project](https://educates.dev/) - The amazing platform this learning material is based on
- [Graham Dumpleton](https://github.com/GrahamDumpleton) & [Jorge Morales](https://github.com/jorgemoralespou) - Original creators of Educates
- Educates Community - For continued development and support
- [Agility Game](https://github.com/agility-game/) - Example microservices application

-----

## 📞 Contact & Support

**Repository Maintainer:** Willem van Heemstra

- **GitHub:** [@vanHeemstraSystems](https://github.com/vanHeemstraSystems)
- **Project:** [Agility Game](https://github.com/agility-game/)

**Need Help?**

1. Check the [documentation](docs/)
1. Review [troubleshooting guide](docs/02-setup/troubleshooting.md)
1. Open an [issue](https://github.com/vanHeemstraSystems/learning-educates/issues)
1. Join the [discussions](https://github.com/vanHeemstraSystems/learning-educates/discussions)

-----

**Note:** This is a learning repository for understanding Educates and deploying it on Azure AKS. For production deployments, ensure you follow all security best practices and Azure Well-Architected Framework guidelines.

**Started:** January 2026  
**Status:** Active Development  

