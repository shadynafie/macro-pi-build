# macro-pi-build

Weekly arm64 builds of [Macro](https://github.com/macro-inc/macro) (AGPLv3) for running its local stack on a Raspberry Pi.

A GitHub Actions workflow on a free ARM runner builds `nix build .#local-stack-binaries` from the latest `macro-inc/macro` and publishes the Nix closure as a release. The Pi imports the newest release with `nix copy` and restarts the stack with `just stack update --binaries-dir`, keeping its data.

This is a personal experiment, not affiliated with Macro. Macro's source and licence: https://github.com/macro-inc/macro
