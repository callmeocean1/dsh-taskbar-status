# Fork notes

This is a fork of `Joker2377/dsh-taskbar-status`, carrying one packaging change for
**DeepSeek Harness Desktop**:

- `koffi` moved from `dependencies` to an **optional peer dependency** (`>=3.1.1 <4`).

Why: DSH Desktop already ships `koffi` 3.1.1 inside the app
(`resources/app.asar.unpacked/dsh/node_modules/koffi`), and the plugin's loader resolves it
from the host module graph. Keeping `koffi` in `dependencies` makes `pnpm` / the DSH Plugins
installer stop for a native build-script approval (`ERR_PNPM_IGNORED_BUILDS`). As an optional
peer, installing this repo through the DSH Plugins page works without extra approval, and
`import('koffi')` still resolves to the bundled copy at runtime.

Base commit: `76d173ab86a8a7c0c79cac1ae2eeca82494181b8` (upstream `0.6.2`).
Verified on DSH Desktop 0.2.2-rc.1 / Electron 44.7.0: plugin loads, `KOFFI_OK 3.1.1`,
taskbar progress bar visible during turns, 42/42 unit tests pass.

No source files (`lib/`, `scripts/`, `test/`) were modified.

License: MIT (see `LICENSE`). All credit to the original author Joker2377.
