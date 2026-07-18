# 11. Database, Cache, And State

Alef includes standard-library surfaces for persistence and cache-backed
programs.

## SQLite Example

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

## Cache Example

```alef
import std.cache { make, get, set }

let cache = make(64)
set(cache, "ticket:TD-101", "open", 60)
println(get(cache, "ticket:TD-101"))
```

## State In HTTP Programs

Alef HTTP handlers return the next state:

```alef
return { "response" => response, "state" => next_state }
```

That makes it possible to write server examples that mutate state and prove the
mutation through a smoke test.
