# MCP Adapter Mapping

Siesta operations map to MCP as a **single meta-tool** plus manifest resources.

| Siesta | MCP |
|--------|-----|
| `siesta.discover` | Tool `siesta` with `operation: discover` |
| `siesta.create` / `invoke` | Tool `siesta` with `operation: create` / `invoke` |
| Manifest | Resource `siesta://{library}/manifest` |
| Handles | Adapter-managed session store |

Use JSON-RPC 2.0 end-to-end per MCP spec (`initialize`, `tools/list`, `tools/call`).
