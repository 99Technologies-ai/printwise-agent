# PrintWise Agent

Public distribution of the **PrintWise Agent** — the local printing companion
for [ShipNest](https://shipnest.ai)'s cloud-based shipping label and order
management platform. The agent runs on a workstation connected to a label or
document printer, talks to the PrintWise cloud over WebSocket, and prints
shipping labels and packing slips that arrive from the connected ShipNest
account.

This repository hosts **binaries only**. The source lives in a private
repository owned by [99Technologies](https://99technologies.com/); use the
issues / contact channels at [shipnest.ai](https://shipnest.ai) for support.

## Download

Pick the latest release tagged `agent-vX.Y.Z` from the
[Releases page](https://github.com/99Technologies-ai/printwise-agent/releases).
Each release contains:

| File                                          | Platform           |
| --------------------------------------------- | ------------------ |
| `printwise-agent-<version>-windows-amd64.exe` | Windows 10 / 11 (x64) |
| `printwise-agent-<version>-macos-amd64`       | macOS 11+ (Intel) |
| `printwise-agent-<version>-linux-amd64`       | Linux (x64) — CLI / service-style |

The Windows build is the primary, fully-featured target (system-tray UI,
sign-in window, auto-updater). macOS and Linux are CLI-style builds for
service deployments.

## Install (Windows)

1. Download `printwise-agent-<version>-windows-amd64.exe` from the latest
   release.
2. Double-click the file. No admin rights are needed — the agent installs
   into your user profile (`%LocalAppData%\PrintWise\Agent\`) and registers
   itself in **Add/Remove Programs** plus a logon-startup item.
3. SmartScreen may show a "Windows protected your PC" dialog the first
   time. Click **More info → Run anyway** — these binaries are not yet
   Authenticode-signed, but they are the same files served from this
   repository's Releases.
4. A printer-shaped tray icon appears and a sign-in window opens. Enter
   your PrintWise server URL plus the credentials issued from your
   ShipNest admin panel.

## Install (macOS / Linux)

These platforms ship a single binary; install where you prefer:

```bash
# macOS
chmod +x printwise-agent-<version>-macos-amd64
sudo mv printwise-agent-<version>-macos-amd64 /usr/local/bin/printwise-agent
printwise-agent --help

# Linux
chmod +x printwise-agent-<version>-linux-amd64
sudo mv printwise-agent-<version>-linux-amd64 /usr/local/bin/printwise-agent
printwise-agent --help
```

Run as a foreground process, or wire into systemd / launchd for an
unattended deployment. (Sample unit files are not yet shipped — open
an issue if you need one.)

## Versioning

Two release channels:

- `agent-vX.Y.Z` — **stable**. Built from a `release/vX.Y.Z` branch, frozen
  once cut over to production. This is the default channel for end-user
  installs.
- `agent-dev-vX.Y.Z` — **pre-release** (marked as such on the Releases
  page). Refreshed on every push to the development branch; expect
  rolling updates and not-yet-tested behavior. Useful for QA / canary
  workstations.

Versions are kept in lockstep with the rest of the ShipNest stack
(orderapi, frontend, printwise service) — picking the version that
matches your ShipNest deployment is the safe default.

## Auto-update

The agent checks for newer versions on a fixed interval and replaces
itself in place when a higher version becomes available on its
configured channel. Stable installs follow `agent-v*`; dev/canary
installs follow `agent-dev-v*`.

## Reporting issues

This repository is read-only — issues and PRs filed here will not be
actioned. Please reach the PrintWise / ShipNest team via:

- The support form on [shipnest.ai](https://shipnest.ai)
- Your account manager, if you have one

When reporting, include: agent version (right-click the tray icon →
**About**), Windows / macOS version, and the contents of the agent log
folder (right-click the tray icon → **Open log folder**).

## License

The PrintWise Agent is proprietary software © 99Technologies. The
binaries published here are made available for use solely with an
authorized PrintWise / ShipNest deployment. Redistribution, modification,
or reverse-engineering is not permitted.
