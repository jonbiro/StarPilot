# Offline Privacy Mode

This branch adds an explicit `OfflinePrivacyMode` setting. It defaults to **enabled** on this branch.

## What it blocks

When enabled, the device does not automatically connect to the comma/Konik or StarPilot backend services used for:

- device registration/authentication
- Athena remote websocket access
- route/log uploading
- Prime status polling
- cloud drive-stat sync
- local stats daemon collection intended for upload
- crash/error reporting to the StarPilot Bugsink endpoint
- StarPilot backend registration
- StarPilot Galaxy presence / remote-toggle sync
- StarPilot stats upload
- Galaxy FRP remote tunnel

The relevant modules also contain their own privacy-mode checks so an accidental/manual launch does not silently reconnect.

## What remains local

- driving and control processes
- driver monitoring
- local route/log recording
- local StarPilot statistics/counters
- settings and local Galaxy UI
- calibration and vehicle state
- local crash/error files

## Functional internet access that is intentionally still allowed

Privacy mode is not a network firewall. Functional, user-facing downloads can still use the internet, including:

- GitHub software update checks for this fork
- model/theme/resource downloads
- maps/navigation providers
- services explicitly configured or invoked by the user (for example a custom notification endpoint or Tailscale setup)

If you need an air-gapped build, those should be disabled separately.

## Integrity metadata

Privacy mode does **not** spoof or suppress software identity. The normal Git branch, commit, remote, diff/dirty state, and other local build metadata remain truthful. No code in this branch attempts to impersonate official comma software or bypass server-side eligibility/enforcement checks.
