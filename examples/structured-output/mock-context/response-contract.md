# Structured Output Contract

The structured output example expects the response to be valid JSON with this shape:

- `answer` — string
- `citations` — array of one or more strings

This example uses an inline schema reference named `refund_policy_schema` inside `structured_output.yaml`, and also ships a companion JSON schema file in the same folder for public inspection.

