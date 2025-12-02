---
description: "Standards for Azure cost estimate documentation with architecture and business context"
applyTo: "**/docs/*-cost-estimate.md"
---

# Azure Cost Estimate Documentation Standards

Guidelines for creating comprehensive Azure cost estimate documents that include architecture context, business justification, and visual diagrams. These documents serve as financial planning artifacts for Azure infrastructure projects.

## Document Purpose

Cost estimate documents should provide:

- **Financial clarity** for stakeholders and budget approvals
- **Architecture context** linking costs to design decisions
- **Business justification** connecting technical choices to outcomes
- **Optimization guidance** for reducing costs without sacrificing quality

## Required Sections

### 1. Header Block

Include metadata at the top of every cost estimate:

```markdown
# Azure Cost Estimate: {Project Name}

**Generated**: {YYYY-MM-DD}
**Region**: {primary-region} ({location-name})
**Environment**: {Production|Staging|Development}
**MCP Tools Used**: {list of azure-pricing/\* tools used}
**Architecture Reference**: {link to WAF assessment or architecture doc}
```

### 2. Executive Summary

Provide a quick overview for stakeholders:

```markdown
## Summary

| Metric           | Value             |
| ---------------- | ----------------- |
| Monthly Estimate | ${min} - ${max}   |
| Annual Estimate  | ${min} - ${max}   |
| Primary Region   | {region}          |
| Pricing Type     | List Price (PAYG) |
| WAF Score        | {X.X}/10          |

### Business Context

{2-3 sentences explaining what this infrastructure supports and why these
investments are necessary. Link costs to business outcomes.}
```

### 3. Architecture Overview

Include a visual diagram and brief description:

```markdown
## Architecture Overview

### Cost Distribution

​`mermaid
%%{init: {'theme':'neutral'}}%%
pie showData
    title Monthly Cost Distribution
    "Compute" : 535
    "Data Services" : 461
    "Messaging" : 200
    "Networking" : 145
​`

### Key Design Decisions Affecting Cost

| Decision          | Cost Impact | Business Rationale       |
| ----------------- | ----------- | ------------------------ |
| Zone redundancy   | +$X/month   | 99.9% SLA requirement    |
| Premium SKUs      | +$X/month   | Performance requirements |
| Private endpoints | +$X/month   | Security/compliance      |
```

### 4. Detailed Cost Breakdown

Organize costs by category with clear subtotals:

```markdown
## Detailed Cost Breakdown

### Compute Services

| Resource | SKU   | Qty | $/Hour | $/Month | Notes     |
| -------- | ----- | --- | ------ | ------- | --------- |
| {name}   | {sku} | {n} | ${x}   | ${y}    | {context} |

**Compute Subtotal**: ~${total}/month
```

**Required categories:**

- Compute Services
- Data Services
- Networking & Edge
- Security & Management
- (Optional) Messaging & Integration

### 5. Regional Analysis

Compare costs across relevant regions:

```markdown
## Regional Comparison

| Region    | Monthly Cost | vs. Primary | Data Residency |
| --------- | ------------ | ----------- | -------------- |
| {region1} | ${x}         | Baseline    | {compliance}   |
| {region2} | ${y}         | +X%         | {compliance}   |
```

### 6. Savings Opportunities

Document reservation and savings plan options:

```markdown
## Savings Plans & Reserved Instances

### {Resource Name}

| Commitment    | Hourly Rate | Monthly Cost | Annual Savings |
| ------------- | ----------- | ------------ | -------------- |
| Pay-as-you-go | ${x}        | ${y}         | -              |
| 1-Year        | ${x}        | ${y}         | ${z} (X%)      |
| 3-Year        | ${x}        | ${y}         | ${z} (X%)      |
```

### 7. Environment Comparison

Show costs across environments:

```markdown
## Environment Cost Comparison

| Environment | Monthly Cost | Notes                        |
| ----------- | ------------ | ---------------------------- |
| Production  | ${x}         | Full SKUs, redundancy        |
| Staging     | ${y}         | Same SKUs, reduced instances |
| Development | ${z}         | Basic SKUs, no redundancy    |

**Total for all environments**: ~${total}/month
```

### 8. Assumptions & References

Document pricing assumptions and link to sources:

```markdown
## Assumptions

- Usage: 730 hours/month (24×7 operation)
- Data transfer: {estimate}
- Pricing: Azure retail list prices (pay-as-you-go)
- Region: {region} ({compliance notes})
- Prices queried: {date} via Azure Pricing MCP

## Pricing Data Accuracy

> **📊 Data Source**: All prices are queried in real-time from the
> [Azure Retail Prices API](https://learn.microsoft.com/en-us/rest/api/cost-management/retail-prices/azure-retail-prices),
> Microsoft's official public pricing endpoint.
>
> **What's included**: Retail list prices (pay-as-you-go), Savings Plan pricing
> (1-year and 3-year), and Spot pricing where available.
>
> **What's NOT included**: Enterprise Agreement (EA) discounts, CSP partner pricing,
> negotiated contract rates, or Azure Hybrid Benefit savings. For official quotes,
> verify with the [Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/)
> or your Microsoft account team.

## References

- [Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/)
- [WAF Assessment]({link})
- [Architecture Diagram]({link})
```

## Best Practices

### DO

- Use real-time pricing from Azure Pricing MCP tools
- Show list prices (PAYG) as the baseline
- Include savings plan options for significant resources
- Link costs to architecture decisions
- Provide business context for premium SKU choices
- Update estimates when architecture changes

### DON'T

- Include customer-specific discounts (these vary by agreement)
- Use outdated pricing data (re-query before publishing)
- Omit assumptions about usage patterns
- Forget to include all environments (dev/staging/prod)
- Skip the regional comparison for EU/compliance scenarios

## Validation Checklist

Before finalizing a cost estimate document:

- [ ] All prices queried via Azure Pricing MCP (document date)
- [ ] Subtotals match category totals
- [ ] Total matches sum of subtotals
- [ ] Architecture diagram or cost distribution chart included
- [ ] Business context provided
- [ ] Savings opportunities documented
- [ ] Regional alternatives analyzed
- [ ] All environments estimated
- [ ] Assumptions clearly stated
- [ ] References linked (WAF assessment, architecture docs)

## File Naming Convention

Use the pattern: `{project-name}-cost-estimate.md`

Examples:

- `ecommerce-cost-estimate.md`
- `patient-portal-cost-estimate.md`
- `data-platform-cost-estimate.md`

Place in `docs/` directory alongside other project documentation.
