# Archon — Releases

Download builds of **Archon**, the priority inbox overlay.

## Install with one command (recommended)

**Mac or Linux:** open Terminal and paste

```bash
curl -fsSL https://github.com/Archon-app/ArchonApp-Releases/releases/latest/download/install.sh | bash
```

**Windows:** open PowerShell and paste

```powershell
irm https://github.com/Archon-app/ArchonApp-Releases/releases/latest/download/install.ps1 | iex
```

The command picks the right build for your computer (Apple chip or Intel,
64-bit Windows or Linux), checks the download, installs it and starts Archon.
No security prompt comes up: files fetched this way are not marked as
browser downloads, so macOS Gatekeeper and Windows SmartScreen leave them alone.
Running it again repairs the install.

| | Mac | Linux | Windows |
| --- | --- | --- | --- |
| Installs to | `/Applications/archon-app.app` (or `~/Applications`) | `~/.local/share/archon/Archon.AppImage` + app menu entry | `%LOCALAPPDATA%\archon-app` (no admin rights needed) |
| A specific version | `… \| ARCHON_VERSION=1.2.3 bash` | `… \| ARCHON_VERSION=1.2.3 bash` | `$env:ARCHON_VERSION="1.2.3"; irm … \| iex` |
| Uninstall (keeps your data) | `… \| bash -s -- --uninstall` | `… \| bash -s -- --uninstall` | `$env:ARCHON_UNINSTALL="1"; irm … \| iex` |

`1.2.3` stands for any published version. On Windows the installer clears
`ARCHON_VERSION` and `ARCHON_UNINSTALL` when it finishes (whether it worked or
not), so they never affect a later command in the same PowerShell window.
Written out in full:

```powershell
$env:ARCHON_UNINSTALL="1"; irm https://github.com/Archon-app/ArchonApp-Releases/releases/latest/download/install.ps1 | iex
```

The scripts are `install.sh` and `install.ps1` on every release. They run
with your user's rights, never `sudo`, so read them first if you like.

## Or download a file yourself

**[⬇ Download the latest release](https://github.com/Archon-app/ArchonApp-Releases/releases/latest)**

| Your computer | File to download |
| --- | --- |
| Mac with an Apple chip (M1, M2, M3, M4…) | `Archon-<version>-macOS-AppleSilicon.dmg` |
| Mac with an Intel chip | `Archon-<version>-macOS-Intel.dmg` |
| Windows 10/11 (64-bit) | `Archon-<version>-Windows-x64-Setup.exe` |
| Linux (64-bit) | `Archon-<version>-Linux-x86_64.AppImage` — `chmod +x` it, then run it |

Not sure which Mac you have? Apple menu → **About This Mac** → **Chip**.
Older builds use Tauri's default names (`archon-app_<version>_aarch64.dmg` =
Apple chip, `_x64` = Intel).

Once installed, Archon checks for updates when it starts and offers them in
the app. You can also check any time from **Settings → Updates**. Updates are
cryptographically signed; the app refuses any update that is not.

> **Alpha builds are not notarized / code-signed yet.** With the one-line
> install above there is no prompt. With a file downloaded in the browser:
>
> - **macOS, current builds:** macOS says *"Apple could not verify
>   'archon-app' is free of malware…"*. Click **Done**, then open
>   **System Settings → Privacy & Security**, scroll down and click
>   **Open Anyway**.
> - **macOS, builds made before ad-hoc signing was enabled:** macOS says the
>   app *"is damaged and can't be opened"*. Move it to Applications, then run
>   this in Terminal:
>   `xattr -dr com.apple.quarantine /Applications/archon-app.app`
> - **Windows:** SmartScreen may ask you to confirm (**More info** →
>   **Run anyway**).
>
> Updates after the first install are not affected.

---
