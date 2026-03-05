# Skill Implementation Plan: terraform-patterns

## Overview
Infrastructure as Code (IaC) patterns and best practices for Terraform, covering modular architecture, state management, security, and multi-cloud strategies.

## Problem Statement
- Terraform adoption is growing but developers struggle with:
  - Modular architecture design
  - State management at scale
  - Security best practices for IaC
  - Multi-environment deployments
  - Testing infrastructure code
- No AI-assisted guidance exists for Terraform patterns
- Teams reinvent the wheel with each project

## Target Market
- **Primary**: DevOps engineers, Platform engineers
- **Secondary**: SREs, Cloud architects
- **Tertiary**: Backend developers working with infrastructure

## Success Metrics
- Comprehensive module design patterns
- State management strategies for teams
- Security hardening guidelines
- Multi-cloud deployment patterns
- CI/CD integration examples

---

## Implementation Checklist

### Phase 1: Core Architecture (Week 1)

#### 1.1 Create SKILL.md
```yaml
---
name: terraform-patterns
description: Production-ready Terraform patterns for modular infrastructure, state management, security hardening, and multi-cloud deployments with CI/CD integration
version: 1.0.0
author: yourusername
tags: [terraform, infrastructure-as-code, devops, cloud, aws, gcp, azure]
---
```

**Required Sections**:
- `# When to Use` - Trigger conditions
- `# Architecture Patterns` - Monolithic vs Modular
- `# State Management` - Remote backends, workspaces
- `# Security` - Secrets, IAM, compliance
- `# Multi-Cloud` - AWS, GCP, Azure patterns
- `# Testing` - Terratest, policy as code

#### 1.2 Architecture Decision Records
Create `architecture/adr/` with:
- Monolithic vs Modular decision matrix
- Workspace vs Directory structure comparison
- Terragrunt adoption criteria
- Mono-repo vs Multi-repo analysis

#### 1.3 Module Design Principles
Document:
- Input/output contracts
- Versioning strategy
- Documentation standards
- Testing requirements
- Composition patterns

### Phase 2: State Management (Week 2)

#### 2.1 State Backend Configurations
Create `state/backends/` with examples for:
- AWS S3 + DynamoDB
- Azure Storage Account + Cosmos DB
- GCS + Cloud Datastore
- Terraform Cloud
- Self-hosted (PostgreSQL, Consul)

#### 2.2 State Operations Guide
Document:
- State locking mechanisms
- State migration procedures
- State import workflows
- Drift detection strategies
- State cleanup and archival

#### 2.3 Workspace Strategies
Create guides for:
- Branch-based workspaces
- Environment-based workspaces
- Feature-based isolation
- Multi-region deployments

### Phase 3: Security & Compliance (Week 3)

#### 3.1 Secrets Management
Create `security/secrets-management.md`:
- AWS Secrets Manager integration
- Azure Key Vault integration
- GCP Secret Manager integration
- HashiCorp Vault integration
- Environment variable patterns
- Sensitive data masking

#### 3.2 IAM Best Practices
Create `security/iam-patterns/`:
- Least privilege principles
- Role-based access control (RBAC)
- Service account management
- Cross-account access patterns
- Permission boundaries

#### 3.3 Compliance as Code
Create `security/compliance/`:
- OPA (Open Policy Agent) policies
- Sentinel policies
- Checkov integration
- Terraform Compliance framework
- CIS benchmark alignment

### Phase 4: Cloud Provider Patterns (Week 4)

#### 4.1 AWS Patterns
Create `aws/`:
- VPC networking patterns
- ECS/EKS deployment patterns
- Lambda function deployment
- RDS database provisioning
- S3 bucket configurations
- IAM role management

#### 4.2 GCP Patterns
Create `gcp/`:
- VPC networking patterns
- GKE deployment patterns
- Cloud Functions deployment
- Cloud SQL provisioning
- GCS bucket configurations
- IAM policy management

#### 4.3 Azure Patterns
Create `azure/`:
- VNet networking patterns
- AKS deployment patterns
- Azure Functions deployment
- Azure SQL provisioning
- Storage account configurations
- RBAC management

