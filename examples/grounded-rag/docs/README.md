# Grounded RAG Example

This example demonstrates a clean, fully grounded retrieval-augmented generation result.

## Goal

Verify that the system:

- retrieved the correct supporting document
- had enough evidence to answer the question
- did not introduce unsupported claims

## Primary test file

- `../grounded_rag.yaml`

## Companion assets

- `../mock-context/retrieved-docs.txt` — human-readable copy of the evidence used in the test
- `../screenshots/expected-output.svg` — example terminal output for a passing run

## Suggested command

```powershell
veritell test .\examples\grounded-rag\grounded_rag.yaml
```

