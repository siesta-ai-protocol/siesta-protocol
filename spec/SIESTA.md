# Siesta Protocol v1.0

Siesta is a language-agnostic protocol for exposing OOP library capabilities to AI agents via structured calls.

## Schemas (normative)

| Schema | Path | Purpose |
|--------|------|---------|
| **Manifest** | [`manifest-schema.json`](manifest-schema.json) | Validates `siesta.manifest.json` |
| **Messages** | [`message-schema.json`](message-schema.json) | Params/results for all `siesta.*` ops + JSON-RPC envelopes |
| **Registry** | [`../registry/schema.json`](../registry/schema.json) | Validates `registry/libraries.yaml` entries |
| **Errors** | [`errors.md`](errors.md) | Error codes and self-healing metadata |

## Discovery-First Model

Libraries ship `siesta.manifest.json` on disk. Runtimes **discover** manifests — no standalone server required.

Applications embed `SiestaKernel` and call `handle(method, params)` in-process. Agents use the protocol directly through your app or agent middleware.

### Discovery sources

1. `composer.json` → `extra.siesta.manifest` (PHP)
2. `package.json` / `siesta.json` discovery paths
3. `packages/**/siesta.manifest.json`
4. `vendor/**/siesta.manifest.json` or `node_modules/**/siesta.manifest.json`

## Operations

| Method | Params | Result |
|--------|--------|--------|
| `siesta.discover` | `{}` | `{ siestaVersion, sessionId, projectRoot?, libraries[] }` |
| `siesta.validate` | `{}` | `{ siestaVersion, valid, libraries[] }` |
| `siesta.introspect` | `{ library }` | `{ siestaVersion, manifest }` |
| `siesta.configure` | `{ library, settings }` | `{ siestaVersion, library, config }` |
| `siesta.create` | `{ library, factory, args? }` | `{ siestaVersion, handle, type, snapshot }` |
| `siesta.invoke` | `{ handle, method, args? }` | handle result **or** `{ siestaVersion, value, type? }` |
| `siesta.release` | `{ handles[] }` | `{ siestaVersion, released }` |
| `siesta.batch` | `{ operations[] }` | `{ siestaVersion, results[] }` or early `{ error, completed }` |
| `siesta.describe` | `{ library, capability }` | `{ siestaVersion, capability, kind, type?, definition }` |

See [`message-schema.json`](message-schema.json) definitions (`*Params` / `*Result`) for full field constraints.

### Example flow

```
1. siesta.create  { library: "siesta-carbon", factory: "now" }
   → { handle: "hdl_1", type: "DateTime", snapshot: { ... } }

2. siesta.invoke  { handle: "hdl_1", method: "addWeeks", args: { weeks: 2 } }
   → { handle: "hdl_2", type: "DateTime", snapshot: { ... } }

3. siesta.invoke  { handle: "hdl_2", method: "format", args: { pattern: "Y-m-d" } }
   → { value: "2026-09-16", type: "string" }
```

## Wire Format

- **In-process:** `kernel.handle(method, params)` → result object or `{ error }`
- **Cross-process:** JSON-RPC 2.0 (`jsonrpc`, `id`, `method`, `params` / `result` / `error`)

Siesta application errors use code `-32000` with `error.data` carrying the structured [`siestaError`](message-schema.json) object (`code`, `message`, `retryable`, optional `field`, `suggestedFix`, `docs`).

## Manifest

Each library declares an optional `adapter.class` for runtime execution. Manifest-only discovery works for validation and introspection.

All `params` and `config` blocks **must** use full JSON Schema object form:

```json
{ "type": "object", "properties": { ... }, "required": [ ... ] }
```

See [manifest-schema.json](manifest-schema.json) and [errors.md](errors.md).

## Handles and sessions

| Concept | Purpose |
|---------|---------|
| `sessionId` | Scoped workspace for an agent run |
| `handle` | Opaque id (`hdl_…`) referencing a live instance |
| `snapshot` | Adapter-defined serializable view of the instance |
| `value` | Primitive / typed result returned inline (no new handle) |

Chainable methods that return objects produce a **new** handle. Value methods return `{ value, type }`.
