Enterprise CI/CD Boilerplate Framework
 Overview

This repository provides a standardized, reusable, and enterprise-grade CI/CD boilerplate framework designed to:

Ensure consistent YAML generation
Enforce coding standards and best practices
Enable AI agent-driven pipeline generation
Support multi-runtime and multi-deployment targets
 Repository Structure
enterprise-cicd-boilerplate/
│
├── standards/
│   ├── yaml-standards.yml
│   ├── naming.yml
│   └── schema.yml
│
├── templates/
│   ├── ci/
│   │   ├── ci-base.yml
│   │   ├── ci-sast.yml
│   │   └── ci-publish.yml
│   │
│   ├── cd/
│   │   ├── cd-base.yml
│   │   └── cd-deploy.yml
│   │
│   └── common/
│       └── variables.yml
│
├── snippets/
│   ├── dotnet.yml
│   ├── node.yml
│   ├── python.yml
│   └── deploy.yml
│
├── pipelines/
│   ├── ci.yml
│   └── cd.yml
│
├── validation/
│   ├── .yamllint.yml
│   └── validate.yml
│
└── agent/
    ├── prompt.txt
    └── mapping.yml
 YAML Standards
Use 2-space indentation
No tabs allowed
Use --- at the beginning of files
Max line length: 120 characters
Use camelCase naming
Add comments for clarity
Example
---
projectName: "sampleApp"
buildConfiguration: "Release"
 CI Pipeline Design
Stages Included
Build
Test
SAST (Security Scans)
Publish Artifact
CI Base Template
---
parameters:
  buildSteps: []
  testSteps: []
  artifactName: "drop"

stages:
  - stage: Build
    jobs:
      - job: BuildJob
        steps:
          - checkout: self
          - ${{ each step in parameters.buildSteps }}:
              - ${{ step }}

  - stage: Test
    dependsOn: Build
    jobs:
      - job: TestJob
        steps:
          - ${{ each step in parameters.testSteps }}:
              - ${{ step }}
SAST Stage

Includes:

Gitleaks → Secret scanning
Semgrep → Static code analysis
Trivy → Vulnerability scanning
- stage: SAST
  jobs:
    - job: SecurityJob
      steps:
        - script: "gitleaks detect --source ."
        - script: "semgrep scan --config auto"
        - script: "trivy fs ."
Artifact Publishing
- stage: Publish
  jobs:
    - job: PublishJob
      steps:
        - task: PublishBuildArtifacts@1
          inputs:
            artifactName: "drop"
 CD Pipeline Design
Responsibilities
Download artifact from CI
Deploy to target environment
CD Base Template
---
parameters:
  environment: ""
  artifactName: "drop"
  deploySteps: []

stages:
  - stage: Deploy_${{ parameters.environment }}
    jobs:
      - job: DeployJob
        steps:
          - task: DownloadBuildArtifacts@0
            inputs:
              artifactName: ${{ parameters.artifactName }}

          - ${{ each step in parameters.deploySteps }}:
              - ${{ step }}
 Deployment Targets
Supported Environments
Azure Web App
- task: AzureWebApp@1
  inputs:
    appName: "$(projectName)"
AKS
- script: "kubectl apply -f deployment.yaml"
Virtual Machine
- script: "scp artifact.zip user@vm:/app/"
- script: "ssh user@vm 'deploy.sh'"
Containers
- script: "docker build -t app:latest ."
- script: "docker push app:latest"
 Runtime Snippets
Example: .NET
dotnet:
  build:
    - script: "dotnet restore"
    - script: "dotnet build --configuration Release"

  test:
    - script: "dotnet test --no-build"
 YAML Validation
yamllint Configuration
rules:
  indentation:
    spaces: 2
  line-length:
    max: 120
  document-start:
    present: true
Validation Pipeline
steps:
  - script: yamllint .
    displayName: "Validate YAML"
 AI Agent Integration
Agent Responsibilities
Load templates
Inject snippets
Maintain consistency
Generate CI & CD YAML
Agent Prompt
You are an enterprise CI/CD YAML generator.

RULES:
- Use only templates
- Do not create new structure
- Always include SAST
- Always publish artifact in CI
- Always download artifact in CD
- Follow YAML standards
Mapping File
runtime:
  dotnet:
    build: dotnet.build
    test: dotnet.test

deploy:
  webapp: deploy.webapp
  aks: deploy.aks
  vm: deploy.vm
  container: deploy.container
 Agent Workflow
User Input
   ↓
Load Templates
   ↓
Inject Snippets
   ↓
Apply Standards
   ↓
Validate YAML
   ↓
Generate CI + CD
 Key Rules
CI must include:
Build → Test → SAST → Publish
CD must:
Download artifact
Deploy using snippets
Artifact name must match between CI & CD
No hardcoding allowed
 Final Outcome

 Standardized CI/CD pipelines
 Secure by default (SAST integrated)
 Multi-environment deployment support
 AI-driven, deterministic YAML generation
 Fully compliant with YAML best practices

You are an Enterprise CI/CD YAML Generator.

STRICT RULES:
- You MUST follow the provided template structure.
- You MUST NOT invent new structure.
- You MUST only fill placeholders.
- You MUST use predefined snippets.
- Output must be deterministic and consistent.

DO NOT:
- Add extra stages
- Change naming conventions
- Add random steps

ALWAYS:
- Use Build → Test → Deploy stages
- Use parameters
- Follow enterprise standards