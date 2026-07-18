# Structs and Enums

Use structs when a shape deserves a name.

```alef
struct Task {
    id: string,
    title: string,
    done: bool
}

fn main() {
    let task = Task {
        id: "task_1",
        title: "Ship docs",
        done: false
    }
    println(task.title)
}
```

Use enums when the valid states are finite.

```alef
enum Shape {
    Circle(f64),
    Rect(f64, f64),
    Point,
}

fn area(s: Shape) -> f64 = match s {
    Circle(r) => 3.14159 * r * r,
    Rect(w, h) => w * h,
    Point => 0.0,
}
```

For UI and JSON-heavy examples, maps are often more ergonomic. For library and
domain code, structs and enums communicate stronger intent.
