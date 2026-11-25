# macro-pi-build

Weekly arm64 builds of [Macro](https://github.com/macro-inc/macro) (AGPLv3) for running its local stack on a Raspberry Pi.

A GitHub Actions workflow on a free ARM runner builds `nix build .#local-stack-binaries` from the latest `macro-inc/macro` and publishes the Nix closure as a release. The Pi imports the newest release with `nix copy` and restarts the stack with `just stack update --binaries-dir`, keeping its data.

This is a personal experiment, not affiliated with Macro. Macro's source and licence: https://github.com/macro-inc/macro

## Automations

| Workflow | When | What |
|---|---|---|
| `build-arm64` | Sundays 10 pm UTC, or by hand | Builds Macro's latest **production release tag** (what macro.com runs) for arm64 and publishes it here. Skips if already built. |
| `security-advisories` | Daily 6:30 am UTC | Runs `cargo deny check advisories` (adapted from Macro's own daily job) against the version last built for the Pi. Opens an issue if a RustSec advisory appears. |

The Pi side (separate) downloads the newest release weekly, restarts Macro keeping its data, health-checks it, and rolls back if the new version fails.
