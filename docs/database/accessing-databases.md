# Accessing a Database

Alef native examples can use `std.db` for SQLite-backed workflows.

```alef
import std.db { connect, exec, query }

fn main() {
    let db = connect("sqlite:/tmp/alef-example.db")
    exec(db, "CREATE TABLE events (id TEXT PRIMARY KEY, body TEXT NOT NULL)", [])
    exec(db, "INSERT INTO events (id, body) VALUES (?1, ?2)", ["e1", "hello"])

    let rows = query(db, "SELECT body FROM events WHERE id = ?1", ["e1"])
    println(rows[0]["body"])
}
```

## Public Example Rule

Public examples should default to SQLite or stubbed local state so they can run
without credentials.

Use external database drivers only in pages that explicitly document that setup.
