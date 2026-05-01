# Obolus (Pipedream Integration)

Obolus is a cross-country tax and net income calculation API.

This initial integration includes two actions:

- `Compare Salary Across Countries`
- `Calculate Net Salary`

Supported countries: `DE`, `AT`, `US`, `CH`, `CA`, `AU`, `UK`, `IE`

## Inputs

- common fields are available directly in the action UI
- advanced fields are grouped behind `Show Advanced Inputs`
- JSON override fields remain available for edge cases and forward compatibility
- `/berechne` supports one-person and two-person scenarios

Direct fields cover common use cases. JSON overrides exist for forward compatibility and niche cases.

### Germany payroll defaults

For standard German employees, the `Calculate Net Salary` action uses the readable Obolus alias fields:

- `standard_german_employee: true`
- `de_pension_insurance: "statutory"`
- `de_health_insurance: "statutory"`
- `de_health_extra_contribution_percent: 2.5`

The extra health contribution is a literal percent value. Use `2.5` for 2.5%, not `25`, `250`, basis points, tenths, or cents.

Legacy backend fields remain available under advanced inputs for compatibility, but should only be used for edge cases:

- `gesetzliche_RV`: `0` means standard statutory pension/unemployment applies; `1` disables that handling for exempt cases.
- `gesetzlicheKvPvStatus`: `0` means statutory GKV/PV; `1` means private health insurance.
- `KV_Art`: `0` means statutory GKV; `1` means private PKV.
- `KVZ`: literal percent points such as `2.5`, not basis points.

For country-specific input and output parameter details, the Obolus `/developers` page can serve as the knowledge base:

https://www.obolusfinanz.de/en/developers

## Outputs

Both actions return the full Obolus API response object, so downstream Pipedream workflow steps can bind directly to nested fields.

Typical `/berechne` output fields:

- `person1`
- `person2`
- `gesamt`
- `faktor`
- `source_url`
- `visual_report`
- `localized_cta`

Typical `/taxcompare` output fields:

- `results`
- `comparison_basis`
- `gross_inputs`

## Links

Website:
https://www.obolusfinanz.de/en

Developer documentation:
https://www.obolusfinanz.de/en/developers

OpenAPI contract:
https://www.obolusfinanz.de/api/openapi

This initial integration targets the currently published public API surface.