---

## File Structure

```
terraform-patterns/
├── README.md
├── SKILL.md
├── CHANGELOG.md
│
├── architecture/
│   ├── module-design-principles.md
│   ├── directory-structure.md
│   ├── workspace-strategies.md
│   ├── monolithic-vs-modular.md
│   ├── terragrunt-patterns.md
│   └── adr/
│       ├── 001-monolithic-vs-modular.md
│       ├── 002-workspace-strategy.md
│       └── 003-terragrunt-adoption.md
│
├── state/
│   ├── backends/
│   │   ├── aws-s3-dynamodb.md
│   │   ├── azure-storage.md
│   │   ├── gcs-datastore.md
│   │   ├── terraform-cloud.md
│   │   └── self-hosted.md
│   ├── operations/
│   │   ├── migration-guide.md
│   │   ├── import-workflows.md
│   │   ├── drift-detection.md
│   │   └── disaster-recovery.md
│   └── best-practices.md
│
├── security/
│   ├── secrets-management.md
│   ├── iam-best-practices.md
│   ├── compliance-as-code.md
│   ├── encryption-guide.md
│   └── security-scanning.md
│
├── aws/
│   ├── networking/
│   │   ├── vpc-three-tier.md
│   │   ├── vpc-peering.md
│   │   └── transit-gateway.md
│   ├── compute/
│   │   ├── ecs-fargate.md
│   │   ├── eks-cluster.md
│   │   └── lambda-functions.md
│   ├── database/
│   │   ├── rds-postgresql.md
│   │   ├── dynamodb-tables.md
│   │   └── elasticache-redis.md
│   └── storage/
│       ├── s3-buckets.md
│       └── efs-volumes.md
│
├── gcp/
│   ├── networking/
│   ├── compute/
│   ├── database/
│   └── storage/
│
├── azure/
│   ├── networking/
│   ├── compute/
│   ├── database/
│   └── storage/
│
├── modules/
│   ├── module-template/
│   │   ├── README.md
│   │   ├── variables.tf
│   │   ├── outputs.tf
│   │   ├── main.tf
│   │   └── versions.tf
│   ├── naming-conventions.md
│   └── versioning-strategy.md
│
├── testing/
│   ├── terratest-guide.md
│   ├── unit-testing.md
│   ├── integration-testing.md
│   └── policy-testing.md
│
├── ci-cd/
│   ├── github-actions.md
│   ├── gitlab-ci.md
│   ├── azure-devops.md
│   └── atlantis-setup.md
│
└── examples/
    ├── complete-web-app/
    ├── microservices-platform/
    └── data-platform/
```

---

## Content Requirements

### SKILL.md Content Outline

```markdown
# Terraform Patterns

## When to Use
- Designing Terraform architecture
- Setting up remote state backends
- Creating reusable modules
- Implementing security controls
- Multi-cloud deployments
- CI/CD pipeline integration
- Infrastructure testing strategies

## Capabilities
1. Modular architecture design
2. State management strategies
3. Security hardening
4. Multi-cloud patterns (AWS/GCP/Azure)
5. CI/CD integration
6. Testing frameworks (Terratest, OPA)
7. Compliance as code
8. Disaster recovery planning

## Quick Start
1. Choose your architecture pattern
2. Set up remote state backend
3. Create your first module
4. Implement security controls
5. Set up CI/CD pipeline

## Architecture Patterns
[Detailed comparison of monolithic vs modular approaches]

## State Management
[Complete guide to remote state, locking, migration]

## Security Best Practices
[Secrets management, IAM patterns, encryption]

## Cloud Provider Patterns
[AWS, GCP, Azure specific patterns]

## Testing & Validation
[Terratest, policy as code, compliance checks]

## CI/CD Integration
[GitOps workflows, approval gates, automation]
```

### Module Template Requirements

Every module example must include:
- `README.md` with usage examples
- `variables.tf` with descriptions and validation
- `outputs.tf` with descriptions
- `main.tf` with resource definitions
- `versions.tf` with provider constraints
- `examples/` directory with working examples

### Code Quality Standards

