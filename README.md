<p align="center">
  <img src="assets/a2wf-logo.png" alt="A2WF Logo" width="180">
</p>

<h1 align="center">A2WF Skill for OpenClaw</h1>

<p align="center">
  <strong>Validate, generate, and audit <code>siteai.json</code> files — the open standard for AI agent governance on websites.</strong>
</p>

<p align="center">
  <a href="https://a2wf.org"><img alt="A2WF v1.0" src="https://img.shields.io/badge/A2WF-v1.0-blue?style=flat-square"></a>
  <a href="https://github.com/openclaw/openclaw"><img alt="OpenClaw Compatible" src="https://img.shields.io/badge/OpenClaw-compatible-green?style=flat-square"></a>
  <a href="LICENSE"><img alt="MIT License" src="https://img.shields.io/badge/license-MIT-yellow?style=flat-square"></a>
</p>

---

## What is A2WF?

**A2WF (Agent-to-Web Framework)** defines what AI agents can and cannot do on your website through a machine-readable `siteai.json` file. Think of it as a **legally actionable robots.txt for AI agents**.

Without A2WF, you can't prove an AI agent violated your rules. With A2WF, you have a dated, machine-readable policy that turns a suggestion into evidence.

→ **[Read the full specification at a2wf.org](https://a2wf.org/specification/)**

## Installation

### Via ClawHub (recommended)

```bash
clawhub install a2wf
```

### Manual

Clone this repo into your OpenClaw workspace skills folder:

```bash
git clone https://github.com/a2wf/openclaw-skill.git ~/.openclaw/workspace/skills/a2wf
```

## Features

### 🔍 Validate

Check any website or `siteai.json` file against the A2WF v1.0 specification:

```
> "Validate the siteai.json of example.com"
```

```bash
# CLI usage
node scripts/validate.mjs https://example.com
node scripts/validate.mjs /path/to/siteai.json
```

Returns errors, warnings, and a compliance score (0–100).

### ⚡ Generate

Create a spec-compliant `siteai.json` from templates:

```
> "Generate a siteai.json for my e-commerce store at shop.example.com"
```

```bash
# CLI usage
node scripts/generate.mjs \
  --domain "https://shop.example.com" \
  --name "My Shop" \
  --category ecommerce \
  --jurisdiction EU \
  --law "GDPR,EU AI Act"
```

**Built-in templates:** `ecommerce` · `banking` · `healthcare` · `news-media` · `restaurant` · `saas`

### 🛡️ Audit

Full compliance audit with discovery check, schema validation, permission analysis, and legal coverage:

```
> "Audit the A2WF compliance of my-site.com"
```

```bash
node scripts/validate.mjs https://my-site.com --audit
```

## Example Output

```json
{
  "valid": true,
  "score": 96,
  "errors": [],
  "warnings": [
    { "path": "$.identity.jurisdiction", "message": "No jurisdiction declared" }
  ],
  "summary": "✅ Valid A2WF v1.0 document (score: 96/100)"
}
```

## siteai.json Quick Reference

```json
{
  "specVersion": "1.0",
  "identity": {
    "domain": "https://example.com",
    "name": "Example Site",
    "inLanguage": "en",
    "jurisdiction": "EU",
    "applicableLaw": ["GDPR", "EU AI Act"]
  },
  "permissions": {
    "read":   { "pricing": { "allowed": true, "rateLimit": 60 } },
    "action": { "createAccount": { "allowed": false } },
    "data":   { "customerRecords": { "allowed": false } }
  }
}
```

| Permission Group | What it controls | Examples |
|:---|:---|:---|
| **read** | What agents can read | pricing, reviews, FAQ, contact info |
| **action** | What agents can do | search, checkout, create accounts |
| **data** | What data agents access | customer records, payment info |

## For Agent Developers

If you're building an AI agent that browses websites, check for `/siteai.json` before taking actions. See [`references/implementer-guide.md`](references/implementer-guide.md) for the complete integration guide.

## Links

- 🌐 [a2wf.org](https://a2wf.org) — Official website
- 📋 [A2WF Specification](https://a2wf.org/specification/) — Full spec
- 🔧 [a2wf/spec](https://github.com/a2wf/spec) — Schema, validator, examples
- 🦞 [OpenClaw](https://github.com/openclaw/openclaw) — AI agent platform

## License

MIT — see [LICENSE](LICENSE).
