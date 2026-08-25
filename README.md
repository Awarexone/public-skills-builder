<div align="center">

<img src="https://img.shields.io/badge/Claude_Code-Skill-orange?style=for-the-badge&logo=anthropic&logoColor=white" />
<img src="https://img.shields.io/badge/Bug%20Bounty-HackerOne%20%7C%20GitHub%20Writeups-red?style=for-the-badge" />
<img src="https://img.shields.io/badge/Python-3.10+-blue?style=for-the-badge&logo=python&logoColor=white" />

# Public Skills Builder

**Generate Claude Code bug bounty skills from public HackerOne reports and GitHub writeups - no private reports needed.**

Feed it 500+ public bug bounty reports. Get back 18 ready-to-use Claude Code skill files - one per vulnerability class - packed with real-world techniques, payloads, and bypass patterns.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://python.org)
[![Stars](https://img.shields.io/github/stars/Awarexone/public-skills-builder?style=social)](https://github.com/Awarexone/public-skills-builder/stargazers)

[Quick Start](#quick-start) · [Output](#output) · [Sources](#sources) · [Usage](#usage)

Built and maintained by **AwareXone** - [Website](https://awarexone.com) · [X](https://x.com/awarexone) · [GitHub](https://github.com/Awarexone)

</div>

---

## Why Use This

Bug bounty reports are the best training data for hunting. This tool reads hundreds of disclosed HackerOne reports and community writeups, then uses Claude to distill them into structured skill files you can load directly into Claude Code.

No private reports required. Everything comes from public data.

---

## Quick Start

```bash
git clone https://github.com/Awarexone/public-skills-builder
cd public-skills-builder

python3 -m venv .venv
source .venv/bin/activate
pip install anthropic requests

cp .env.example .env
# Edit .env - add your ANTHROPIC_API_KEY
```

---

## Sources

| Source | Auth needed | What it fetches |
|--------|-------------|-----------------|
| HackerOne public feed | None | Publicly disclosed reports |
| HackerOne REST API | H1 API key | Your own resolved reports |
| GitHub writeup repos | None (optional token) | 1,200+ community writeups |

---

## Output

One markdown skill file per vulnerability class, ready to load into Claude Code:

```
skills/
  hunt-idor.md
  hunt-ssrf.md
  hunt-xss.md
  hunt-rce.md
  hunt-oauth.md
  hunt-sqli.md
  hunt-business-logic.md
  ... (18 vuln classes total)
  README.md  ← index of all skills
```

Each skill file contains:
- Crown jewel targets
- Attack surface signals
- Step-by-step hunting methodology
- Payloads and grep patterns
- Bypass techniques
- Gate 0 validation checklist

---

## Usage

```bash
# Public GitHub writeups only (just needs Claude API key)
python3 public_skills_builder.py --source github

# HackerOne public disclosed reports (no H1 key needed)
python3 public_skills_builder.py --source h1-public

# Everything - all sources, all vuln classes
python3 public_skills_builder.py --source all --limit 500

# Specific vuln classes only
python3 public_skills_builder.py --vuln-type idor ssrf xss oauth

# Specific H1 program
python3 public_skills_builder.py --source h1 --program shopify --limit 200
```

---

## Supported Vuln Classes

`idor` `ssrf` `xss` `sqli` `rce` `auth-bypass` `oauth` `race-condition`
`business-logic` `graphql` `cache-poison` `xxe` `upload` `ssti` `csrf`
`subdomain` `llm-ai` `crypto`

---

## Using the Skills in Claude Code

Once generated, load a skill into Claude Code by pointing it at the file:

```bash
claude
# Then: "Load skills/hunt-idor.md and help me hunt IDOR on target.com"
```

Or copy skill files into your Claude Code project's `.claude/` directory so they load automatically.

---

## Requirements

- Python 3.10+
- `ANTHROPIC_API_KEY` - from [console.anthropic.com](https://console.anthropic.com)
- `H1_API_KEY` - optional, from [hackerone.com/settings/api_token](https://hackerone.com/settings/api_token)
- `GITHUB_TOKEN` - optional, increases GitHub API rate limits

---

## Legal

For authorized security testing only. Only test targets within an approved bug bounty program scope.

---

<div align="center">

MIT License · Built for bug hunters who learn from the community

**Star if this saved you research time**

</div>