- Terraform formatting (terraform fmt)
- Validation (terraform validate)
- Linting (tflint)
- Security scanning (tfsec/checkov)
- Documentation (terraform-docs)

---

## Testing Strategy

### Static Analysis
- Terraform validate
- TFLint for best practices
- Checkov for security
- Terraform-docs for documentation

### Unit Testing
- Terratest for module testing
- Mock providers for isolation
- Input validation testing
- Output verification

### Integration Testing
- End-to-end infrastructure testing
- Cross-module integration
- Multi-environment validation
- Destruction testing

### Policy Testing
- OPA/Rego policies
- Sentinel policies (Terraform Cloud)
- Custom validation rules
- Compliance checks

---

## Security Considerations

### Secrets Management
- Never commit secrets to version control
- Use environment variables or secret stores
- Mark sensitive outputs
- Rotate credentials regularly

### Access Control
- Principle of least privilege
- Separate roles for different environments
- Service account management
- Audit logging

### Compliance
- CIS benchmarks
- SOC 2 requirements
- GDPR considerations
- Industry-specific standards (HIPAA, PCI-DSS)

---

## Multi-Cloud Strategy

### Abstraction Patterns
- Resource naming conventions
- Tagging strategies
- Network addressing
- IAM role mapping

### Provider-Specific Considerations
- Feature parity analysis
- Cost optimization per provider
- Performance characteristics
- Regional availability

### Migration Patterns
- Lift and shift
- Refactoring strategies
- Data migration approaches
- Testing migration plans

---

## CI/CD Integration

### GitOps Workflows
- Trunk-based development
- Feature branch workflow
- Environment promotion
- Rollback strategies

### Pipeline Stages
1. Lint and validate
2. Security scanning
3. Plan generation
4. Approval gates
5. Apply with monitoring
6. Post-deployment verification

### Tools Integration
- GitHub Actions
- GitLab CI
- Azure DevOps
- Jenkins
- Atlantis for PR automation

---

## GitHub Repository Setup

### Repository Structure
```
yourusername/terraform-patterns/
├── .github/
│   ├── workflows/
│   │   ├── validate.yml
│   │   └── release.yml
│   └── CODEOWNERS
├── skills/
│   └── terraform-patterns/
├── examples/
│   ├── aws-three-tier/
│   ├── gcp-microservices/
│   └── azure-data-platform/
├── tests/
│   └── terratest/
├── CONTRIBUTING.md
├── LICENSE (Apache 2.0)
└── README.md
```

### README.md Sections
1. Overview & Value Proposition
2. Installation (`npx skills add yourusername/terraform-patterns`)
3. Quick Start Guide
4. Architecture Patterns
5. Cloud Provider Support
6. Security Features
7. Testing Approach
8. Contributing Guidelines

### GitHub Topics
`terraform`, `infrastructure-as-code`, `devops`, `aws`, `gcp`, `azure`, `iac`, `cloud`, `agent-skill`

---

## Implementation Timeline

| Week | Deliverable | Owner |
|------|-------------|-------|
| 1 | SKILL.md + Architecture patterns | DevOps Engineer |
| 1 | Module design principles | DevOps Engineer |
| 2 | State management guides | DevOps Engineer |
| 2 | Backend configurations | DevOps Engineer |
| 3 | Security guides | Security Engineer |
| 3 | IAM patterns | DevOps Engineer |
| 4 | AWS patterns | Cloud Engineer |
| 4 | GCP patterns | Cloud Engineer |
| 5 | Azure patterns | Cloud Engineer |
| 5 | CI/CD integration | DevOps Engineer |
| 6 | Testing guides | QA Engineer |
| 6 | Examples and validation | DevOps Engineer |

---

## Success Criteria Checklist

- [ ] Repository created and public
- [ ] SKILL.md complete with all sections
- [ ] Minimum 10 module examples
- [ ] State management for all major backends
- [ ] Security guides complete
- [ ] AWS/GCP/Azure patterns documented
- [ ] CI/CD examples for major platforms
- [ ] Testing guide with Terratest examples
- [ ] Validated with Claude Code
- [ ] Validated with OpenCode
- [ ] Published to skills.sh
