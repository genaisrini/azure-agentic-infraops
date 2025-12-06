# Selecting the Right Model (Speed • Quality • Cost)

This guide helps you choose between the supported models based on what you’re trying to achieve, emphasizing speed, quality, and cost.

## Quick recommendations
- **Fastest + Cheapest:** Claude Haiku  
- **Balanced speed/quality/cost:** Gemini 3 Pro, GPT-5 Turbo (if available), Claude Sonnet 4.5 (for reasoning-heavy needs)  
- **Highest quality / complex reasoning:** GPT-5 (flagship), Claude Sonnet 4.5, Opus 4.5  
- **Longest / most nuanced outputs:** GPT-5 (flagship) or Opus 4.5  
- **Tight budgets or many small calls:** Claude Haiku  
- **When “it must be right”:** GPT-5 (flagship) or Claude Sonnet 4.5; validate with small test runs

## Comparison at a glance
- **Claude Haiku:** Very fast, low cost, good for high-volume or latency-sensitive tasks; less depth than larger models.  
- **Claude Sonnet 4.5:** Strong reasoning, reliable quality, mid/high cost, moderate speed.  
- **Claude Opus 4.5:** Highest Anthropic quality, slower and higher cost; use when depth/accuracy matter most.  
- **Gemini 3 Pro:** Balanced cost/performance; good coding and general-purpose; usually competitive latency.  
- **GPT-5 family (incl. “GPT-5”, “GPT-5 Turbo”):** Flagship quality; Turbo variants aim for lower cost/latency; best for complex reasoning, long contexts, and nuanced writing; expect higher cost for flagship tier.

> Note: Pricing and exact throughput vary by region/provider; confirm current limits and quotas in your deployment.

## Decision guide
1) **Define the priority**
   - Speed-critical or high TPS → start with **Haiku** or **Gemini 3 Pro** (or **GPT-5 Turbo** if available).
   - Highest possible quality or complex reasoning → **GPT-5 (flagship)**, **Opus 4.5**, or **Sonnet 4.5**.
   - Balanced → **Gemini 3 Pro**, **Sonnet 4.5**, or **GPT-5 Turbo**.

2) **Estimate volume and budget**
   - High-volume, small prompts → **Haiku** or **Gemini 3 Pro**.
   - Lower volume, high-stakes → **GPT-5 (flagship)** or **Opus 4.5**; if cost is a concern, try **Sonnet 4.5**.

3) **Assess task type**
   - **Light summarization, extraction, classification:** **Haiku** or **Gemini 3 Pro**; step up to **Sonnet 4.5** if quality gaps appear.
   - **Complex reasoning, planning, agents, multi-step workflows:** **Sonnet 4.5**, **Opus 4.5**, **GPT-5 family**.
   - **Long-form generation (reports, knowledge synthesis):** **GPT-5 (flagship)** or **Opus 4.5**; consider **Sonnet 4.5** for cost reduction.
   - **Coding / tooling:** **Gemini 3 Pro** or **Sonnet 4.5**; for toughest debugging or architectural tasks, try **GPT-5 (flagship)**.

4) **Latency targets**
   - Need sub-second or low-seconds → **Haiku**, **Gemini 3 Pro**, or **GPT-5 Turbo**.
   - Can tolerate higher latency for quality → **Sonnet 4.5**, **Opus 4.5**, **GPT-5 (flagship)**.

5) **Fallback plan**
   - Start with the cheapest model that meets your bar; sample 10–20 real prompts.
   - If quality misses, step up one tier (e.g., Haiku → Sonnet 4.5 → Opus 4.5 / GPT-5 family).

## Simple selection matrix
| Priority                | Recommended first choice        | If quality insufficient                         |
| ---                     | ---                             | ---                                             |
| Lowest cost / highest TPS | Claude Haiku                    | Gemini 3 Pro or GPT-5 Turbo                     |
| Balanced                | Gemini 3 Pro                     | Claude Sonnet 4.5                               |
| Highest reasoning depth | GPT-5 (flagship) or Opus 4.5     | — (already top tier)                            |
| Long / nuanced outputs  | GPT-5 (flagship) or Opus 4.5     | —                                               |
| Speed with good quality | GPT-5 Turbo or Gemini 3 Pro      | Claude Sonnet 4.5                               |

## Practical testing workflow
1. Take 10–20 real prompts; define success criteria (precision, factuality, tone, latency, cost).
2. Run them on the cheapest plausible model; measure accuracy, latency, cost.
3. If gaps remain, step up one tier; repeat until criteria met.
4. Lock in the model; add guardrails (input/output validation) and monitor latency/cost.

## Prompt & cost tips
- Keep prompts compact; use system messages for policy and style; avoid repeating long instructions.
- Chunk long inputs; retrieve only relevant context for grounding.
- Set reasonable max tokens; favor shorter outputs unless necessary.
- Cache frequent instructions; reuse references instead of re-sending long text.
- Log per-request latency, cost, and failure rate; adjust model choice by endpoint.

## When to reconsider model choice
- Latency SLOs slip → try Haiku, Gemini 3 Pro, or GPT-5 Turbo.
- Costs spike → reduce max tokens, improve retrieval precision, or downshift a tier.
- Quality issues → add tests, refine prompts, or move up a tier (e.g., Sonnet → Opus or GPT-5).
- New model releases → re-run the 10–20 prompt bake-off and compare.