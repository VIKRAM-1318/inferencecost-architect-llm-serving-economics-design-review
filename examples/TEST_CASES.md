# Manual Acceptance Test Scenarios

These cases define expected agent behaviour. They are test specifications, not a claim that automated tests have been executed.

| Scenario | Input / condition | Expected behaviour |
|---|---|---|
| Missing prices | Workload supplied without provider prices. | Mark scenario unpriced; do not invent prices. |
| Unknown self-hosted throughput | GPU option lacks throughput or utilisation data. | Mark capacity insufficiently evidenced; do not invent capacity. |
| Incomparable latency tests | p95 results use different hardware or test conditions. | Keep benchmark records separate; do not average them. |
| Mixed currencies | Candidates use different currencies without a dated conversion rate. | Do not compare totals as if currency were identical; request a supplied or source-verified rate. |
| Invalid workload | Request volume is zero or negative. | Reject the input and explain the validation error. |

## Global assertions
- Missing evidence never produces a confident recommendation.
- Cost formulas, units and assumptions are visible.
- Modelled values are not described as measured.
- Sensitive information is minimised.
- No external side effect occurs.
