[![Examples CI](https://github.com/terrywerk/veritell-examples/actions/workflows/examples-ci.yml/badge.svg)](https://github.com/terrywerk/veritell-examples/actions/workflows/examples-ci.yml)

# Veritell Examples

Public-facing example suites for Veritell CLI.

These examples show how to evaluate:

- grounded RAG behavior
- abstention when evidence is missing
- structured JSON output
- hallucination failures and CI gating

They are designed to work out-of-box with `veritell-cli` and use fixed `mock_response` values, so you can run them without connecting a live model.

## Files in this repo

- `grounded_rag.yaml`
- `abstention.yaml`
- `structured_output.yaml`
- `hallucination_failure.yaml`
- `refund_policy_schema.json`

## Quick start

From this repo, with `veritell-cli` already installed in your environment:

```powershell
veritell test .\grounded_rag.yaml
veritell test .\abstention.yaml
veritell test .\structured_output.yaml
veritell test .\hallucination_failure.yaml
```

If you are developing locally with the sibling repo in this workspace, you can install it from source:

```powershell
python -m pip install -e ..\veritell-cli
```

## What each example demonstrates

### `grounded_rag.yaml`

Checks:

- expected evidence was retrieved
- retrieved context contains the answer
- final response is grounded and does not introduce unsupported claims

### `abstention.yaml`

Checks:

- the system abstains when the evidence is missing
- the abstaining answer stays grounded in the provided context

### `structured_output.yaml`

Checks:

- the response is valid JSON
- the response matches the required schema

### `hallucination_failure.yaml`

Checks:

- unsupported claim detection fires
- terminal output highlights unsupported spans
- CI reliability gating fails when the score is below threshold

## CI gating demo

Passing example:

```powershell
veritell test .\grounded_rag.yaml --fail-below 80
```

Failing example:

```powershell
veritell test .\hallucination_failure.yaml --fail-below 80
```

## Full demo sequence

```powershell
veritell test .\grounded_rag.yaml
veritell test .\abstention.yaml
veritell test .\structured_output.yaml
veritell test .\hallucination_failure.yaml --fail-below 80
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
