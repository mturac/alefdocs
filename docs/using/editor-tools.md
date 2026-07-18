# Editor Plugins and IDEs

Alef projects are plain text and work in any editor.

Recommended editor behavior:

- syntax highlighting for `.alef`
- run task for `alef run main.alef`
- run task for `bash scripts/smoke.sh`
- diagnostics pane for command output

Language-server support should expose:

- hover information
- completion
- go-to definition
- rename
- workspace symbols

For public examples, editor setup should be optional. A user should be able to
clone the repo and run the smoke script from a terminal.
