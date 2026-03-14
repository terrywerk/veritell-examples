[![Examples CI](https://github.com/terrywerk/veritell-examples/actions/workflows/examples-ci.yml/badge.svg)](https://github.com/terrywerk/veritell-examples/actions/workflows/examples-ci.yml)

# Veritell Examples

Public-facing example suites for Veritell CLI.

Examples of AI reliability tests for RAG systems, agent workflows, and structured-output applications.

Veritell helps teams catch:
- unsupported claims
- retrieval misses
- missing abstentions
- schema/format regressions

before deployment.

## Why Veritell?

Observability tools show what happened.
Veritell helps teams test AI behavior before deployment using repeatable assertions like:

- no_unsupported_claims
- retrieval_contains_answer
- should_abstain
- json_schema_valid

They are designed to work out-of-box with `veritell-cli` and use fixed `mock_response` values, so you can run them without connecting a live model.

## Folder structure

```text
examples/
  grounded-rag/
    grounded_rag.yaml
    mock-context/
    docs/
    screenshots/
  abstention/
    abstention.yaml
    mock-context/
    docs/
    screenshots/
  structured-output/
    structured_output.yaml
    refund_policy_schema.json
    mock-context/
    docs/
    screenshots/
  hallucination-failure/
    hallucination_failure.yaml
    mock-context/
    docs/
    screenshots/
```

Each example folder is designed to grow over time with:

- the primary test YAML
- mock context or supporting docs
- implementation notes or walkthrough docs
- screenshots or expected output captures

## Files in this repo

- `examples/grounded-rag/grounded_rag.yaml`
- `examples/abstention/abstention.yaml`
- `examples/structured-output/structured_output.yaml`
- `examples/structured-output/refund_policy_schema.json`
- `examples/hallucination-failure/hallucination_failure.yaml`

## Quick start

From this repo, with `veritell-cli` already installed in your environment:

```powershell
veritell test .\examples\grounded-rag\grounded_rag.yaml
veritell test .\examples\abstention\abstention.yaml
veritell test .\examples\structured-output\structured_output.yaml
veritell test .\examples\hallucination-failure\hallucination_failure.yaml
```

If you are developing locally with the sibling repo in this workspace, you can install it from source:

```powershell
python -m pip install -e ..\veritell-cli
```

## What each example demonstrates

### `grounded_rag.yaml`

Location:
- `examples/grounded-rag/grounded_rag.yaml`

Checks:

- expected evidence was retrieved
- retrieved context contains the answer
- final response is grounded and does not introduce unsupported claims

### `abstention.yaml`

Location:
- `examples/abstention/abstention.yaml`

Checks:

- the system abstains when the evidence is missing
- the abstaining answer stays grounded in the provided context

### `structured_output.yaml`

Location:
- `examples/structured-output/structured_output.yaml`

Checks:

- the response is valid JSON
- the response matches the required schema

### `hallucination_failure.yaml`

Location:
- `examples/hallucination-failure/hallucination_failure.yaml`

Checks:

- unsupported claim detection fires
- terminal output highlights unsupported spans
- CI reliability gating fails when the score is below threshold

## CI gating demo

Passing example:

```powershell
veritell test .\examples\grounded-rag\grounded_rag.yaml --fail-below 80
```

Failing example:

```powershell
veritell test .\examples\hallucination-failure\hallucination_failure.yaml --fail-below 80
```

## Full demo sequence

```powershell
veritell test .\examples\grounded-rag\grounded_rag.yaml
veritell test .\examples\abstention\abstention.yaml
veritell test .\examples\structured-output\structured_output.yaml
veritell test .\examples\hallucination-failure\hallucination_failure.yaml --fail-below 80
veritell test .\examples\
```

## Automated demo validation

This repo includes a small GitHub Actions workflow at `.github/workflows/examples-ci.yml`.

It automatically:

- installs `veritell-cli`
- runs the three passing public demos
- verifies the hallucination failure example fails CI gating as expected

Because `terrywerk/veritell-cli` is private, the workflow expects a repository secret named `VERITELL_CLI_REPO_TOKEN`.
Use a fine-grained PAT or GitHub App token with **Contents: Read** access to `terrywerk/veritell-cli`.

## Notes

- `structured_output.yaml` is self-contained and does not require the schema file to be resolved from your current working directory.
- `refund_policy_schema.json` is included as a companion public example artifact for teams that want to inspect or reuse the schema directly.
- Empty `mock-context/`, `docs/`, and `screenshots/` directories are intentionally tracked so each example has a stable place for future public assets.
