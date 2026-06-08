<p align="center">
  <h1 align="center">encoding-doctor</h1>
  <p align="center"><b>Scan, fix, and verify file encoding issues — in one command.</b></p>
  <p align="center">
    <img src="https://img.shields.io/badge/python-3.9+-blue?style=flat-square" />
    <img src="https://img.shields.io/badge/license-MIT-green?style=flat-square" />
    <img src="https://img.shields.io/badge/platform-Windows%20%7C%20macOS%20%7C%20Linux-lightgrey?style=flat-square" />
    <img src="https://img.shields.io/badge/scan-free%20forever-brightgreen?style=flat-square" />
    <img src="https://img.shields.io/badge/PyPI-encoding--doctor-blue?style=flat-square" />
  </p>
  <p align="center">
    <a href="https://stateflow-dev.github.io/stateflowlabs/encoding-doctor.html">Docs & Pricing</a> ·
    <a href="https://pypi.org/project/encoding-doctor/">PyPI</a> ·
    <a href="https://stateflow-dev.github.io/stateflowlabs/">Stateflow Labs</a>
  </p>
</p>

---

> Stop debugging encoding manually.
> One command. Project clean.

---

## The Problem

You push code. CI fails.  
You open the file. Characters look fine in your editor.  
But the bytes tell a different story.

```
"Confidence ├óÔÇáÔÇÖ base=%.2f"   ← what your file actually contains
"Confidence → base=%.2f"          ← what it should be
```

This happens when UTF-8 files are opened as cp1252 on Windows,
modified, and saved back — corrupting every special character silently.

**encoding-doctor finds it, fixes it, and verifies it — automatically.**

---

## Install

```bash
pip install encoding-doctor
```

---

## Quick Start

```bash
# Scan is free forever — no license needed
enc-doctor scan ./my_project

# Fix, verify, restore — requires a license
enc-doctor activate YOUR-LICENSE-KEY
enc-doctor fix    ./my_project
enc-doctor verify ./my_project
```

Get a license → **[stateflow.dev/encoding-doctor](https://stateflow.dev/encoding-doctor)**

---

## See It Running

```
C:\Users\dev\my_project> enc-doctor scan .

SCAN REPORT
============================================================
  Total files scanned : 42
  Files with issues   : 4
  Clean files         : 38

  WARN  src/engine.py
        > mojibake: arrow → (3x)
  WARN  config/settings.ini
        > BOM (\xef\xbb\xbf) detected (1x)
        > CRLF line endings (4x)
  WARN  data/users.csv
        > null bytes (2x)
  WARN  src/utils.py
        > CRLF line endings (5x)

  Run 'enc-doctor fix <path>' to repair fixable issues.
  Review this report carefully before running fix.
```

```
C:\Users\dev\my_project> enc-doctor fix . --dry-run

DRY RUN
============================================================
  FIXED  src/engine.py
         > mojibake fixed: arrow → (3x)
  FIXED  config/settings.ini
         > BOM stripped
         > CRLF -> LF (4 lines)
  FIXED  data/users.csv
         > null bytes removed (2)
  FIXED  src/utils.py
         > CRLF -> LF (5 lines)

  Would fix 5 issue(s).
```

```
C:\Users\dev\my_project> enc-doctor verify .

VERIFY REPORT
============================================================
  PASS  42 / 42 files
  All files valid UTF-8. Safe to commit.
```

---

## What It Fixes

| Problem | Description | Free |
|---|---|---|
| **Mojibake** | UTF-8 bytes mis-read as cp1252, saved as garbage | scan only |
| **BOM** | `\xef\xbb\xbf` prefix from Notepad/Excel that breaks parsers | scan only |
| **CRLF** | Windows `\r\n` mixed with Unix `\n` — causes Git diff noise | scan only |
| **Null bytes** | Binary corruption from FTP or terminal copy-paste | scan only |
| **Non-UTF-8** | Detected and reported for manual conversion | scan only |

`scan` is **free forever**.  
`fix`, `verify`, `restore` require a license.

---

## Full Workflow

```bash
# 1. Install
pip install encoding-doctor

# 2. Activate license (one-time)
enc-doctor activate XXXX-XXXX-XXXX-XXXX

# 3. Scan — see what's broken
enc-doctor scan ./my_project

# 4. Back up your project first (always)
xcopy my_project my_project_backup\ /E /I /H   # Windows
cp -r my_project my_project_backup             # macOS / Linux

# 5. Preview changes without writing
enc-doctor fix ./my_project --dry-run

# 6. Fix
enc-doctor fix ./my_project

# 7. Verify
enc-doctor verify ./my_project

# Safe to commit ✓
```

---

## License Commands

```bash
enc-doctor activate   XXXX-XXXX-XXXX-XXXX   # activate on this machine
enc-doctor license                           # show current license status
enc-doctor deactivate                        # free up seat (switching machines)
```

---

## Compatibility

| Platform | Versions |
|---|---|
| **Windows** | 10, 11 |
| **macOS** | 10.15 Catalina — macOS 26 Tahoe |
| **Linux** | Ubuntu 20.04+ · Debian 10+ · Fedora 36+ · Arch |
| **Python** | 3.9+ |

Zero dependencies. Pure Python standard library only.  
If Python runs on it, encoding-doctor runs on it.

---

## Commands

```
enc-doctor scan       <path> [--all]      Detect encoding issues — free forever
enc-doctor fix        <path> [--dry-run]  Fix detected issues
enc-doctor verify     <path>              Confirm all files are valid UTF-8
enc-doctor restore    <file>              Restore a file from .bak backup
enc-doctor activate   <license-key>       Activate your license
enc-doctor deactivate                     Free up your license seat
enc-doctor license                        Show current license status
```

---

## Warning

> **encoding-doctor fix modifies files in-place.**
>
> - Always run `scan` first and review the report before running `fix`
> - Back up your project folder before running `fix`
> - Backups are also created automatically as `.bak` files per file
> - Run `verify` after every fix before committing
> - When in doubt, run on a Git-tracked project so you can revert with `git checkout .`

---

## Built From Real Bugs

encoding-doctor was built from real encoding corruption found in production Python projects on Windows.

The mojibake patterns in the scanner are not hypothetical — they are byte sequences extracted directly from corrupted source files using hex analysis.

---

## Pricing

| Plan | Price | Seats |
|---|---|---|
| **Solo** | $19 one-time | 1 developer |
| **Team** | $49 one-time | Up to 5 developers |

No subscription. No renewal. Pay once, use forever.

Get a license → **[stateflow.dev/encoding-doctor](https://stateflow.dev/encoding-doctor)**

---

## Keywords

encoding fix python · mojibake fixer · UTF-8 repair · BOM remover · CRLF normalizer · null byte cleaner · cp1252 utf-8 · windows encoding fix · python encoding tool · file encoding repair · encoding corruption · developer tools · cli encoding · encoding doctor

---

## Part of Stateflow Labs

encoding-doctor is a utility tool from [Stateflow Labs](https://stateflow-dev.github.io/stateflowlabs/) —
a runtime developer tooling ecosystem for Python developers.

Related projects:

- [ALGOgent Runtime](https://github.com/stateflow-dev/algogent-runtime) — Lightweight runtime intelligence SDK
- [Adaptive Runtime](https://github.com/stateflow-dev/adaptive-runtime) — Runtime intelligence layer for stateful systems

---

## License

MIT © [Stateflow Labs](https://github.com/stateflow-dev)
