# Siesta Conformance Checklist

## Library Authors

- [ ] `siesta.manifest.json` validates against `spec/manifest-schema.json`
- [ ] All `params` and `config` use JSON Schema object form
- [ ] Adapter implements `LibraryAdapterInterface`
- [ ] At least one documented agent scenario
- [ ] Structured errors with `retryable` and `suggestedFix` where applicable

## Adapter Implementers

- [ ] JSON-RPC 2.0 wire format
- [ ] All v1 operations implemented
- [ ] Handle lifecycle (create, invoke, release, expired detection)
- [ ] Manifest introspection via `siesta.introspect`
