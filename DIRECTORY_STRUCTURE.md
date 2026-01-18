# Directory Structure Guide

This document explains the complete directory structure of the learning-educates repository and the purpose of each directory and key files.

## Root Level Structure

```
learning-educates/
├── README.md                   # Main repository documentation
├── LICENSE                     # Apache 2.0 license
├── CONTRIBUTING.md            # Contribution guidelines
├── DIRECTORY_STRUCTURE.md     # This file
├── .gitignore                 # Git ignore patterns
├── docs/                      # Comprehensive documentation
├── examples/                  # Example configurations
├── workshops/                 # Workshop content
├── scripts/                   # Automation scripts
├── infrastructure/            # Infrastructure as Code
└── notebooks/                 # Learning notebooks
```

## Detailed Directory Breakdown

### 📚 /docs

Comprehensive documentation organized by learning progression:

```
docs/
├── 01-introduction/
│   ├── README.md              # Section overview
│   ├── what-is-educates.md    # Introduction to Educates
│   ├── architecture.md        # System architecture deep-dive
│   ├── use-cases.md          # Real-world applications
│   └── comparison.md         # Educates vs alternatives
│
├── 02-setup/
│   ├── README.md              
│   ├── prerequisites.md       # Detailed prerequisites
│   ├── azure-aks-setup.md    # Complete AKS setup guide
│   ├── educates-installation.md  # Educates installation
│   ├── dns-configuration.md   # DNS and ingress configuration
│   ├── ssl-certificates.md    # SSL/TLS setup
│   ├── troubleshooting.md     # Common issues and solutions
│   └── verification.md        # Post-installation verification
│
├── 03-workshop-development/
│   ├── README.md
│   ├── workshop-structure.md  # Workshop file organization
│   ├── custom-resources.md    # Educates CRDs explained
│   ├── content-creation.md    # Writing workshop content
│   ├── markdown-features.md   # Markdown extensions
│   ├── executable-commands.md # Clickable commands
│   ├── best-practices.md      # Workshop development best practices
│   ├── testing.md            # Testing workshops
│   └── publishing.md         # Publishing to registries
│
├── 04-advanced-topics/
│   ├── README.md
│   ├── virtual-clusters.md    # Using vcluster for admin access
│   ├── custom-images.md       # Creating custom workshop images
│   ├── resource-management.md # Quotas, limits, and budgets
│   ├── security-policies.md   # Kyverno policies
│   ├── multi-tenancy.md      # Multi-tenant workshops
│   ├── custom-dashboards.md   # Creating custom dashboards
│   └── integration.md        # Integrating with external systems
│
└── 05-agility-game/
    ├── README.md
    ├── overview.md            # Agility Game overview
    ├── microservices-architecture.md  # Architecture details
    ├── space-selector.md     # Space selector microservice
    ├── workshop-design.md    # Workshop series design
    ├── deployment-patterns.md # Deployment strategies
    ├── service-mesh.md       # Service mesh integration
    └── observability.md      # Monitoring and logging
```

### 💡 /examples

Reference configurations and templates:

```
examples/
├── README.md                  # Examples overview
│
├── aks-config/
│   ├── README.md
│   ├── basic-cluster.yaml    # Basic AKS configuration
│   ├── production-cluster.yaml  # Production-ready config
│   ├── cluster-config.yaml   # Generic cluster config
│   ├── terraform/            # Terraform examples
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   ├── outputs.tf
│   │   └── README.md
│   └── bicep/               # Bicep examples
│       ├── main.bicep
│       ├── modules/
│       └── README.md
│
├── educates-config/
│   ├── README.md
│   ├── values.yaml          # Base values file
│   ├── values-aks.yaml      # AKS-specific values
│   ├── values-production.yaml  # Production values
│   └── infrastructure-providers/
│       ├── aks.yaml
│       ├── eks.yaml
│       └── gke.yaml
│
└── workshops/
    ├── README.md
    ├── kubernetes-basics/   # Example: Kubernetes fundamentals
    │   ├── workshop.yaml
    │   ├── resources/
    │   └── exercises/
    ├── microservices-101/   # Example: Microservices intro
    │   ├── workshop.yaml
    │   ├── resources/
    │   └── exercises/
    └── agility-game-deployment/  # Example: Full deployment
        ├── workshop.yaml
        ├── resources/
        └── exercises/
```

