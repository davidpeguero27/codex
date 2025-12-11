# Utility Scripts

This directory contains various utility scripts for repository maintenance and development.

## Available Scripts

### `debug-codex.sh`

A development helper script for debugging the Codex Extension in VS Code.

**Purpose**: Builds and runs the latest `codex-rs` binary automatically when used as the CLI executable in VS Code settings.

**Usage**:

```bash
./scripts/debug-codex.sh [args...]
```

**Configuration**:
Set this in your VS Code settings to always use the latest development build:

```json
{
  "chatgpt.cliExecutable": "/path/to/codex/scripts/debug-codex.sh"
}
```

---

### `asciicheck.py`

Validates that files contain only ASCII characters (plus an allowed list of Unicode codepoints).

**Purpose**: Ensures consistent character encoding across documentation and prevents issues with special characters that can break regexes or cause rendering problems in Markdown.

**Usage**:

```bash
# Check files for non-ASCII characters
./scripts/asciicheck.py file1.md file2.md

# Fix files by replacing non-ASCII with ASCII equivalents
./scripts/asciicheck.py --fix file1.md file2.md
```

**Substitutions**:

- Non-breaking spaces to regular spaces
- Em/en dashes to hyphens
- Curly quotes to straight quotes
- Ellipsis to three dots

---

### `readme_toc.py`

Verifies and optionally updates the Table of Contents in Markdown files.

**Purpose**: Keeps the Table of Contents in sync with the actual headings in the document. Particularly useful for maintaining README.md files.

**Usage**:

```bash
# Check if ToC is up-to-date (default: README.md)
./scripts/readme_toc.py

# Check a specific file
./scripts/readme_toc.py path/to/file.md

# Update the ToC automatically
./scripts/readme_toc.py --fix
./scripts/readme_toc.py --fix path/to/file.md
```

**Requirements**:
The Markdown file must have ToC markers:

```markdown
<!-- Begin ToC -->

- [Heading 1](#heading-1)
<!-- End ToC -->
```

---

### `stage_npm_packages.py`

Stages npm packages for release by downloading native artifacts and building tarballs.

**Purpose**: Automates the process of preparing npm packages for release, including native binary components.

**Usage**:

```bash
# Stage packages for a release
./scripts/stage_npm_packages.py \
  --release-version 0.6.0 \
  --package codex \
  --package codex-responses-api-proxy \
  --package codex-sdk
```

**Options**:

- `--release-version`: Version to stage (e.g., `0.6.0` or `0.6.0-alpha.1`)
- `--package`: Package name to stage (can be specified multiple times)
- `--workflow-url`: Optional workflow URL to reuse for native artifacts
- `--output-dir`: Directory for npm tarballs (default: `dist/npm`)
- `--keep-staging-dirs`: Retain temporary staging directories

**Output**: Tarballs are written to `dist/npm/` by default.

---

## CI/CD Integration

Many of these scripts are used in GitHub Actions workflows:

- `asciicheck.py` - Used to validate documentation
- `readme_toc.py` - Used to ensure ToC is up-to-date
- `stage_npm_packages.py` - Used in release workflows

## See Also

- [codex-cli/scripts/README.md](../codex-cli/scripts/README.md) - CLI-specific build and packaging scripts
