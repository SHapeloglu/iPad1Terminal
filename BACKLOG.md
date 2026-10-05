# BACKLOG.md — iPad1Terminal

Scheduled work: `TASKS.md` phases 0–6 (bootstrap → local PTY → input/UI → ANSI/VT100 screen model → SSH via the installed `ssh` binary under PTY → usability → stability). Context: `PROJECT_CONTEXT.md`.

## Ordering constraints (from PROJECT_CONTEXT)

- Local terminal must be stable on hardware before SSH work.
- ANSI/VT100 screen model before serious SSH usage.
- Never implement an SSH protocol stack from scratch — reuse PTY + installed `ssh`.
- iPad1VNC's built-in terminal will only be removed after this app has working SSH (see iPad1VNC `RESPONSIBILITY_AUDIT.md` on its beta4 branch).

## Unscheduled ideas

- 256-color / bold / underline attributes after basic colors are stable.
- Bounded scrollback search.
- Session logging to `iPad1Files/Documents/` (opt-in, size-capped).
- `mosh`-style reconnect hints when Wi-Fi drops (UX only, no new protocol).
- Snippets shared with iPad1VNC profiles (host/user metadata, never passwords).

## Out of scope

Theme system (intentional), file manager features (iPad1Files), FTP/SFTP transfers (iPad1FTPDownloader), VNC (iPad1VNC).
