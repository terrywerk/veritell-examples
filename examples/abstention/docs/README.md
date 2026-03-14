# Abstention Example

This example demonstrates the correct behavior when the retrieved context does not contain the answer.

## Goal

Verify that the system:

- refuses to answer when evidence is missing
- explains that the information is absent from the provided context
- avoids hallucinating a historical policy

## Primary test file

- `../abstention.yaml`

## Companion assets

- `../mock-context/retrieved-docs.txt` — the intentionally incomplete context
- `../screenshots/expected-output.svg` — example terminal output for a passing abstention run

## Suggested command

```powershell
veritell test .\examples\abstention\abstention.yaml
```

