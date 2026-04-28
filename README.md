# YAML Templates Repository

A comprehensive collection of enterprise-grade CI/CD pipeline templates for modern software development across multiple platforms and programming languages.

## 🚀 Overview

This repository provides production-ready YAML templates for Continuous Integration (CI) and Continuous Deployment (CD) pipelines across four major platforms. All templates follow strict YAML coding standards and include mandatory security scanning with enterprise-grade best practices.

**Supported Platforms:**
- **GitHub Actions** - GitHub Workflows YAML
- **Azure DevOps** - Azure Pipelines YAML  
- **GitLab CI** - GitLab CI/CD YAML
- **Jenkins** - Jenkins Pipeline (Declarative)

## 📋 Supported Languages & Frameworks

### Backend Languages
- **.NET** (C#, F#, VB.NET)
- **Java** (Spring Boot, Maven, Gradle)
- **Python** (Django, Flask, FastAPI)
- **Node.js** (Express, NestJS)
- **Go** (Gin, Echo, native)
- **Rust** (Actix, Rocket, Axum)
- **PHP** (Laravel, Symfony, CodeIgniter)
- **Ruby** (Rails, Sinatra)

### Frontend Frameworks
- **React** (Create React App, Next.js)
- **Angular** (Angular CLI)
- **Vue.js** (Vue CLI, Nuxt.js)
- **TypeScript** (Pure TypeScript projects)

## 🏗️ Repository Structure

```
yaml-templates/
├── github-actions/
│   ├── ci/                    # CI templates for GitHub Actions
│   │   ├── dotnet-ci.yml
│   │   ├── java-ci.yml
│   │   ├── python-ci.yml
│   │   ├── node-ci.yml
│   │   ├── react-ci.yml
│   │   ├── angular-ci.yml
│   │   ├── vue-ci.yml
│   │   ├── typescript-ci.yml
│   │   ├── go-ci.yml
│   │   ├── rust-ci.yml
│   │   ├── php-ci.yml
│   │   └── ruby-ci.yml
│   └── cd/                    # CD templates for GitHub Actions
│       ├── webapp-cd.yml
│       ├── container-cd.yml
│       ├── aks-cd.yml
│       ├── vm-cd.yml
│       ├── react-cd.yml
│       ├── angular-cd.yml
│       ├── vue-cd.yml
│       ├── typescript-cd.yml
│       ├── go-cd.yml
│       ├── rust-cd.yml
│       ├── php-cd.yml
│       └── ruby-cd.yml
├── azure-devops/
│   ├── ci/                    # CI templates for Azure DevOps
│   └── cd/                    # CD templates for Azure DevOps
├── gitlab-ci/
│   ├── ci/                    # CI templates for GitLab CI
│   └── cd/                    # CD templates for GitLab CI
├── jenkins/
│   ├── ci/                    # CI templates for Jenkins
│   └── cd/                    # CD templates for Jenkins
└── reference/
    └── ai-reference.yml       # AI agent reference guide
```

## 🔧 Template Features

### CI Pipeline Features
- **Build Automation** - Compile, transpile, and package applications
- **Testing** - Unit tests, integration tests, code coverage
- **Code Quality** - Linting, formatting, static analysis
- **Security Scanning** - SAST with Gitleaks, Semgrep, and Trivy
- **Artifact Management** - Build artifact creation and storage

### CD Pipeline Features
- **Multi-Environment Deployment** - Staging and Production environments
- **Deployment Strategies** - Blue-green, rolling updates
- **Infrastructure Targets**:
  - Azure Web Apps
  - Azure Container Apps
  - Azure Kubernetes Service (AKS)
  - Virtual Machines
  - Static Web Apps
- **Verification** - Health checks and smoke tests

## 🛡️ Security Features

All templates include comprehensive security scanning:

- **Gitleaks** - Secret and credential detection
- **Semgrep** - Static application security testing (SAST)
- **Trivy** - Vulnerability scanning for dependencies and containers
- **Dependency Scanning** - Package vulnerability assessment

## 🚀 Quick Start

### 1. Choose Your Platform
Select the appropriate directory for your CI/CD platform:
- `github-actions/` for GitHub Actions
- `azure-devops/` for Azure DevOps Pipelines
- `gitlab-ci/` for GitLab CI/CD
- `jenkins/` for Jenkins

### 2. Select Language Template
Navigate to the `ci/` directory and choose your language:
```bash
# Example: React CI pipeline for GitHub Actions
yaml-templates/github-actions/ci/react-ci.yml
```

### 3. Select Deployment Template
Navigate to the `cd/` directory and choose your deployment target:
```bash
# Example: Container deployment for GitHub Actions
yaml-templates/github-actions/cd/container-cd.yml
```

### 4. Customize Variables
Update the environment variables in the templates:
```yaml
env:
  AZURE_WEBAPP_NAME: "your-app-name"
  NODE_VERSION: "20.x"
  PROJECT_NAME: "${{ github.event.repository.name }}"
```

## 📖 Usage Examples

### GitHub Actions - React Application
```yaml
# .github/workflows/ci.yml
name: "React CI Pipeline"
# Copy content from yaml-templates/github-actions/ci/react-ci.yml

# .github/workflows/cd.yml  
name: "React CD Pipeline"
# Copy content from yaml-templates/github-actions/cd/react-cd.yml
```

### Azure DevOps - .NET Web App Pipeline
```yaml
# azure-pipelines-ci.yml
# Copy content from yaml-templates/azure-devops/ci/dotnet-ci.yml

# azure-pipelines-cd.yml
# Copy content from yaml-templates/azure-devops/cd/webapp-cd.yml
```

### GitLab CI - Python Application
```yaml
# .gitlab-ci.yml
# Copy content from yaml-templates/gitlab-ci/ci/python-ci.yml
```

### Jenkins - Go Container Pipeline
```groovy
// Jenkinsfile
// Copy content from yaml-templates/jenkins/ci/go-ci.yml
```

## 🔄 Pipeline Architecture

### Standard CI Pipeline Flow (Mandatory Structure)
Every CI pipeline follows this **mandatory** 4-stage order:

1. **Build Stage**
   - Install language SDK/runtime
   - Restore dependencies  
   - Compile source code
   - Publish/stage build output

2. **Test Stage**
   - Run unit tests
   - Publish test results
   - Generate coverage reports
   - Code quality checks

3. **SAST Stage (Security Scanning)** — **MANDATORY**
   - **Gitleaks** — Secret and credential detection
   - **Semgrep** — Static application security testing (SAST)
   - **Trivy** — Vulnerability scanning for dependencies and containers

4. **Publish Stage**
   - Create build artifacts
   - Archive SAST reports
   - Prepare for CD consumption

### Standard CD Pipeline Flow
1. **Download** - Retrieve build artifacts from CI
2. **Deploy Staging** - Deploy to staging environment with verification
3. **Verify Staging** - Health checks and smoke tests
4. **Deploy Production** - Deploy to production with approval gates
5. **Verify Production** - Final verification and monitoring

## 🎯 Deployment Targets

### Web Applications
- **Azure Web Apps** - PaaS web hosting
- **Static Web Apps** - JAMstack applications
- **App Service** - Containerized web apps

### Containers
- **Azure Container Apps** - Serverless containers
- **Azure Container Instances** - Simple container hosting
- **Docker Registry** - Container image storage

### Kubernetes
- **Azure Kubernetes Service (AKS)** - Managed Kubernetes
- **Helm Charts** - Kubernetes package management
- **kubectl** - Direct Kubernetes deployment

### Infrastructure
- **Virtual Machines** - IaaS deployments
- **Azure Functions** - Serverless computing
- **Logic Apps** - Workflow automation

## 🔧 Configuration & Standards

### YAML Coding Standards
All templates follow these enterprise standards:

- **Document start:** Every file begins with `---`
- **Indentation:** 2 spaces, no tabs
- **Naming:** snake_case for variables, kebab-case for files
- **Comments:** File header + complex block comments
- **Line length:** Max 120 characters
- **Strings:** Quote special characters (`:`, `@`, `#`, etc.)
- **Encoding:** UTF-8

### File Naming Convention
- **CI files:** `{language}-ci.yml` (e.g., `dotnet-ci.yml`, `react-ci.yml`)
- **CD files:** `{target}-cd.yml` (e.g., `webapp-cd.yml`, `container-cd.yml`)

### Required Secrets
Configure these secrets in your CI/CD platform:

#### Azure Deployment
```
AZURE_CREDENTIALS          # Azure service principal
AZURE_WEBAPP_PUBLISH_PROFILE
AZURE_SUBSCRIPTION_ID
AZURE_RESOURCE_GROUP
```

#### Container Registry
```
ACR_USERNAME
ACR_PASSWORD
DOCKER_REGISTRY_URL
CONTAINER_REGISTRY
```

#### Security Scanning
```
GITHUB_TOKEN              # For Gitleaks
SONAR_TOKEN               # Optional
```

### Common Variables Across Platforms
```yaml
# Azure DevOps
PROJECT_NAME: "$(Build.Repository.Name)"
ARTIFACT_NAME: "$(Build.Repository.Name)-drop"

# GitHub Actions  
PROJECT_NAME: "${{ github.event.repository.name }}"
ARTIFACT_NAME: "${{ github.event.repository.name }}-drop"

# GitLab CI
PROJECT_NAME: "$CI_PROJECT_NAME"
ARTIFACT_NAME: "$CI_PROJECT_NAME-drop"

# Jenkins
PROJECT_NAME: "${env.JOB_NAME}"
ARTIFACT_NAME: "${env.JOB_NAME}-drop"
```

## 📊 Template Statistics

- **Total Templates**: 80+
- **CI Templates**: 44 (Multiple languages × 4 platforms)
- **CD Templates**: 28+ (Multiple deployment targets × 4 platforms)
- **Platforms Supported**: 4 (GitHub Actions, Azure DevOps, GitLab CI, Jenkins)
- **Languages Supported**: 12+ (Backend + Frontend frameworks)
- **Deployment Targets**: 8+ (Web Apps, Containers, Kubernetes, VMs, Static Sites)

### Coverage by Platform
- **GitHub Actions**: 24+ templates (Most comprehensive)
- **Azure DevOps**: 15+ templates (Enterprise-focused)
- **GitLab CI**: 17+ templates (DevOps-integrated)
- **Jenkins**: 17+ templates (Traditional CI/CD)

## 🔍 AI Agent Usage

The `yaml-templates/reference/ai-reference.yml` file contains:
- Complete YAML coding standards
- Mandatory CI/CD structure rules
- Language-specific requirements
- Deploy target specifications
- AI generation guidelines

AI agents should read this reference file before generating any YAML templates to ensure consistency and compliance with enterprise standards.

## 🤝 Contributing

### Adding New Templates

#### New Language Support
1. Create `{language}-ci.yml` in each platform's `ci/` folder
2. Follow the mandatory 4-stage structure: Build → Test → SAST → Publish
3. Use platform-specific syntax for language setup
4. Include proper test result publishing
5. Update `file-paths-registry.yml`

#### New Deployment Target
1. Create `{target}-cd.yml` in each platform's `cd/` folder
2. Follow the 2-stage structure: Download → Deploy
3. Include health checks and verification steps
4. Add proper error handling and rollback capabilities

#### New CI/CD Platform
1. Create new folder: `{platform-name}/ci/` and `{platform-name}/cd/`
2. Implement same stage structure using platform's native syntax
3. Ensure SAST stage includes all three security tools
4. Maintain variable naming consistency

### Template Guidelines
- Follow the existing naming convention
- Include comprehensive comments and documentation
- Add mandatory security scanning steps (Gitleaks, Semgrep, Trivy)
- Provide environment variable documentation
- Test templates with real projects
- Use `continueOnError: true` for SAST tools
- Include smoke tests for web deployments

### Validation Requirements
All templates must pass:
- `yamllint` validation
- Platform-specific syntax validation  
- SAST stage presence check
- Artifact naming consistency between CI and CD
- Security scanning tool integration

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

- **Documentation**: Check the `yaml-templates/README.md` for detailed guides
- **Issues**: Report bugs and request features via GitHub Issues
- **Discussions**: Join community discussions for best practices

## 🔗 Related Resources

### Platform Documentation
- [Azure DevOps Pipelines](https://docs.microsoft.com/en-us/azure/devops/pipelines/)
- [GitHub Actions](https://docs.github.com/en/actions)
- [GitLab CI/CD](https://docs.gitlab.com/ee/ci/)
- [Jenkins Pipeline](https://www.jenkins.io/doc/book/pipeline/)

### Security Tools
- [Gitleaks](https://github.com/zricethezav/gitleaks) - Secret Detection
- [Semgrep](https://semgrep.dev/) - Static Analysis
- [Trivy](https://trivy.dev/) - Vulnerability Scanner

### Azure Services
- [Azure Web Apps](https://docs.microsoft.com/en-us/azure/app-service/)
- [Azure Container Apps](https://docs.microsoft.com/en-us/azure/container-apps/)
- [Azure Kubernetes Service](https://docs.microsoft.com/en-us/azure/aks/)
- [Azure Static Web Apps](https://docs.microsoft.com/en-us/azure/static-web-apps/)

## 🏷️ Tags

`ci-cd` `yaml` `github-actions` `azure-devops` `gitlab-ci` `jenkins` `templates` `automation` `devops` `pipeline` `deployment` `security` `sast` `docker` `kubernetes` `azure` `enterprise` `production-ready`

---

**Made with ❤️ for the DevOps community**

*Enterprise-grade CI/CD templates with mandatory security scanning and best practices built-in.*