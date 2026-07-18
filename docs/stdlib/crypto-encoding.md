# Crypto And Encoding Reference

Native path (`alef run`). Digests, HMAC, random bytes, and base64 helpers.

## `std.crypto`

| Function | Role |
|----------|------|
| `sha256(data)` | SHA-256 hex digest of a string |
| `hmac_sha256(key, data)` | HMAC-SHA256 hex digest |
| `random_bytes(n)` | Cryptographic random bytes as hex (length `n`) |
| `sha256_base64(data)` | SHA-256 over base64-decoded input (specialized form) |

Additional primitives (AES, Ed25519, PBKDF2, and related helpers) ship on the
native binary; start with the functions above for signatures and tokens.

### Runnable digests

```alef
import std.crypto { sha256, hmac_sha256, random_bytes }

fn main() {
    println(sha256("abc"))
    println(hmac_sha256("secret", "payload"))
    println(random_bytes(16))
}
```

```bash
alef run main.alef
```

## `std.encoding` and `std.base64`

| Function | Role |
|----------|------|
| `std.encoding.base64_encode(s)` | Base64-encode a string |
| `std.encoding.base64_decode(s)` | Base64-decode a string |
| `std.base64.encode(s)` / `decode(s)` | Same helpers under the `std.base64` namespace |

### Encode and decode

```alef
import std.encoding { base64_encode, base64_decode }

fn main() {
    let wire = base64_encode("hello")
    println(wire)
    println(base64_decode(wire))
}
```

## Notes

- Prefer HMAC + short-lived tokens over putting secrets in cookies.
- Cookie helpers live on `std.http` — see [HTTP And JSON](http-json.md).
- July 2026 snapshot: [What's New](../reference/whats-new-2026-07.md).
