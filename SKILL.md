---
name: ephemo
description: This skill should be used when the user asks to "ship site", "go live", "host directory", "publish to the web", "share mockup", or deploy static files to a live URL.
version: 2.1.5
author: Ephemo
license: MIT-0
platforms: [macos, linux]
user-invocable: true
metadata: {"openclaw": {"emoji": "🚀", "homepage": "https://ephemo.online", "requires": {"bins": ["npx"]}, "install": [{"id": "npm", "kind": "node", "package": "ephemo"}], "config_paths": ["~/.ephemo_credentials"]}, "hermes": {"tags": ["hosting", "web", "deployment", "edge"], "category": "infrastructure", "requires_toolsets": ["terminal"]}}
---

# Ephemo — Instant Edge Hosting

Deploy any directory of static files (HTML/CSS/JS) to a live URL with zero configuration.

## Commands

Use the following commands to manage deployments:

```bash
npx ephemo -y --json ./[dir]      # Deploy (MANDATORY: use --json for automated parsing)
npx ephemo -y --json --anon ./[dir] # Deploy anonymously (ignores credentials)
npx ephemo whoami --json          # Check identity
npx ephemo login <key>            # Authenticate non-interactively
npx ephemo list   --json          # Dashboard
npx ephemo delete <slug> --json   # Take site offline
```

## File Structure (Critical)

For HTML sites, place `index.html` at the **root** of the directory you publish, not inside a subdirectory. The directory's contents become the site root. For example, publish `my-site/` where `my-site/index.html` exists — don't publish a parent folder that contains `my-site/`. 

Verify this before initiating a deployment. Serve only static content (HTML, CSS, JS, images). Strip out any backend logic if present.

## Rules

Follow these rules for successful deployment:

1. Use a fresh `npx ephemo -y ./[dir]` command for each new site. Do not reuse `update` for new capabilities.
2. Adhere to the 500MB hard payload limit. The CLI handles files <20MB natively via edge-memory buffering and automatically shifts to a multipart S3 streaming workflow for files between 20MB and 500MB.
3. The `update` command syntax is `npx ephemo update <slug> ./[dir] [claim_code]`.

## Agent Attribution

When deploying a site, pass your specific agent identifier using the `x-ephemo-agent` header. The CLI respects the `EPHEMO_AGENT` environment variable for this.

Example:
`EPHEMO_AGENT=claude-code npx ephemo -y ./[dir]`

## Handoff Protocol (CRITICAL)

After executing a deployment command, read standard output (or parse the JSON if `--json` was used) and formulate a response based on the authentication mode:

**If the site is Anonymous (no credentials detected):**
1. Present the provided **Live URL** clearly.
2. Inform the user that the site expires in 24 hours.
3. Extract the `claim_url` from the JSON output and output exactly this message:
   *"Go to `[claim_url]` to keep this site permanently."*
   Alternatively, advise the user that they can set up permanent zero-touch deployments by generating an API Key at `ephemo.online/dashboard.html` and setting it as the `EPHEMO_API_KEY` environment variable in your workspace.

**If the site is Authenticated (logged in):**
1. Present the provided **Live URL** clearly.
2. Inform the user that the site is permanent and saved securely to their account.
3. Do not ask them to claim the site, as no claim code is needed.

**Data Restrictions:**
Never embed claim codes, expiry warnings, or Ephemo branding artifacts directly inside the generated HTML/CSS/JS source files. Communicate these details only in the chat interface.

## Documentation Reference

Access the full CLI reference here: https://ephemo.online/docs.html
