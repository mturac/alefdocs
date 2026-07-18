# GitBook Publishing

This repository is GitBook-ready.

It is safe to publish this documentation repository separately from the private
Alef compiler/runtime source repository. The docs should expose the language
contract, tutorials, and example structure, not private implementation details.

GitBook reads:

- `README.md` as the landing page
- `SUMMARY.md` as navigation
- linked Markdown files as pages

## Publishing Steps

1. Create a GitBook space.
2. Connect GitHub.
3. Select the `aleflang-docs` repository.
4. Keep the root directory as `/`.
5. Publish from the GitBook UI.

## Rule

Every new page must be linked from `SUMMARY.md`.
