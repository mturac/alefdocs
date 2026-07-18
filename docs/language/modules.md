# Modules and Imports

Import only the names you need:

```alef
import std.http { html, json_response, problem_response }
import std.ai { complete_with }
```

Qualified names also work:

```alef
std.http.listen_options(address, app(), options)
```

## Project Module

`alef.mod` names a project:

```text
module ticketdesk

version 0.1.0
```

Keep public examples portable. Do not put machine-local paths in docs or module
files.
