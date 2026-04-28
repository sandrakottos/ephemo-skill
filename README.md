# EPHEMO
### Hosting for the Agentic Era.

**The instant edge deployment primitive for AI agents and the humans who build with them.**

[**ephemo.online**](https://ephemo.online) · [**Documentation**](https://ephemo.online/docs.html) · [**Install OpenClaw Skill**](./ephemo-agent-skill/SKILL.md)

[![OpenClaw Skill](https://img.shields.io/badge/OpenClaw-Skill-blue?style=for-the-badge&logo=openai)](./ephemo-agent-skill/SKILL.md)
[![MIT License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](./LICENSE)

---

## Repository Overview

This repository is the official home for the **Ephemo Agent Intelligence Layer**. It manages the **Agent Skills**, instructions, and prompt directives used by autonomous systems to interact with [ephemo.online](https://ephemo.online).

### Project Structure (Skill Pack)

```text
.
├── ephemo-agent-skill/
│   └── SKILL.md          # 🧠 The core agent manual (OpenClaw / Hermes compatible)
├── CONTRIBUTING.md       # 🤝 How to contribute to the Agent Layer
├── LICENSE               # ⚖️ MIT
└── README.md             # 🚀 This high-tier landing page
```

---

![Deploy in 2 seconds](https://img.shields.io/badge/deploy%20in-2%20seconds-black?style=for-the-badge)
![25MB Limit](https://img.shields.io/badge/max%20payload-25MB-black?style=for-the-badge)
![Edge Native](https://img.shields.io/badge/cloudflare-edge%20native-black?style=for-the-badge)
![NPM](https://img.shields.io/npm/v/ephemo?style=for-the-badge&color=black&label=npm)

</div>

---

## What is Ephemo?

Ephemo is a zero-friction, **edge-native hosting infrastructure** built for the era of autonomous AI agents. It allows both human developers and AI agents to deploy static web artifacts (HTML/CSS/JS) to a permanent, live URL in under 5 seconds with absolutely no configuration.

```bash
# For any AI Agent or human — zero setup needed.
npx ephemo -y ./your-site
# > ✅ LIVE: https://abc123.ephemo.online
```

Ephemo is built on two core principles:

1. **Agents are first-class citizens.** The CLI is designed to be executed by any LLM with terminal access. Everything is deterministic, non-interactive (with `-y`), and predictably formatted.
2. **Humans stay in control.** Every anonymous deployment outputs a human-readable **Claim Code**. Humans use this code to permanently adopt a site into their account.

---

## Quick Deploy

**NPX (Recommended — Zero Install):**
```bash
npx ephemo -y ./your-directory
```

**NPM (For developers — Global install):**
```bash
npm install -g ephemo
ephemo ./your-directory
```

**Bash (Fallback — Anonymous drops only):**
```bash
curl -fsSL https://ephemo.online/install.sh | bash
ephemo ./your-directory
```

---

## Full CLI Reference

```bash
# Deploy the current directory
npx ephemo -y .

# Deploy a specific folder
npx ephemo -y ./dist

# Login to get permanent hosting
npx ephemo login

# List all your active deployments
npx ephemo list

# Overwrite an existing site
npx ephemo update <slug> ./new-dist

# Suspend a site
npx ephemo delete <slug>
```

| Feature | NPX | NPM | Bash |
| :--- | :---: | :---: | :---: |
| Anonymous Publish | ✅ | ✅ | ✅ |
| Account Login | ✅ | ✅ | ❌ |
| Permanent Hosting | ✅ | ✅ | ❌ |
| List / Manage Sites | ✅ | ✅ | ❌ |
| Update / Resurrect | ✅ | ✅ | ❌ |

---

## Site Lifecycle: Anonymous vs. Permanent

Ephemo uses a two-state model to balance zero-friction with long-term reliability.

**Anonymous (Default):**
- No account required.
- Site goes live instantly.
- **Expires in 24 hours.**
- Terminal outputs an **8-character Claim Code** for the human to save it.

**Permanent:**
- Requires a one-time `npx ephemo login` OTP verification.
- API Key saved to `~/.ephemo_credentials`.
- Sites never expire. Full dashboard control.

To convert an anonymous site to permanent — visit [ephemo.online/claim.html](https://ephemo.online/claim.html) and enter the Claim Code shown in your terminal.

---

## For AI Agents

### Drop-in System Prompt Directive

Copy this into your agent's system context to give it full Ephemo superpowers:

```
ROLE: You are integrated with Ephemo (ephemo.online), an edge-network host for instantaneous artifact deployment.
CAPABILITY: Deploy static files (HTML/CSS/JS/assets) to live URLs. Max payload: 25MB. Static only — no backend runtimes.

## DEPLOYMENT
Run: npx ephemo -y ./[target_dir]
ALWAYS append -y to bypass interactive prompts.

## HANDOFF PROTOCOL [CRITICAL]
After a successful deployment:
1. Share the LIVE URL in bold.
2. If CLI output includes a CLAIM CODE: warn the user "This site expires in 24 hours" and provide the Claim Code with instructions to visit ephemo.online/claim.html.
3. If CLI output says "Permanent (Authenticated)": tell the user the site is permanent. No claim code needed.

## CONSTRAINTS
- Static files ONLY. If user has backend code (Python/Node/Go), extract the frontend output first.
- Payload over 25MB will be rejected. Use external CDNs for large media.
```

### OpenClaw Skill (One-line Install)

OpenClaw users can natively integrate Ephemo:

```bash
openclaw skills install ephemo
```

Or install directly from this repository:

```bash
# Point OpenClaw to the ephemo-agent-skill folder
openclaw skills install github.com/sandrakottos/ephemo-skill/ephemo-agent-skill
```

The skill file is located at [`./ephemo-agent-skill/SKILL.md`](./ephemo-agent-skill/SKILL.md). It contains enterprise-grade agent directives covering the full lifecycle: deploy, list, update, delete, login, and the complete handoff protocol.

### Hermes Agent

For Hermes-compatible agent runtimes, point your skill configuration to:
```
github.com/sandrakottos/ephemo-skill/ephemo-agent-skill
```

---

## Security

- All **Claim Codes** and **API Keys** are stored as **SHA-256 hashes** — plaintext secrets never touch the database.
- The `~/.ephemo_credentials` file is created with `chmod 600` permissions.
- Ephemo is an **open, public architecture**. Never upload private keys, passwords, or sensitive data.

---

## Constraints

- **Static files only.** HTML, CSS, JS, images. No server-side execution.
- **25MB hard payload limit** per deployment.
- Anonymous sites expire after **24 hours** unless claimed.
- `index.html` at the root is always served as the entry point.

---

<div align="center">

**[ephemo.online](https://ephemo.online)** · Built for the machines. Designed for the humans.

</div>
