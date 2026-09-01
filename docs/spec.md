---
title: Protocol
---

# Siesta Protocol v1.0

See the full specification in the [repository](https://github.com/siesta-ai-protocol/siesta/blob/main/spec/SIESTA.md).

## Core Flow

1. `siesta.discover` — find libraries
2. `siesta.introspect` — read manifest
3. `siesta.create` — factory → handle
4. `siesta.invoke` — method → value or new handle

All messages use JSON-RPC 2.0.
