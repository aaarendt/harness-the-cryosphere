# Troubleshooting

Load this when a documented setup/build command fails or behaves
unexpectedly. These apply regardless of platform (first hit on WSL2, since
confirmed to recur on EC2).

- **Conda's `auto_activate_base` can shadow the Python interpreter** needed
  to build OpenJarvis's Rust extension (`openjarvis_rust`). Fix with
  `conda config --set auto_activate_base false` if conda is present — this
  has reverted on its own before, so re-check it if the build breaks again.
- **Install `build-essential` (gcc/cc) before running the OpenJarvis
  installer.** Its absence causes `linker \`cc\` not found` errors when
  building the Rust extension.
- **`~/.openjarvis/.scripts/build-extension.sh` has a real bug**: it builds
  the Rust extension via `uv run maturin develop` from `~/.openjarvis/src`,
  which resolves a *different* venv than the one the `jarvis` CLI wrapper
  actually execs (`~/.openjarvis/.venv`). Its own post-build self-check only
  verifies the wrong venv, so it can report success while the real serving
  venv still has no working extension. Confirmed to still require this
  manual workaround even on fresh installs:
  ```bash
  cd ~/.openjarvis/src
  uv run maturin build -m rust/crates/openjarvis-python/Cargo.toml --release
  uv pip install --python ~/.openjarvis/.venv/bin/python <path-to-built-wheel> --force-reinstall
  ```
  Verify with:
  `~/.openjarvis/.venv/bin/python -c "from openjarvis._rust_bridge import RUST_AVAILABLE; print(RUST_AVAILABLE)"`
  → should print `True`. Don't trust `jarvis doctor`'s "Rust extension:
  building" background-task label — it can stay stale even once the
  extension actually works.
- No first-class "hooks" system exists in OpenJarvis (nothing analogous to
  Claude Code's pre-tool-use/stop hooks). Closest analogs: `confirm_callback`
  on `ToolExecutor`, `CapabilityPolicy` (`openjarvis/security/capabilities.py`),
  or a skills-based verifier pattern (currently the preferred approach).
