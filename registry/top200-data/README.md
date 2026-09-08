# Top 200 data

Source list: [`libraries.json`](libraries.json)  
Generator: [`generate.mjs`](generate.mjs)

```bash
# from monorepo root
node siesta-protocol/registry/top200-data/generate.mjs
```

Regenerates:

- [`../TOP200.md`](../TOP200.md) tracker
- [`../libraries.yaml`](../libraries.yaml) registry
- wrapper packages under `siesta-php/packages/siesta-*` and `siesta-ts/packages/*`

Does not overwrite existing `siesta-carbon` / `carbon-date` packages (`existing: true`).
