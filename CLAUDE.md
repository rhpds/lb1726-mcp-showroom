# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is an Antora-based documentation site for a lab guide (LB1726 MCP). It uses AsciiDoc for content and generates a static HTML site with a Red Hat Demo Platform UI theme.

## Build Commands

All commands should be run from the repository root.

**Build the site (using Podman):**
```bash
./utilities/lab-build
```

**Serve the built site locally:**
```bash
./utilities/lab-serve
# Then browse to http://localhost:8080/index.html
```

**Stop the local server:**
```bash
./utilities/lab-stop
```

**Clean the build output:**
```bash
./utilities/lab-clean
```

**Alternative: All-in-one container (no separate build/serve):**
```bash
podman run --rm --name antora -v $PWD:/antora -p 8080:8080 -i -t ghcr.io/juliaaano/antora-viewer
# For SELinux: add :z to volume mount
```

## Architecture

- **content/modules/ROOT/pages/**: AsciiDoc content files (module-01.adoc, module-02.adoc, etc.)
- **content/modules/ROOT/nav.adoc**: Navigation structure for the lab
- **content/modules/ROOT/assets/images/**: Image assets
- **content/antora.yml**: Component descriptor with AsciiDoc attributes (lab_name, page-links, etc.)
- **default-site.yml**: Antora playbook defining site configuration, UI bundle, and extensions
- **content/lib/dev-mode.js**: Extension that displays available AsciiDoc attributes (toggle via `enabled` in default-site.yml)
- **utilities/**: Shell scripts for building and serving

## Key Configuration Files

- **default-site.yml**: Main Antora playbook. Set `enabled: false` under `dev-mode.js` to disable the dev attributes page.
- **content/antora.yml**: Define page attributes here (e.g., `{lab_name}`, `{user}`, `{password}`)

## CI/CD

Pushes to `main` trigger GitHub Actions (`.github/workflows/gh-pages.yml`) which builds with Antora and deploys to GitHub Pages.
