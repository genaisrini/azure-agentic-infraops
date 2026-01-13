---
name: step2-architecture
description: Generate Step 2 architecture assessment for simple web API project
agent: azure-principal-architect
tools:
  - read_file
  - create_file
  - mcp_azure_mcp_cloudarchitect
  - mcp_azure-pricing_get_customer_discount
---

Review the requirements in [01-requirements.md](../01-requirements.md) and create a comprehensive
WAF assessment.

Generate architecture assessment content following the template at
[02-architecture-assessment.template.md](../../../.github/templates/02-architecture-assessment.template.md).

After approval, save to `agent-output/simple-web-api/02-architecture-assessment.md`

**Requirements:**

1. Include all invariant H2 sections in the exact order specified in the template
2. Provide WAF scores for all 5 pillars (Security, Reliability, Performance, Cost, Operations)
3. Include cost estimates using Azure Pricing MCP tools
4. Recommend appropriate SKUs for each service
5. Document any trade-offs made
