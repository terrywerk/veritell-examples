# Veritell Examples

Detect hallucinations, broken RAG, and unsafe AI outputs in under 2 minutes.

This repository contains ready-to-run AI reliability tests that simulate real-world failures — so you can see exactly how Veritell catches issues **before they reach production**.

---

## ⚡ Start here (60-second demo)

Run a failing test first to see what breaks:

```bash
veritell test .\examples\hallucination-failure\hallucination_failure.yaml
```

You’ll immediately see:

* ❌ Unsupported claims flagged
* ❌ Reliability score drop
* ❌ CI gating failure

This is exactly the kind of issue that typically ships unnoticed.

---

## 🧠 What Veritell does

Most teams rely on logs and observability **after something goes wrong**.

Veritell helps you test AI behavior **before deployment** using repeatable assertions like:

* `no_unsupported_claims`
* `retrieval_contains_answer`
* `should_abstain`
* `json_schema_valid`

Think of it as:

> **Unit testing for LLM behavior**

---

## 🎯 Try this on your own AI system

Curious what issues might exist in your LLM app?

We’ll run a **free AI reliability scan** on your prompts, RAG pipeline, or agent workflows.

👉 Join the beta: https://veritell.ai/join-beta

You’ll get:
- Hallucination detection
- Retrieval gap analysis
- Schema / output validation
- A reliability score

(No setup required)

---

## 👥 Who this is for

* Teams building RAG applications
* AI agents in production
* LLM-powered features with compliance or risk concerns
* Engineering teams that want CI/CD reliability for AI

---

## 📦 What’s in this repo

Examples of AI reliability testing for:

* Grounded RAG systems
* Abstention behavior
* Structured outputs (JSON/schema validation)
* Hallucination detection and failure scenarios

Each example includes:

* Test YAML definitions
* Mock context or supporting data
* Expected outputs
* Failure scenarios

---

## 📂 Folder structure

```
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

---

## 🚀 Quick start

With `veritell-cli` installed:

```bash
veritell test .\examples\grounded-rag\grounded_rag.yaml
veritell test .\examples\abstention\abstention.yaml
veritell test .\examples\structured-output\structured_output.yaml
veritell test .\examples\hallucination-failure\hallucination_failure.yaml
```

Run all examples:

```bash
veritell test .\examples\
```

---

## 📊 Example output

```
Suite: examples/grounded-rag/grounded_rag.yaml

PASS public_grounded_rag_contractors_pto-<generated-id>
score=1.00 assertions=3/3 methods=deterministic,heuristic

Summary:
total=1 passed=1 failed=0 errors=0 skipped=0
reliability=100.00% score=1.00
```

Veritell keeps output compact while surfacing what matters:

* Pass/fail status
* Reliability score
* Assertion coverage

---

## 🔍 What each example demonstrates

### grounded_rag.yaml

* Retrieval contains the correct answer
* Context supports the response
* No unsupported claims introduced

---

### abstention.yaml

* Model abstains when evidence is missing
* Abstention stays grounded in context

---

### structured_output.yaml

* Output is valid JSON
* Output conforms to required schema

---

### hallucination_failure.yaml

* Unsupported claim detection triggers
* Problematic spans are highlighted
* CI reliability gating fails when below threshold

---

## 🧪 CI reliability gating

Passing example:

```bash
veritell test .\examples\grounded-rag\grounded_rag.yaml --fail-below 80
```

Failing example:

```bash
veritell test .\examples\hallucination-failure\hallucination_failure.yaml --fail-below 80
```

---

## 🔁 Full demo sequence

```bash
veritell test .\examples\grounded-rag\grounded_rag.yaml
veritell test .\examples\abstention\abstention.yaml
veritell test .\examples\structured-output\structured_output.yaml
veritell test .\examples\hallucination-failure\hallucination_failure.yaml --fail-below 80
veritell test .\examples\
```

---

## ⚙️ Local development setup

If working alongside the CLI repo:

```bash
python -m pip install -e ..\veritell-cli
```

---

## 🤖 Automated demo validation

This repo includes a GitHub Actions workflow:

`.github/workflows/examples-ci.yml`

When `VERITELL_CLI_REPO_TOKEN` is configured:

* Installs `veritell-cli`
* Runs passing demo suites
* Verifies hallucination failure triggers CI gating

If not configured:

* Workflow remains green
* Clear skip notice is logged

---

## 🔐 Required configuration

Because `terrywerk/veritell-cli` is private, the workflow requires:

```
VERITELL_CLI_REPO_TOKEN
```

Use a fine-grained PAT or GitHub App token with:

* **Contents: Read** access

---

## 📝 Notes

* `structured_output.yaml` is self-contained
* `refund_policy_schema.json` is included as a reusable example schema
* Empty directories (`mock-context/`, `docs/`, `screenshots/`) are intentional for future assets

---

## 🚀 What to do next

If you're building with LLMs:

👉 Run these tests on your own system
👉 Catch failures before your users do
👉 Add AI reliability checks to your CI pipeline

Start here:

👉 https://veritell.ai/join-beta

---
