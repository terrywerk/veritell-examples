# Hallucination Failure Example

This example is intentionally designed to fail.

## Goal

Verify that Veritell:

- detects an unsupported claim span
- explains why the span is unsupported
- fails a CI reliability gate when requested

## Primary test file

- `../hallucination_failure.yaml`

## Companion assets

- `../mock-context/retrieved-docs.txt` — source context proving the correct refund window
- `../screenshots/expected-output.svg` — example terminal output showing the failure block and unsupported span

## Suggested command

```powershell
veritell test .\examples\hallucination-failure\hallucination_failure.yaml --fail-below 80
```

