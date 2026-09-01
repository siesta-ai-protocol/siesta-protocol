# Siesta

AI-ready OOP libraries. Let the agent nap.

[Get Started](quickstart.html){: .btn .btn-primary }
[Protocol Spec](spec.html){: .btn .btn-outline }

## What is Siesta?

Siesta lets reusable OOP libraries expose **structured agent-callable capabilities**. Your agent discovers a manifest, creates object handles, and invokes methods — no code search required.

```json
{"method":"siesta.invoke","params":{"handle":"hdl_1","method":"addWeeks","args":{"weeks":2}}}
```

## Supported Libraries

| Library | Language | Package | Status |
|---------|----------|---------|--------|
| Carbon Date/Time | PHP | `siesta/carbon` | Official |

[Add your library →](libraries.html)
