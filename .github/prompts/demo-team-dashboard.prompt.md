---
description: 'Demo scenario: Internal team dashboard with Azure Static Web Apps'
agent: 'project-planner'
tools:
  - createFile
  - editFiles
---

# Demo: Team Dashboard Requirements

Pre-populated requirements for a 30-minute live demo of the full 7-step workflow.

## Project Overview

**Project Name**: team-dashboard
**Project Type**: Web App
**Target Environment**: prod
**Timeline**: 2 weeks

### Business Context

Internal team dashboard for displaying project metrics, team availability,
and sprint progress. Used by a 50-person engineering department to track
daily standups and project health.

### Stakeholders

| Role           | Name/Team       | Responsibility         |
| -------------- | --------------- | ---------------------- |
| Business Owner | Engineering VP  | Approves requirements  |
| Technical Lead | Platform Team   | Architecture decisions |
| Operations     | DevOps Team     | Day-2 support          |
| Security       | InfoSec         | Compliance sign-off    |

---

## Functional Requirements

### Core Capabilities

1. Display team member availability (in-office, remote, PTO)
2. Show sprint burndown charts from Azure DevOps
3. Display key project metrics (build status, test coverage)
4. Support dark/light theme toggle

### User Types & Load

| User Type   | Expected Count | Peak Concurrent | Geographic Region |
| ----------- | -------------- | --------------- | ----------------- |
| Engineers   | 50             | 30              | Europe            |
| Managers    | 10             | 5               | Europe            |

### Integration Requirements

| System       | Integration Type | Direction | Protocol |
| ------------ | ---------------- | --------- | -------- |
| Azure DevOps | API              | Inbound   | REST     |
| MS Graph     | API              | Inbound   | REST     |

### Data Requirements

| Data Type       | Volume | Retention | Sensitivity |
| --------------- | ------ | --------- | ----------- |
| User profiles   | 1 MB   | Ongoing   | Internal    |
| Sprint metrics  | 10 MB  | 90 days   | Internal    |
| Availability    | 1 MB   | 7 days    | Internal    |

---

## Non-Functional Requirements (NFRs)

### Availability & Reliability

| Requirement        | Target   | Notes                    |
| ------------------ | -------- | ------------------------ |
| **SLA**            | 99.9%    | Business hours critical  |
| **RTO**            | 4 hours  | Acceptable for internal  |
| **RPO**            | 24 hours | Daily backup sufficient  |
| **Maintenance**    | Weekends | Preferred update window  |

### Performance

| Metric               | Target  | Notes              |
| -------------------- | ------- | ------------------ |
| **Response Time**    | < 500ms | Dashboard load     |
| **Concurrent Users** | 30      | Peak during standup|

### Scalability

| Dimension    | Current | 12-Month | Notes            |
| ------------ | ------- | -------- | ---------------- |
| Users        | 60      | 100      | Team growth      |
| Data Volume  | 12 MB   | 50 MB    | More metrics     |

---

## Compliance & Security

### Regulatory Requirements

- [x] **None** - Internal tool, no external data

### Data Residency

| Requirement          | Details        |
| -------------------- | -------------- |
| **Primary Region**   | swedencentral  |
| **Data Sovereignty** | EU only        |

### Security Requirements

| Control              | Requirement              |
| -------------------- | ------------------------ |
| **Authentication**   | Azure AD (SSO)           |
| **Authorization**    | Azure AD groups          |
| **Encryption**       | Platform-managed         |
| **Network**          | Public (internal users)  |

---

## Cost Constraints

### Budget

| Period        | Budget | Currency |
| ------------- | ------ | -------- |
| **Monthly**   | $50    | USD      |
| **Annual**    | $600   | USD      |

### Cost Optimization Priorities

| Priority                 | Rank |
| ------------------------ | ---- |
| Minimize monthly spend   | 1    |
| Reduce operational cost  | 2    |

---

## Operational Requirements

### Monitoring & Observability

| Capability     | Requirement       |
| -------------- | ----------------- |
| **Logging**    | Application Logs  |
| **Metrics**    | Platform metrics  |
| **Alerting**   | Email on errors   |

### Support Model

| Aspect            | Requirement    |
| ----------------- | -------------- |
| **Support Hours** | Business hours |
| **Response Time** | P1: 4 hours    |

---

## Regional Preferences

**Primary Region**: `swedencentral`
**Secondary Region**: N/A (single region sufficient)

---

## Demo Workflow Script

### Phase 1: Requirements (5 min)

```text
Invoke: @project-planner
Prompt: "Create requirements for team-dashboard using this specification"
Output: agent-output/team-dashboard/01-requirements.md
```

### Phase 2: Architecture (5 min)

```text
Invoke: @azure-principal-architect
Prompt: "Assess the team-dashboard requirements"
Output: agent-output/team-dashboard/02-architecture-assessment.md
```

### Phase 3: Design Artifacts (3 min)

```text
Invoke: @diagram-generator
Prompt: "Create architecture diagram for team-dashboard"
Output: agent-output/team-dashboard/03-des-diagram.py
```

### Phase 4: Implementation Plan (5 min)

```text
Invoke: @bicep-plan
Prompt: "Create implementation plan for team-dashboard"
Output: agent-output/team-dashboard/04-implementation-plan.md
```

### Phase 5: Bicep Implementation (7 min)

```text
Invoke: @bicep-implement
Prompt: "Implement the team-dashboard infrastructure"
Output: infra/bicep/team-dashboard/
```

### Phase 6: Deployment (3 min)

```text
Invoke: @deploy
Prompt: "Deploy team-dashboard to Azure"
Output: agent-output/team-dashboard/06-deployment-summary.md
```

### Phase 7: Documentation (2 min)

```text
Invoke: @workload-documentation-generator
Prompt: "Generate documentation for team-dashboard"
Output: agent-output/team-dashboard/07-*.md
```

---

## Expected Architecture

Simple, cost-effective solution:

- **Azure Static Web Apps** (Free tier) - React frontend
- **Azure SQL Database** (Basic) - Optional, only if needed
- **Azure AD** - Authentication (existing)
- **Application Insights** - Monitoring

Estimated cost: ~$5-15/month

---

## Demo Tips

1. **Skip Azure login** - Pre-authenticate before demo
2. **Pre-create resource group** - `rg-team-dashboard-demo`
3. **Have Azure portal open** - Show resources after deployment
4. **Prepare rollback** - `git stash` if demo goes wrong
