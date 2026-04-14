# Royalty Pool Formula v0.1

A machine-readable specification for calculating royalty allocation from permission-aware trace events, resonance scoring, and internal accounting units.

This repository defines the **Royalty Pool Formula** as a structured, auditable specification using **JSON Schema**, **YAML examples**, and **GitHub Actions validation**.

It is designed as a minimal, extensible foundation for **permission → trace → resonance → allocation → recirculation** workflows.

---

## Overview

`Royalty Pool Formula v0.1` is a formal specification for calculating how value should be distributed from trace-based contribution events.

The core idea is simple:

- value enters the system as a **pool**
- trace-related events are evaluated through **permission**, **origin traceability**, **agency attribution**, and **resonance**
- the resulting scores are normalized into **allocation shares**
- distribution remains **auditable**, **machine-readable**, and **extensible**

This repository focuses on the **specification layer**, not on blockchain, payments, or financial settlement infrastructure.

---

## Core Concepts

The formula is built around the following flow:

1. **Permission**  
   Confirm whether a use is permitted, restricted, or prohibited.

2. **Trace**  
   Record relevant trace-linked events in a structured form.

3. **Resonance**  
   Compute contribution scores from similarity, confidence, decay, and policy-aware factors.

4. **Allocation**  
   Normalize contribution scores into proportional royalty shares.

5. **Recirculation**  
   Optionally return part of downstream value to upstream structures or origins.

---

## Repository Structure

```text
.
├─ schema/
│  └─ royalty-pool-formula-v0.1.schema.json
├─ examples/
│  └─ royalty-pool-formula-v0.1.sample.yaml
└─ .github/
   └─ workflows/
      └─ validate-specs.yml

Directory overview
schema/

JSON Schema files for machine-readable specification validation.

royalty-pool-formula-v0.1.schema.json
Defines the structural contract for the Royalty Pool Formula specification.
This schema is the canonical validation layer for required sections, variable definitions, formula containers, policy blocks, extensions, and sample structure.
examples/

Example documents that are expected to pass schema validation.

royalty-pool-formula-v0.1.sample.yaml
A minimal human-readable YAML example conforming to the schema.
This file demonstrates the intended document shape and serves as the primary validation target in CI.
.github/workflows/

Continuous Integration workflows for automatic validation.

validate-specs.yml
Runs schema validation against the sample YAML on push, pull_request, and manual dispatch.
This ensures that schema changes and example files remain consistent over time.
Design Intent

This repository is structured around three layers:

Specification layer — defined in schema/
The formal, machine-readable contract.
Example layer — defined in examples/
Human-readable sample documents that illustrate how the specification is used.
Validation layer — defined in .github/workflows/
Automated checks that verify examples remain compatible with the schema.
Why this structure

This layout keeps the repository easy to understand and maintain:

clear separation of concerns
human-readable examples
machine-verifiable contracts
CI-based consistency checks

It also makes future expansion straightforward, for example:

adding v0.2 or v1.0 schemas
adding multiple example documents
adding JSON samples alongside YAML samples
expanding validation workflows for additional spec files
Schema Usage

This repository provides a machine-readable schema and a sample YAML document for the Royalty Pool Formula specification.

Files
schema/royalty-pool-formula-v0.1.schema.json
examples/royalty-pool-formula-v0.1.sample.yaml
.github/workflows/validate-specs.yml
What this does
schema/royalty-pool-formula-v0.1.schema.json
JSON Schema that defines the document structure for Royalty Pool Formula v0.1
examples/royalty-pool-formula-v0.1.sample.yaml
A minimal sample document expected to pass schema validation
.github/workflows/validate-specs.yml
GitHub Actions workflow that automatically validates the sample YAML
Local validation
1. Install dependencies
python -m pip install --upgrade pip
python -m pip install jsonschema PyYAML
2. Validate the sample YAML against the schema
python - <<'PY'
import json
import yaml
from jsonschema import Draft202012Validator

schema_path = "schema/royalty-pool-formula-v0.1.schema.json"
sample_path = "examples/royalty-pool-formula-v0.1.sample.yaml"

with open(schema_path, "r", encoding="utf-8") as f:
    schema = json.load(f)

with open(sample_path, "r", encoding="utf-8") as f:
    sample = yaml.safe_load(f)

validator = Draft202012Validator(schema)
errors = sorted(validator.iter_errors(sample), key=lambda e: e.path)

if errors:
    for err in errors:
        path = ".".join(str(x) for x in err.path)
        print(f"[ERROR] path={path or '<root>'}")
        print(err.message)
        print("-" * 80)
    raise SystemExit(1)

print("Validation passed: royalty-pool-formula-v0.1.sample.yaml")
PY
Expected result
Validation passed: royalty-pool-formula-v0.1.sample.yaml
Validation scope

This schema validates the structural integrity of the specification, including:

top-level required sections
variable definition objects
formula expression containers
similarity weight defaults
policy rule structure
extension blocks
sample input/output structure
Notes
The schema validates document structure, not mathematical correctness.
Formula strings in expression fields are treated as human-readable symbolic expressions.
YAML is used for readability, while JSON Schema is used for deterministic validation.
The GitHub Actions workflow runs the same validation logic automatically on push, pull request, and manual dispatch.
Specification Summary

The formula is organized into the following major sections:

spec
Metadata for the specification itself
context
Accounting unit and processing pipeline
pool
Defines how the distributable royalty pool is calculated
resonance_score
Defines how contribution scores are computed
event_score
Defines the score of each relevant event
similarity
Defines weighted similarity composition across layers
allocation
Defines normalization and proportional distribution
event_weights
Default weights for event types
policy_rules
Permission, origin, and agency rules
extensions
Optional future blocks such as bias controls and upstream recirculation
validation
Human-readable validation constraints
sample
Example inputs and outputs
implementation_notes
Suggested storage and execution order
Formula Philosophy

This specification is not intended to be a generic engagement score.

It is designed to preserve the following principles:

permission first
trace-based allocation
origin traceability
agency attribution
value recirculation
auditability
internal accounting rather than speculative tokenization

In other words, the goal is not merely to reward activity, but to formalize how value can flow back through permitted and traceable contribution structures.

Recommended Workflow
Edit the schema in schema/
Update or add examples in examples/
Run local validation
Commit changes
Confirm GitHub Actions passes
Future Expansion

A natural future layout may look like this:

.
├─ schema/
│  ├─ royalty-pool-formula-v0.1.schema.json
│  └─ royalty-pool-formula-v0.2.schema.json
├─ examples/
│  ├─ royalty-pool-formula-v0.1.sample.yaml
│  ├─ royalty-pool-formula-v0.1.sample.json
│  └─ royalty-pool-formula-v0.2.sample.yaml
└─ .github/
   └─ workflows/
      └─ validate-specs.yml

Potential future additions:

semantic version evolution
JSON example support
stricter schema constraints
multiple policy profiles
additional recirculation models
allocation report schemas
ledger interoperability specifications
Status

Current status: Draft (v0.1.0)

This repository defines an initial machine-readable structure intended for iteration, validation, and future expansion.

License

Add your license information here.

Example:

This repository is released under the terms of the applicable project license.
See LICENSE for details.
Contributing

Contributions may include:

schema refinements
additional examples
validation improvements
documentation cleanup
future version drafting

A dedicated CONTRIBUTING.md can be added as the repository expands.

Start Here

For first-time readers:

Read the overview in this README
Open examples/royalty-pool-formula-v0.1.sample.yaml
Review schema/royalty-pool-formula-v0.1.schema.json
Run the validation command locally
Check .github/workflows/validate-specs.yml for CI behavior
