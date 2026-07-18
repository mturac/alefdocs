# Bytecode and JIT

The normal command is:

```bash
alef run main.alef
```

Bytecode modes are available for runtime work:

```bash
alef --bytecode run main.alef
alef --strict-bytecode run main.alef
```

`--bytecode` attempts bytecode first and may fall back to the tree-walking
runtime for unsupported bytecode features.

`--strict-bytecode` does not fall back. Use it when validating bytecode support.

JIT support is runtime-feature dependent and should be documented separately
from the production default path.
