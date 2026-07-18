# Database and Cache

## Database

Alef native examples use `std.db` for SQLite-backed workflows.

```alef
import std.db { connect, exec, query }

let db = connect("sqlite:/tmp/app.db")
exec(db, "CREATE TABLE events (id TEXT PRIMARY KEY, body TEXT)", [])
exec(db, "INSERT INTO events (id, body) VALUES (?1, ?2)", ["e1", "hello"])
let rows = query(db, "SELECT body FROM events WHERE id = ?1", ["e1"])
println(rows[0]["body"])
```

## Cache

```alef
import std.cache { make, get, set }

let cache = make(64)
set(cache, "ticket:TD-101", "open", 60)
println(get(cache, "ticket:TD-101"))
```
