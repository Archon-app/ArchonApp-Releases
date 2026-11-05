# Archon — Releases

Download builds of **Archon**, the priority inbox overlay.

**[⬇ Download the latest release](https://github.com/Archon-app/ArchonApp-Releases/releases/latest)**

| Platform | File to download |
| --- | --- |
| macOS (Apple Silicon) | `archon-app_<version>_aarch64.dmg` |
| macOS (Intel) | `archon-app_<version>_x64.dmg` |
| Windows | `archon-app_<version>_x64-setup.exe` |
| Linux | `archon-app_<version>_amd64.AppImage` — `chmod +x` it, then run it |

Once installed, Archon checks for updates when it starts and offers them in
the app. You can also check any time from **Settings → Updates**. Updates are
cryptographically signed; the app refuses any update that is not.

> **Alpha builds are not notarized / code-signed yet.** On macOS, the first
> launch needs right-click → **Open**. On Windows, SmartScreen may ask you to
> confirm ("More info" → "Run anyway"). Updates after the first install are
> not affected.

---

## For maintainers

This repository only hosts **releases**. Source code lives in the private
`Archon-app/Archon-app` repository. Nothing in this branch is used by the app.

### How the app finds updates

Installed copies poll

```
https://github.com/Archon-app/ArchonApp-Releases/releases/latest/download/latest.json
```

so the `latest.json` attached to the **latest published release** is what
every user sees. Drafts and pre-releases are never "latest", so they are
invisible to installed apps.

### Each release contains

| Asset | Purpose |
| --- | --- |
| `*.app.tar.gz` + `.sig` | macOS update bundle (one per architecture) |
| `*.dmg` | macOS first install |
| `*-setup.exe` + `.sig` | Windows installer, also the Windows update bundle |
| `*.AppImage` + `.sig` | Linux app, also the Linux update bundle |
| `latest.json` | update manifest: version, notes, and per-platform URL + signature |

One installer format per OS on purpose: each one can update itself. A `.deb`,
`.rpm` or `.msi` install would be offered updates it cannot apply.

### Publishing a release

Never upload files here by hand — a hand-assembled `latest.json` with a stale
signature breaks updates for every user without any visible error.

- **All platforms:** in `Archon-app`, run the **Release** GitHub Actions
  workflow (manual only). It builds every platform, uploads to a **draft**
  release here, and assembles `latest.json`. Test the draft, then publish it.
- **Local macOS-only build:** in `Archon-app`, run
  `./run-archon.sh release` then `./run-archon.sh publish`.

Full process, signing key handling and troubleshooting:
`docs/updater.md` in the `Archon-app` repository.

### Rules

- **Never edit, replace or delete assets of a published release.** Ship a new,
  higher version instead. Installed copies may already be downloading them.
- **Never commit binaries to this branch.** They belong on releases.
- **Rolling back** means publishing the old code under a new, higher version.
