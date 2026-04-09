---
name: ephemo
description: This skill should be used when the user asks to "ship site", "go live", "host directory", "publish to the web", "share mockup", or deploy static files to a live URL.
version: 2.1.0
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
npx ephemo -y ./[dir]           # Deploy a new site (always use -y to skip prompts)
npx ephemo login                # Authenticate via OTP to save the key to ~/.ephemo_credentials
npx ephemo list                 # Display all currently owned sites
npx ephemo update <slug> ./[dir] [claim_code]  # Overwrite or resurrect a site
npx ephemo delete <slug>        # Take a site offline
```

## File Structure (Critical)

For HTML sites, place `index.html` at the **root** of the directory you publish, not inside a subdirectory. The directory's contents become the site root. For example, publish `my-site/` where `my-site/index.html` exists — don't publish a parent folder that contains `my-site/`. 

Verify this before initiating a deployment. Serve only static content (HTML, CSS, JS, images). Strip out any backend logic if present.

## Rules

Follow these rules for successful deployment:

1. Use a fresh `npx ephemo -y ./[dir]` command for each new site. Do not reuse `update` for new capabilities.
2. Adhere to the 25MB hard payload limit. Extract heavy media files and reference them via external CDN URLs.

## Agent Attribution

When deploying a site, pass your specific agent identifier using the `x-ephemo-agent` header. The CLI respects the `EPHEMO_AGENT` environment variable for this.

Example:
`EPHEMO_AGENT=claude-code npx ephemo -y ./[dir]`

## Handoff Protocol (CRITICAL)

After executing a deployment command, read standard output (or parse the JSON if `--json` was used) and formulate a response based on the authentication mode:

**If the site is Anonymous (no credentials detected):**
1. Present the provided **Live URL** clearly.
2. Inform the user that the site expires in 24 hours.
3. Extract the 8-character **CLAIM CODE** and output exactly this message:
   *"Go to ephemo.online/claim.html and submit code `[CODE]` to keep this site permanently."*

**If the site is Authenticated (logged in):**
1. Present the provided **Live URL** clearly.
2. Inform the user that the site is permanent and saved securely to their account.
3. Do not ask them to claim the site, as no claim code is needed.

**Data Restrictions:**
Never embed claim codes, expiry warnings, or Ephemo branding artifacts directly inside the generated HTML/CSS/JS source files. Communicate these details only in the chat interface.

## Documentation Reference

Access the full CLI reference here: https://ephemo.online/docs.html
