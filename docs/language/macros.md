# Macros & Metaprogramming

Alef features a powerful macro system that allows for compile-time metaprogramming and Domain-Specific Language (DSL) generation right within the language!

Macros are evaluated at compile time and return an AST (Abstract Syntax Tree) expression or statement to replace the macro call.

## The `macro` Keyword

Define a macro using the `macro` keyword.

```alef
macro my_html(content) {
    return "<div class=\"container\">" + content + "</div>";
}
```

## Calling Macros

Invoke a macro using the `!` syntax (similar to Rust).

```alef
fn main() {
    let ui = my_html!("Hello, World");
    println(ui); 
}
```

Macros can parse raw tokens, meaning you can pass custom syntax inside `{ ... }`, `( ... )`, or `[ ... ]`.

```alef
fn main() {
    let app = html! {
        <div class="app">
            <h1>Welcome to Alef!</h1>
        </div>
    };
}
```

> **Note:** The macro system is currently in active development. Native support for complex AST manipulation is landing in upcoming releases.
