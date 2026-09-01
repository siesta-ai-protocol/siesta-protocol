# Siesta Protocol v1.0

Siesta is a language-agnostic protocol for exposing OOP library capabilities to AI agents via structured calls.

## Discovery-First Model

Libraries ship `siesta.manifest.json` on disk. Runtimes **discover** manifests — no standalone server required.

Applications embed `SiestaKernel` and call `handle(method, params)` in-process. Agents use the protocol directly through your app or agent middleware.

### Discovery sources

1. `composer.json` → `extra.siesta.manifest` (PHP)
2. `package.json` / `siesta.json` discovery paths
3. `packages/**/siesta.manifest.json`
4. `vendor/**/siesta.manifest.json` or `node_modules/**/siesta.manifest.json`

## Operations

| Method | Description |
|--------|-------------|
| `siesta.discover` | Find manifests; report valid/executable/registered |
| `siesta.validate` | Validate all discovered manifests |
| `siesta.introspect` | Fetch library manifest |
| `siesta.configure` | Set library-level config |
| `siesta.create` | Call a factory → handle + snapshot |
| `siesta.invoke` | Call method on handle → value or new handle |
| `siesta.release` | Dispose handles |
| `siesta.batch` | Sequence of operations |
| `siesta.describe` | Docs for a factory or method |

## Wire Format

JSON-RPC 2.0 when crossing process boundaries; in-process apps call `kernel.handle()` directly.

## Manifest

Each library declares an optional `adapter.class` for runtime execution. Manifest-only discovery works for validation and introspection.

See [manifest-schema.json](manifest-schema.json) and [errors.md](errors.md).
