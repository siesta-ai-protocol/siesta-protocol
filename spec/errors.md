# Siesta Error Codes

| Code | Retryable | Description |
|------|-----------|-------------|
| `LIBRARY_NOT_FOUND` | No | Library id not registered |
| `HANDLE_EXPIRED` | Yes | Handle released or invalid |
| `METHOD_NOT_FOUND` | No | Factory or method not in manifest |
| `INVALID_ARGUMENT` | Yes | Args failed validation |
| `TYPE_MISMATCH` | Yes | Value type wrong |
| `CONFIG_INVALID` | Yes | Config settings invalid |
| `PERMISSION_DENIED` | No | Operation not allowed |
| `INTERNAL` | No | Unexpected server error |

## Self-Healing

Errors include `retryable`, `field`, `suggestedFix`, and `docs` when applicable:

```json
{
  "code": "INVALID_ARGUMENT",
  "message": "weeks must be a non-negative integer",
  "retryable": true,
  "field": "weeks",
  "suggestedFix": { "weeks": 1 }
}
```
