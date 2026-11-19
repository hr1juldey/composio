---
'@composio/python-sdk': patch
---

Fix custom tools with keyword-only parameters failing at execution. `@experimental.tool()` accepted functions like `def search(*, payload: MyInput, ctx)` when inferring the schema, but called them positionally at runtime, raising `TypeError`. The decorator now binds the validated input and session context by the declared parameter kinds; positional signatures are unchanged.
