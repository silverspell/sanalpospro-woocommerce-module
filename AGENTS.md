# AGENTS.md

## LoopFlow

### Build and test

Validation runs inside the LoopFlow devcontainer (`.devcontainer/loopflow/devcontainer.json`) with the commands from `.loopflow.yml`:

- Build/lint: `find . -path ./.devcontainer -prune -o -name '*.php' -print0 | xargs -0 -r -n1 php -l`
- Tests: the repository has no automated test suite; validation passes when all PHP files lint successfully.

### Coding conventions

- PHP WordPress/WooCommerce plugin code under `sanalpospro-payment-module/`.
- WordPress global functions and hooks are prefixed with `sppro_`; classes under `includes/` use the `SPPRO_` prefix (for example `SPPRO_Blocks_Support`).
- Namespaced library code lives in `vendor/Eticsoft/{Sanalpospro,Common}`; this is vendored dependency code and is not edited as part of plugin changes.
- Four-space indentation, braces on the same line for function declarations, and snake_case for WordPress functions, hooks, and options.
- Use WordPress escaping/sanitization helpers (`esc_html`, `esc_attr`, `esc_url`, `wp_kses_post`, `sanitize_*`) for output and input handling.
- All user-facing strings use the `sanalpospro-payment-module` text domain.
- Templates live under `templates/`, admin screens under `admin/`, and front-end assets under `assets/`.

### Invariants

Draft, derived from the code; violations require human review:

- Keep WordPress/WooCommerce hook names, option/meta keys, and gateway IDs stable to avoid breaking existing installations.
- Never expose API credentials, merchant keys, or tokens in client-side code, logs, or templates.
- Treat `vendor/` as vendored third-party code; regenerate rather than hand-edit it.
- All payment-related input and output must remain sanitized/escaped at the WordPress boundary.
- Do not weaken plugin activation, uninstall, or payment callback behavior without explicit human review.

### ADRs

No ADR directory is present in this repository. Architecture decisions are currently documented in commit history and the module `readme.md`/`readme.txt`.