### 🎓 /workshops

Actual workshop content for use with Educates:

```
workshops/
├── README.md                 # Workshop catalog
│
├── template-workshop/        # Reusable workshop template
│   ├── README.md
│   ├── workshop.yaml        # Workshop definition
│   ├── resources/           # K8s resources
│   │   ├── namespace.yaml
│   │   ├── deployment.yaml
│   │   ├── service.yaml
│   │   └── ingress.yaml
│   ├── exercises/           # Workshop content
│   │   ├── 01-introduction.md
│   │   ├── 02-setup.md
│   │   ├── 03-implementation.md
│   │   └── 04-conclusion.md
│   ├── workshop/            # Additional files
│   │   ├── setup.d/        # Setup scripts
│   │   │   └── 01-init.sh
│   │   ├── profile.d/      # Environment variables
│   │   │   └── env.sh
│   │   └── content/        # Static assets
│   │       └── images/
│   └── Dockerfile          # Custom workshop image (optional)
│
├── agility-game-intro/      # Workshop 1: Introduction
│   ├── README.md
│   ├── workshop.yaml
│   ├── resources/
│   ├── exercises/
│   │   ├── 01-what-is-agility-game.md
│   │   ├── 02-microservices-overview.md
│   │   ├── 03-architecture-tour.md
│   │   └── 04-next-steps.md
│   └── workshop/
│
├── space-selector-deployment/  # Workshop 2: Deploy space-selector
│   ├── README.md
│   ├── workshop.yaml
│   ├── resources/
│   │   ├── space-selector-deployment.yaml
│   │   ├── space-selector-service.yaml
│   │   ├── space-selector-ingress.yaml
│   │   └── acr-secret.yaml
│   ├── exercises/
│   │   ├── 01-container-overview.md
│   │   ├── 02-build-image.md
│   │   ├── 03-push-to-registry.md
│   │   ├── 04-deploy-to-kubernetes.md
│   │   ├── 05-expose-service.md
│   │   └── 06-testing-and-validation.md
│   └── workshop/
│       ├── setup.d/
│       │   ├── 01-clone-repo.sh
│       │   └── 02-acr-login.sh
│       └── content/
│           └── diagrams/
│
└── microservices-complete/  # Workshop 3: Full deployment
    ├── README.md
    ├── workshop.yaml
    ├── resources/
    │   ├── namespaces/
    │   ├── databases/
    │   ├── microservices/
    │   └── ingress/
    ├── exercises/
    │   ├── 01-preparation.md
    │   ├── 02-database-setup.md
    │   ├── 03-deploy-services.md
    │   ├── 04-service-mesh.md
    │   ├── 05-observability.md
    │   └── 06-advanced-patterns.md
    └── workshop/
        └── setup.d/
            ├── 01-infrastructure.sh
            ├── 02-dependencies.sh
            └── 03-config.sh
```

### 🔧 /scripts

Automation and utility scripts:

