# encfix-precision

**Scan, fix, and verify file encoding issues across your project in one command.**

Fixes mojibake, BOM, CRLF line endings, null bytes, and non-UTF-8 encoding —
automatically detected and repaired, with backups created before every change.

Built from real encoding bugs found in production Python projects on Windows.

---

## Install

```bash
pip install encfix-precision
```

---

## Usage

```bash
# Step 1 — scan first, always
enc-doctor scan ./my_project

# Step 2 — preview changes without writing
enc-doctor fix ./my_project --dry-run

# Step 3 — fix (backups created automatically as .bak)
enc-doctor fix ./my_project

# Step 4 — verify everything is clean
enc-doctor verify ./my_project
```

---

## Free vs Licensed

| Command | Access |
|---|---|
| `scan` | ✅ Free forever |
| `fix` | 🔑 Requires license |
| `verify` | 🔑 Requires license |
| `restore` | 🔑 Requires license |

```bash
# Activate your license
enc-doctor activate <YOUR-KEY>

# Check license status
enc-doctor license

# Deactivate (free up seat for another machine)
enc-doctor deactivate
```

Get your license → [stateflow.dev/encoding-doctor](https://stateflow-dev.github.io/stateflowlabs)

---

## What it fixes

| Problem | Description |
|---|---|
| **Mojibake** | UTF-8 bytes mis-read as cp1252 and saved as garbage |
| **BOM** | `\xef\xbb\xbf` prefix added by Notepad/Excel that breaks parsers |
| **CRLF** | Windows `\r\n` mixed with Unix `\n` — causes Git diff noise |
| **Null bytes** | Binary corruption from FTP or terminal copy-paste |
| **Non-UTF-8** | Detected and flagged for manual conversion |

---

## Warning

> **encoding-doctor modifies files in-place.**
>
> - Always run `scan` first and review the report before running `fix`.
> - Backups are created automatically as `.bak` files.
> - Run on a Git-tracked project so you can always revert with `git checkout .`
> - Do not run `fix` on production files without testing first.
> - `verify` after every fix before committing.

---

## Options

```bash
enc-doctor scan   <path> [--all]       # --all shows clean files too
enc-doctor fix    <path> [--dry-run]   # --dry-run previews without writing
enc-doctor verify <path>
enc-doctor restore <file>              # restore single file from .bak
```

---

## Security

encoding-doctor ships with **zero third-party dependencies** — checked automatically before every release.

| Check | Tool | Result |
|---|---|---|
| Static analysis | `bandit` | 0 high · 0 medium · 0 low severity issues |
| Dependency scan | `pip-audit` | 0 known CVE vulnerabilities |
| Import audit | AST parser | 0 third-party imports — standard library only |

Standard library modules used: `dataclasses`, `json`, `os`, `pathlib`, `platform`, `shutil`, `sys`, `typing`, `urllib`.

---

## Run tests

```bash
pip install pytest
pytest tests/ -v
```

---

## License

MIT © [Stateflow Labs](https://github.com/stateflow-dev)
