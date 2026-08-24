# INTEGRATION

## Purpose

This document defines how `iPad1Terminal` may interact with the other iPad 1 applications without violating responsibility boundaries.

---

## Application responsibility

```text
iPad1Terminal
= local shell + terminal emulation + SSH
```

It is not:

- a file manager
- a VNC client
- a PDF reader
- an FTP download engine

---

## iPad1Files

Canonical shared files root:

```text
/var/mobile/Media/iPad1Files/
```

Potential terminal integration:

### Quick directory shortcut

A `Files` quick command may send:

```bash
cd /var/mobile/Media/iPad1Files/
```

This is preferred over copying or embedding iPad1Files logic.

### Open terminal in directory

Future optional URL scheme could allow iPad1Files to request:

```text
Open iPad1Terminal at a selected directory
```

Example conceptual scheme:

```text
ipad1terminal://local?cwd=/var/mobile/Media/iPad1Files/Documents/
```

Do not implement until the Local Terminal lifecycle and URL parsing are stable.

Security rule:

- validate path
- never silently execute arbitrary command text passed by another application

Only a directory path should be accepted for this use case.

---

## iPad1VNC

Responsibility separation:

```text
iPad1Terminal
= CLI / PTY / SSH

iPad1VNC
= graphical remote desktop
```

Do not add remote desktop features to the terminal.

---

## iPad1FTPDownloader

FTPDownloader remains responsible for network file downloading.

`iPad1Terminal` should not become another FTP downloader.

If command-line `ftp`, `scp`, or similar tools are installed on the jailbroken device, users may run them manually in the terminal. That does not change application ownership.

---

## iPad1PDFReader

No direct dependency is required.

A user may operate on files under the shared root through normal shell commands.

Do not embed PDF rendering.

---

## Future SSH/SCP behavior

SSH is part of this application.

SCP/SFTP graphical file management is not required for initial v1.

If later added, prefer routing destination selection through iPad1Files rather than creating a second general-purpose file browser.

---

## URL scheme safety

Potential future schemes:

```text
ipad1terminal://local
ipad1terminal://local?cwd=...
ipad1terminal://ssh?profile=...
```

Do not support:

```text
?command=rm ...
```

or arbitrary external command execution by URL scheme.

This avoids making the app an accidental command-execution vector.

---

## Shared code policy

Do not copy major code from:

- iPad1Files
- iPad1VNC
- iPad1FTPDownloader
- iPad1PDFReader

Use small public integration contracts instead.

---

## Shared platform policy

All iPad 1 family applications continue to target:

```text
iPad 1
iOS 5.1.1
armv7
256 MB RAM
non-ARC / MRC
Theos
```

Each project must still be independently buildable.
