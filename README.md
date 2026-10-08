# Install Dial

Public installer scripts for Dial. This repository contains no Dial application source or binaries.
Dial's source repository and release downloads remain private. You need a GitHub account granted
access to `KiidxAtlas/dial`; the installer opens GitHub login if you are not signed in.

## Windows (PowerShell)

```powershell
irm https://raw.githubusercontent.com/KiidxAtlas/dial-install/main/install.ps1 | iex
```

The installer handles GitHub CLI, Git for Windows, sign-in, checksums, executable version verification,
and your user PATH. Windows App Installer (`winget`) is required to install missing prerequisites.
Then run `dial --sandbox off` in your project. Native Windows command tools run with your normal user
permissions and approval prompts; Windows filesystem confinement requires WSL. MLX requires Apple Silicon.

## macOS / Linux

```sh
curl -fsSL https://raw.githubusercontent.com/KiidxAtlas/dial-install/main/install.sh | bash
```

The installer sets up a checksum-verified GitHub CLI without Homebrew or administrator access, handles
sign-in, selects the matching release, and adds Dial to your shell configuration. Open a new terminal
and run `dial`, or start immediately with `~/.local/bin/dial`. Linux additionally needs a working
bubblewrap sandbox; see the private Dial README for Linux/WSL setup.

Run the same command to update. Failed downloads, checksums or executable version checks preserve
the existing Dial binary. A release must contain the matching archive and checksum; the installer
exits with a clear message if your platform's download has not been published yet.

Supported release targets: Apple Silicon and Intel Mac, native Windows x64, Linux x86-64.
A public installer does not grant access to private downloads or bypass GitHub permissions.

To select a version, download the script and run `bash install.sh v0.1.3` or
`powershell -NoProfile -ExecutionPolicy Bypass -File .\install.ps1 -Version v0.1.3`.

## Maintainers

The canonical installers and tests live in `KiidxAtlas/dial/scripts`. Copy only the two installers,
their standalone tests, and LICENSE here when updating. Never copy source code, credentials or release binaries.
The public CI tests installers with disposable fixtures; it does not access the private repository.
