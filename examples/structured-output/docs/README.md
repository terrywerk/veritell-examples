# Structured Output Example

This example demonstrates schema-validated JSON output.

## Goal

Verify that the system:

- returns valid JSON
- includes the required fields
- conforms to the documented response schema

## Primary test file

- `../structured_output.yaml`

## Companion assets

- `../refund_policy_schema.json` — standalone public schema artifact
- `../mock-context/response-contract.md` — human-readable schema summary
- `../screenshots/expected-output.svg` — example terminal output for a passing structured-output run

## Suggested command

```powershell
veritell test .\examples\structured-output\structured_output.yaml
```

