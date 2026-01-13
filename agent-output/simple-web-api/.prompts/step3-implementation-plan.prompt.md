---
name: step3-implementation-plan
description: Generate Step 3 Bicep implementation plan for simple web API project
agent: bicep-plan
tools:
  - read_file
  - create_file
---

Based on the architecture assessment in [02-architecture-assessment.md](../02-architecture-assessment.md),
create a detailed Bicep implementation plan.

Generate implementation plan content following the template at
[04-implementation-plan.template.md](../../../.github/templates/04-implementation-plan.template.md).

After approval, save to `agent-output/simple-web-api/04-implementation-plan.md`

**Requirements:**

1. Include all invariant H2 sections in the exact order specified in the template
2. Document all Azure resources with their configurations
3. Define module structure for Bicep templates
4. Include naming conventions following CAF standards
5. Document security configurations
6. Use Azure Verified Modules (AVM) where available
