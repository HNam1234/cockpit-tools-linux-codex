# Codex Desktop Linux account switching

This branch adds Linux support for the Codex account switch flow when Cockpit
Tools is used with the unofficial codex-desktop-linux package.

## What is supported

- Auto-detection through codex-desktop on PATH, common install paths, and
  Linux desktop entries.
- Native package shims such as /usr/bin/codex-desktop that delegate to
  /opt/codex-desktop/start.sh.
- Manual selection of the launcher directory, start.sh, or Electron binary.
- Closing and starting the real Electron main process instead of treating the
  launcher shell PID as the app PID.
- CODEX_HOME injection for managed Codex instances. Multi-instance launches
  use CODEX_MULTI_LAUNCH=1, which is understood by the unofficial launcher.

## Use

1. Build and run this branch.
2. Open Cockpit Tools → Codex.
3. Leave the Codex application path empty so detection can find
   /usr/bin/codex-desktop. If detection is unavailable, choose
   /usr/bin/codex-desktop, /opt/codex-desktop/start.sh, or the
   /opt/codex-desktop directory.
4. Enable automatic Codex launch on account switch, then click Chuyển.

The default Linux app data directory is detected from
$XDG_CONFIG_HOME/Codex or ~/.config/Codex. Managed non-default instances
use an isolated .codex-desktop directory below their CODEX_HOME.

The implementation is intentionally scoped to the unofficial launcher
contract: CODEX_HOME, CODEX_MULTI_LAUNCH, CODEX_ELECTRON_USER_DATA_DIR,
--app-id=codex-desktop, and --class=codex-desktop.
