---
# YAML Templates for CI/CD Pipelines

## Overview

This repository contains enterprise-grade YAML templates for CI/CD pipelines across multiple tools and programming languages. All templates follow strict YAML coding standards and best practices with mandatory security scanning.

## Structure

```
yaml-templates/
├── reference/
│   └── ai-reference.yml         ← AI agent reference with standards and rules
├── azure-devops/
│   ├── ci/                      ← Azure DevOps CI pipelines
│   │   ├── dotnet-ci.yml
│   │   ├── node-ci.yml
│   │   ├── python-ci.yml
│   │   └── java-ci.yml
│   └── cd/                      ← Azure DevOps CD pipelines
│       ├── webapp-cd.yml
│       ├── aks-cd.yml
│       ├── vm-cd.yml
│       └── container-cd.yml
├── github-actions/
│   ├── ci/                      ← GitHub Actions workflows
│   │   └── dotnet-ci.yml
│   └── cd/
│       └── webapp-cd.yml
├── gitlab-ci/
│   ├── ci/                      ← GitLab CI pipelines
│   │   └── dotnet-ci.yml
│   └── cd/
│       └── webapp-cd.yml
└── jenkins/
    ├── ci/                      ← Jenkins pipelines
    │   └── dotnet-ci.yml
    └── cd/
        └── webapp-cd.yml
```

## Supported CI/CD Tools

- **Azure DevOps** — Azure Pipelines YAML
- **GitHub Actions** — GitHub Workflows YAML
- **GitLab CI** — GitLab CI/CD YAML
- **Jenkins** — Jenkins Pipeline (Declarative)

## Supported Languages

- **.NET** — dotnet restore, build, test, publish
- **Node.js** — npm ci, build, test with Jest
- **Python** — pip install, build, pytest
- **Java** — Maven clean, package, test

## Supported Deploy Targets

- **Azure Web App** — Azure App Service with zip deployment
- **AKS** — Azure Kubernetes Service with kubectl
- **VM** — Virtual Machine via SSH copy + restart
- **Container** — Docker build, push, run

## CI Pipeline Structure (All Tools)

Every CI pipeline follows this **mandatory** stage order:

### 1. Build Stage
- Install language SDK/runtime
- Restore dependencies
- Compile source code
- Publish/stage build output

### 2. Test Stage
- Run unit tests
- Publish test results
- Generate test reports

### 3. SAST Stage (Security Scanning)
**Mandatory — Always includes all three tools:**
- **Gitleaks** — Secret and credential detection
- **Semgrep** — Static code analysis
- **Trivy** — Dependency and filesystem vulnerability scan

### 4. Publish Stage
- Publish build artifact for CD consumption
- Archive SAST reports

## CD Pipeline Structure (All Tools)

Every CD pipeline follows this structure:

### 1. Download Stage
- Download artifact from CI pipeline
- Verify artifact integrity

### 2. Deploy Stage
- Deploy to target environment
- Run smoke tests
- Verify deployment health

## YAML Coding Standards

All templates follow these standards:

- **Document start:** Every file begins with `---`
- **Indentation:** 2 spaces, no tabs
- **Naming:** snake_case for variables
- **Comments:** File header + complex block comments
- **Line length:** Max 120 characters
- **Strings:** Quote special characters (`:`, `@`, `#`, etc.)
- **Encoding:** UTF-8

## File Naming Convention

- **CI files:** `{language}-ci.yml` (e.g., `dotnet-ci.yml`)
- **CD files:** `{target}-cd.yml` (e.g., `webapp-cd.yml`)

## Usage Examples

### Azure DevOps .NET Web App Pipeline

**CI Pipeline:** `azure-devops/ci/dotnet-ci.yml`
- Builds .NET application
- Runs unit tests with VSTest
- Performs SAST scanning
- Publishes artifact as `{project-name}-drop`

**CD Pipeline:** `azure-devops/cd/webapp-cd.yml`
- Downloads artifact from CI
- Deploys to Azure Web App
- Runs smoke test on `/health` endpoint

### GitHub Actions Node.js Container Pipeline

**CI Workflow:** `github-actions/ci/node-ci.yml`
- Builds Node.js application
- Runs Jest tests
- Performs security scanning
- Publishes artifact

**CD Workflow:** `github-actions/cd/container-cd.yml`
- Downloads artifact from CI workflow
- Builds Docker image
- Pushes to container registry
- Deploys container

## Variables and Secrets

### Common Variables
```yaml
PROJECT_NAME: "$(Build.Repository.Name)"  # Azure DevOps
PROJECT_NAME: "${{ github.event.repository.name }}"  # GitHub Actions
PROJECT_NAME: "$CI_PROJECT_NAME"  # GitLab CI
PROJECT_NAME: "${env.JOB_NAME.split('/')[0]}"  # Jenkins
```

### Required Secrets
- `AZURE_CREDENTIALS` — Azure service principal
- `RESOURCE_GROUP` — Azure resource group
- `CONTAINER_REGISTRY` — Container registry URL
- `REGISTRY_USERNAME` / `REGISTRY_PASSWORD` — Registry credentials
- `VM_SSH_CONNECTION` — SSH connection for VM deployment

## AI Agent Usage

The `reference/ai-reference.yml` file contains:
- Complete YAML coding standards
- Mandatory CI/CD structure rules
- Language-specific requirements
- Deploy target specifications
- AI generation rules

AI agents should read this file before generating any YAML templates to ensure consistency and compliance.

## Key Features

✅ **Standardized Structure** — Same stages across all tools
✅ **Mandatory SAST** — Security scanning cannot be skipped
✅ **Tool-Specific Syntax** — Native YAML for each platform
✅ **Language Support** — .NET, Node.js, Python, Java
✅ **Multi-Target Deploy** — Web App, AKS, VM, Container
✅ **Enterprise Ready** — Proper error handling, health checks
✅ **YAML Compliant** — Follows coding standards and best practices

## Adding New Templates

### New Language
1. Create `{language}-ci.yml` in each tool's `ci/` folder
2. Follow the 4-stage structure: Build → Test → SAST → Publish
3. Use tool-specific syntax for language setup
4. Include proper test result publishing

### New Deploy Target
1. Create `{target}-cd.yml` in each tool's `cd/` folder
2. Follow the 2-stage structure: Download → Deploy
3. Include health checks and verification steps
4. Add proper error handling

### New CI/CD Tool
1. Create new folder: `{tool-name}/ci/` and `{tool-name}/cd/`
2. Implement same stage structure using tool's native syntax
3. Ensure SAST stage includes all three security tools
4. Maintain variable naming consistency

## Validation

All templates should pass:
- `yamllint` validation
- Tool-specific syntax validation
- SAST stage presence check
- Artifact naming consistency between CI and CD

## Best Practices

- Always use the reference file for AI generation
- Maintain consistent variable naming across tools
- Include proper error handling and health checks
- Use `continueOnError: true` for SAST tools
- Publish test results and SAST reports as artifacts
- Include smoke tests for web deployments
- Add rollout verification for Kubernetes deployments