# Siesta Protocol

<p align="center">
  <img src="assets/logo.svg" alt="Siesta" width="480">
</p>

<p align="center"><strong>Let the libraries work. Take a siesta.</strong></p>

Language-agnostic specification for **AI-ready OOP libraries**. Instead of agents searching your codebase and reimplementing library behavior from scratch, they discover `siesta.manifest.json` files, validate them, and invoke capabilities through structured protocol calls.

## Repositories

| Repo | Purpose |
|------|---------|
| **[siesta-protocol](https://github.com/siesta-ai-protocol/siesta-protocol)** (this repo) | Spec, JSON schemas, adapter mappings, registry format |
| **[siesta-php](https://github.com/siesta-ai-protocol/siesta-php)** | PHP reference runtime + Carbon adapter |
| **[siesta-ts](https://github.com/siesta-ai-protocol/siesta-ts)** | TypeScript runtime |

## Protocol Operations

| Method | Description |
|--------|-------------|
| `siesta.discover` | Find manifest files; report validation status |
| `siesta.validate` | Validate all discovered manifests |
| `siesta.introspect` | Fetch library manifest |
| `siesta.configure` | Set library config |
| `siesta.create` | Factory → handle + snapshot |
| `siesta.invoke` | Method on handle → value or new handle |
| `siesta.release` | Dispose handles |
| `siesta.batch` | Operation sequence |

## Discovery Model

Libraries ship a **`siesta.manifest.json`** beside their code. Runtimes **discover** manifests from:

- `composer.json` → `extra.siesta.manifest`
- Project `siesta.json` discovery paths
- `packages/**/siesta.manifest.json` and `vendor/**/siesta.manifest.json`

No standalone server required — applications embed protocol awareness via `SiestaKernel` (PHP) or `SiestaKernel` (TS).

## Manifest

```json
{
  "siesta": "1.0",
  "library": "my-library",
  "adapter": { "class": "Vendor\\MyLibraryAdapter" },
  "factories": { ... },
  "types": { ... }
}
```

See [spec/SIESTA.md](spec/SIESTA.md) and [spec/manifest-schema.json](spec/manifest-schema.json).

## PHP / Composer

```bash
composer require siesta/protocol
```

Schema path: `vendor/siesta/protocol/spec/manifest-schema.json`

## License

MIT
