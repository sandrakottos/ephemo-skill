---
name: ephemo
description: Deploy static files to a live URL instantly. Use when asked to publish, host, deploy, share, or put something online. Outputs a shareable URL in seconds.
version: 2.1.0
author: Ephemo
license: MIT-0
platforms: [macos, linux]
user-invocable: true
metadata: {"openclaw": {"emoji": "🚀", "homepage": "https://ephemo.online", "requires": {"bins": ["npx"]}, "install": [{"id": "npm", "kind": "node", "package": "ephemo"}], "config_paths": ["~/.ephemo_credentials"]}, "hermes": {"tags": ["hosting", "web", "deployment", "edge"], "category": "infrastructure", "requires_toolsets": ["terminal"]}}
---

# Ephemo — Instant Edge Hosting

Deploy any directory of static files (HTML/CSS/JS) to a live URL. Zero config.

## Commands

```bash
npx ephemo -y ./[dir]           # Deploy (always use -y to skip prompts)
npx ephemo login                # Auth via OTP → saves key to ~/.ephemo_credentials
npx ephemo list                 # Show all your sites
npx ephemo update <slug> ./[dir] [claim_code]  # Overwrite / resurrect a site
npx ephemo delete <slug>        # Take offline (soft delete, reversible)
```

## Rules

1. **New site = new command.** Always `npx ephemo -y ./[dir]`. Never reuse `update` for new sites.
2. **Pre-flight:** Verify `index.html` exists at the root of the target directory before deploying.
3. **Static only.** HTML/CSS/JS/images. No backends. If user has server code, extract the front-end first.
4. **25MB hard limit.** Move heavy media to an external CDN and reference by URL.

## Handoff Protocol (CRITICAL)

After deploying, parse stdout and report to the user:

- **Always:** Share the **Live URL** in bold.
- **If anonymous (no credentials):** Site expires in 24h. Provide the 8-char **CLAIM CODE** and say: *"Go to ephemo.online/claim.html and submit code `[CODE]` to keep this site permanently."*
- **If authenticated:** Say the site is **permanent**. No claim code needed.
- **NEVER** embed claim codes, expiry warnings, or Ephemo branding inside the deployed HTML/CSS/JS files.

## Docs

Full reference: https://ephemo.online/docs.html
