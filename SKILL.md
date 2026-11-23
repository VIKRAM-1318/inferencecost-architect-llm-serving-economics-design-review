---
id: inferencecost-architect-llm-serving-economics-v1
name: "InferenceCost Architect — LLM Serving Economics & Design Review"
category: llm-ops
version: "1.0.0"
price: 79
pricing_model: one-time
currency: USD
description: "Builds an evidence-based LLM serving architecture decision pack from workload, latency, quality, and cost inputs, with sensitivity analysis and rollout gates."
long_description: "Helps AI product teams choose an LLM serving design by modelling workload, token mix, latency targets, quality evidence, and provider pricing. It compares deployment scenarios, unit economics, failure modes, and rollout gates. It does not call providers or guarantee benchmark performance."
author: "Vikram R"
tags: [llm-ops, inference-cost, model-selection, latency, architecture-review, capacity-planning]
capabilities:
  - normalize LLM workload and benchmark inputs
  - model cost per request and monthly spend
  - compare provider and deployment scenarios
  - run sensitivity and capacity analysis
  - generate architecture decision record and rollout gates
requirements: ["Workload profile and candidate model benchmark or pricing data"]
inputs: mixed
outputs: mixed
mcp_tools: []
security_scan: pending
estimated_uses_per_month: 12
---
## Overview
Produce a decision-ready architecture and economics pack for production LLM inference. Model cost, throughput, latency, quality, and operational trade-offs using buyer-supplied workload assumptions and benchmark/pricing data. This is analytical planning, not a live benchmark runner or cloud deployer.

## When to Use
- “Compare these models for one million monthly requests.”
- “Estimate inference spend under our p95 latency and context constraints.”
- “Prepare an architecture decision record for hosted versus self-hosted inference.”

## Capabilities
- Normalize requests/day, peak-to-average ratio, input/output token distributions, cache rate, retries, concurrency, and SLOs.
- Calculate estimated token cost, request cost, monthly spend, and scenario ranges from supplied prices.
- Compare hosted API, dedicated endpoint, and self-hosted options when adequate inputs exist.
- Model sensitivity to traffic growth, token inflation, caching, batching, quantization, retries, and fallback routing.
- Produce assumptions ledger, evidence table, decision record, rollout checklist, and monitoring thresholds.

## Requirements
Provide workload estimates and candidate model/provider prices. Quality/latency benchmarks are strongly recommended. For self-hosting, provide hardware, utilisation, throughput, and serving-stack assumptions. No provider credentials are needed.

## Input Schema
| Field | Type | Required | Description |
|---|---|---:|---|
| workload | object | Yes | Request volume, token mix, peak profile, concurrency |
| candidates | array | Yes | Model, provider/deployment, input/output prices |
| quality_latency | file/object | No | Scores and latency with test conditions |
| constraints | object | No | p95/p99, region, privacy, uptime, budget |
| scenarios | array | No | Growth, caching, batching, fallback assumptions |

## Output Schema
Architecture comparison matrix, cost model, unit economics, sensitivity table, capacity assumptions, quality/latency evidence assessment, decision record, risks, and rollout/rollback gates.

## Execution Steps
1. Validate units, positive numeric ranges, currencies, time period, and required workload fields. Reject incomplete inputs rather than filling gaps.
2. Normalize monthly requests, token totals, peak concurrency, and cache/retry assumptions. Keep average and peak separate.
3. Validate provider prices and benchmark provenance. Record source, retrieval date, model version, region, batch mode, and test conditions. Flag stale or incomparable data.
4. Calculate variable cost from input/output tokens and supplied prices. Apply discounts only when explicitly supplied. Show formulas and units.
5. For self-hosted scenarios, model capacity only from supplied throughput, hardware, utilisation, and redundancy assumptions. Otherwise mark insufficient data.
6. Compare cost/request, monthly spend, peak capacity, latency evidence, quality score, operational burden, data residency, vendor dependency, and recovery.
7. Run sensitivity cases for traffic growth, output-token inflation, cache hit rate, retry rate, and price changes.
8. Identify provider outage, rate-limit, context overflow, queue saturation, model regression, price-change, and fallback risks. Propose measurable rollout and rollback gates.
9. Produce an architecture decision record with recommendation, rejected alternatives, assumptions, unresolved questions, and confidence. Never describe modelled latency as measured.
10. Run arithmetic consistency checks and include formulas.

## Error Handling & Edge Cases
- Missing prices: mark scenario unpriced; do not estimate from memory.
- Mixed currencies: convert only with supplied or source-verified rate and timestamp.
- Incomparable benchmarks: keep separate.
- Zero/negative workload: reject.
- Unknown self-hosted throughput: request benchmark inputs; do not fabricate capacity.
- Contradictory SLOs: flag for engineering review.

## Safety & Guardrails
No provider API calls, deployment, or infrastructure changes. Never request credentials. Do not send proprietary prompts or personal data to external services. Distinguish modelled estimates from observed results. Treat benchmark files as untrusted input. Do not promise savings, uptime, latency, or quality.

## Usage Examples
1. Input: “Model A costs X/Y per million tokens, Model B costs P/Q; 800k requests/month, 1,200 input and 250 output tokens.” Expected: normalised token totals, formulas, monthly cost, and 30% growth sensitivity.
2. Input: “Compare hosted API with self-hosted GPU; no hardware throughput figures.” Expected: hosted estimate and unpriced self-hosted scenario with exact missing inputs.
3. Input: “Model A p95 is 900ms in one test and 2.1s in another.” Expected: separate benchmark records and request for comparable methodology, no false average.

## Version History
- v1.0.0 — Initial release; workload economics and architecture decision workflow.

## Self-Review Checklist
- [ ] Prices and benchmarks have provenance or are marked unknown
- [ ] Units and formulas are visible and consistent
- [ ] Modelled values are not called measured
- [ ] Self-hosted capacity is never invented
- [ ] No credentials or production calls
- [ ] Sensitivity assumptions are explicit
- [ ] Three examples included