```
scripts/
├── README.md                # Scripts documentation
│
├── setup/                   # Infrastructure setup
│   ├── README.md
│   ├── create-aks-cluster.sh      # Create AKS cluster
│   ├── install-educates.sh        # Install Educates
│   ├── configure-dns.sh           # Configure DNS/ingress
│   ├── setup-acr.sh              # Azure Container Registry
│   └── install-dependencies.sh    # Install required tools
│
├── workshop-tools/          # Workshop management
│   ├── README.md
│   ├── create-workshop.sh        # Create new workshop
│   ├── validate-workshop.sh      # Validate workshop files
│   ├── test-workshop.sh          # Test workshop locally
│   ├── publish-workshop.sh       # Publish to registry
│   ├── deploy-workshop.sh        # Deploy to cluster
│   └── list-workshops.sh         # List available workshops
│
└── utilities/               # General utilities
    ├── README.md
    ├── cleanup.sh           # Clean up resources
    ├── backup-workshops.sh  # Backup workshop content
    ├── monitor-cluster.sh   # Cluster monitoring
    ├── check-quotas.sh     # Check resource quotas
    └── export-logs.sh      # Export logs
```

### 🏗️ /infrastructure

Infrastructure as Code for AKS and related resources:

```
infrastructure/
├── README.md
│
├── terraform/               # Terraform configurations
│   ├── README.md
│   ├── main.tf             # Main configuration
│   ├── variables.tf        # Variable definitions
│   ├── outputs.tf          # Output definitions
│   ├── terraform.tfvars    # Variable values (gitignored)
│   ├── terraform.tfvars.example  # Example values
│   ├── versions.tf         # Provider versions
│   ├── modules/            # Reusable modules
│   │   ├── aks-cluster/
│   │   │   ├── main.tf
│   │   │   ├── variables.tf
│   │   │   └── outputs.tf
│   │   ├── network/
│   │   │   ├── main.tf
│   │   │   ├── variables.tf
│   │   │   └── outputs.tf
│   │   ├── acr/
│   │   │   ├── main.tf
│   │   │   ├── variables.tf
│   │   │   └── outputs.tf
│   │   └── monitoring/
│   │       ├── main.tf
│   │       ├── variables.tf
│   │       └── outputs.tf
│   └── environments/       # Environment-specific configs
│       ├── dev/
│       │   └── terraform.tfvars
│       ├── staging/
│       │   └── terraform.tfvars
│       └── production/
│           └── terraform.tfvars
│
└── bicep/                  # Bicep configurations
    ├── README.md
    ├── main.bicep         # Main deployment
    ├── parameters.json    # Parameters (gitignored)
    ├── parameters.json.example  # Example parameters
    └── modules/           # Reusable modules
        ├── aks.bicep
        ├── network.bicep
        ├── acr.bicep
        └── monitoring.bicep
```

### 📓 /notebooks

Jupyter notebooks for interactive learning:

```
notebooks/
├── README.md                      # Notebooks overview
├── requirements.txt              # Python dependencies
├── .env.example                  # Environment variables example
│
├── 01-educates-basics.ipynb     # Introduction to Educates
├── 02-aks-setup.ipynb           # Setting up AKS
├── 03-workshop-development.ipynb  # Creating workshops
├── 04-kubernetes-resources.ipynb  # Working with K8s resources
├── 05-agility-game-deployment.ipynb  # Deploying Agility Game
├── 06-advanced-patterns.ipynb   # Advanced deployment patterns
│
└── utils/                        # Shared utilities
    ├── __init__.py
    ├── aks_helper.py            # AKS interaction helpers
    ├── educates_helper.py       # Educates helpers
    └── workshop_helper.py       # Workshop management helpers
```

## Key Files Explained

### Root Level Files

#### README.md

Main repository documentation. Contains:

- Project overview and goals
- Quick start guide
- Links to detailed documentation
- Prerequisites and installation
- Contact information

#### LICENSE

Apache 2.0 license file for the repository.

#### CONTRIBUTING.md

Guidelines for contributing to the repository:

- Code of conduct
- How to submit issues
- Pull request process
- Development workflow
- Testing requirements

#### .gitignore

Specifies files and directories to ignore:

```gitignore
# Terraform
*.tfstate
*.tfstate.backup
.terraform/
*.tfvars

# Environment files
.env
*.env

# IDE
.vscode/
.idea/
*.swp

# OS
.DS_Store
Thumbs.db

# Jupyter
.ipynb_checkpoints/

# Secrets
secrets/
*.pem
*.key
```

