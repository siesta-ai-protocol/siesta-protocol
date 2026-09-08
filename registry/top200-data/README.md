# Top 200 data

Source list: [`libraries.json`](libraries.json)

| Script | Purpose |
|--------|---------|
| [`generate.mjs`](generate.mjs) | Initial packages + tracker + registry |
| [`deepen-lib.mjs`](deepen-lib.mjs) | Shared S→D helpers |
| [`deepen-pass.mjs`](deepen-pass.mjs) | Deepen batch 1 |
| [`deepen-pass-2.mjs`](deepen-pass-2.mjs) | Deepen batch 2 |
| [`add-package-versions.mjs`](add-package-versions.mjs) | Add `package` + `since` + registry version fields |

```bash
# from monorepo root
node siesta-protocol/registry/top200-data/generate.mjs
node siesta-protocol/registry/top200-data/deepen-pass.mjs
node siesta-protocol/registry/top200-data/deepen-pass-2.mjs
node siesta-protocol/registry/top200-data/deepen-pass-3.mjs
```

Does not overwrite existing `siesta-carbon` / `carbon-date` packages (`existing: true`).