### Workshop Files

#### workshop.yaml

Main workshop definition file. Specifies:

- Workshop metadata (title, description, vendor)
- Docker image to use
- Resource requirements
- Session configuration
- Applications to enable (terminal, editor, etc.)
- Environment objects to create

Example structure:

```yaml
apiVersion: training.educates.dev/v1beta1
kind: Workshop
metadata:
  name: workshop-name
spec:
  title: "Workshop Title"
  description: "Workshop description"
  vendor: "vanHeemstraSystems"
  difficulty: beginner|intermediate|advanced
  duration: 30m|1h|2h
  url: https://github.com/...
  
  workshop:
    image: workshop-image:tag
  
  session:
    namespaces:
      budget: small|medium|large
    applications:
      terminal:
        enabled: true
      editor:
        enabled: true
      console:
        enabled: true
  
  environment:
    objects:
    - # Kubernetes resources
```

#### resources/

Directory containing Kubernetes manifests that will be:

- Pre-deployed to the workshop environment
- Created per session
- Shared across all sessions

#### exercises/

Markdown files containing workshop instructions:

- Numbered sequentially (01-, 02-, etc.)
- Contains explanatory text
- Includes executable command blocks
- Can reference variables

#### workshop/setup.d/

Bash scripts run during workshop initialization:

- Files executed in alphanumeric order
- Must be executable (`chmod +x`)
- Used for:
  - Cloning repositories
  - Installing dependencies
  - Configuring environment

#### workshop/profile.d/

Shell scripts sourced into user’s environment:

- Sets environment variables
- Configures PATH
- Defines aliases
- Creates shell functions

## Creating New Content

### Adding a New Workshop

1. Copy the template:
   
   ```bash
   cp -r workshops/template-workshop workshops/my-new-workshop
   ```
1. Update workshop.yaml with your workshop details
1. Create your exercises in exercises/
1. Add necessary resources in resources/
1. Test locally:
   
   ```bash
   ./scripts/workshop-tools/test-workshop.sh my-new-workshop
   ```

### Adding New Documentation

1. Identify the appropriate docs/ subdirectory
1. Create your markdown file following the naming convention
1. Update the README.md in that section
1. Link from the main README.md if it’s a major addition

### Adding Scripts

1. Place in the appropriate scripts/ subdirectory
1. Make executable: `chmod +x script-name.sh`
1. Add documentation in the script header
1. Update scripts/README.md with usage information

## File Naming Conventions

### Workshops

- Directory names: `lowercase-with-dashes`
- Exercise files: `##-descriptive-name.md` (e.g., `01-introduction.md`)
- Resource files: `resource-type-name.yaml` (e.g., `deployment-api.yaml`)

### Documentation

- File names: `lowercase-with-dashes.md`
- Section READMEs: Always `README.md`

### Scripts

- File names: `lowercase-with-dashes.sh`
- Executable: Always `chmod +x`

### Infrastructure

- Terraform: Standard Terraform naming (main.tf, variables.tf, etc.)
- Bicep: Standard Bicep naming (main.bicep, modules/*.bicep)

## Version Control

### What to Commit

- Source code and scripts
- Documentation
- Workshop content
- Example configurations
- Infrastructure templates (without sensitive data)

### What NOT to Commit (.gitignore)

- Secrets and credentials
- Environment-specific configurations
- Terraform state files
- Generated files
- IDE-specific files
- Large binary files

## Next Steps

1. Review the main <README.md> for project overview
1. Read <docs/01-introduction/what-is-educates.md> to understand Educates
1. Follow <docs/02-setup/azure-aks-setup.md> to set up your environment
1. Explore example workshops in <examples/workshops/>
1. Create your first workshop using the template in <workshops/template-workshop/>

-----

**Last Updated:** January 2026  
**Maintained by:** Willem van Heemstra (@vanHeemstraSystems)
