# Documentation project instructions

## About this project

- This is a documentation site built on [Mintlify](https://mintlify.com)
- Pages are MDX files with YAML frontmatter
- Configuration lives in `docs.json` (NEVER use `mint.json` — it is deprecated)
- Live at `https://ownpay.org/docs` (proxied via Nginx to `ownpay.mintlify.dev`)
- GitHub repo: `own-pay/ownpay-docs` (master branch)
- Pushes to `master` auto-deploy to Mintlify
- Full `docs.json` schema at [mintlify.com/docs.json](https://mintlify.com/docs.json)

## Navigation structure

The site uses 4 header tabs:

| Tab | Content |
|-----|---------|
| **Documentation** | Get Started, Fundamentals, People, Payments, Gateways & Currencies, Appearance, Notifications, Mobile, Reports & Finance, System, Security & Access, Checkout |
| **API Reference** | Overview, Authentication, Errors, Webhooks, Merchant API (auto-gen), Mobile API (auto-gen), Admin API (auto-gen) |
| **Developer** | Getting Started, SDKs & Libraries (PHP, Laravel, Node.js, Python, WooCommerce, WHMCS), Plugin System, Building Plugins, Translations, AI Tools |
| **Resources** | About (Features, Architecture, Roadmap, Ecosystem), Advanced (Security, Performance, Backup, Migration, Rate Limiting), Troubleshooting (Errors, FAQ, Debug Mode), Community (Contributing, Code of Conduct, Changelog, Glossary), Code Examples |

There is also a global anchor for Changelog.

## Canonical content locations (never duplicate)

| Topic | Canonical Page | Pages that link to it |
|-------|---------------|---------------------|
| API authentication | `/api/authentication` | `/api/overview`, `/security/api-keys`, `/developer/quickstart` |
| Webhook signature verification | `/api/webhooks` | `/developer/webhook-integration`, `/notifications/webhooks` |
| Transaction statuses | `/fundamentals/payment-flow` | `/payments/transactions`, `/payments/refunds`, `/developer/quickstart` |
| Brand concept | `/fundamentals/brands` | `/people/brands`, `/fundamentals/domains` |
| Gateway concept | `/fundamentals/gateways` | `/gateways/configuration`, `/gateways/manual-methods` |
| Ledger concept | `/fundamentals/ledger` | `/payments/ledger`, `/reports/balance-verification` |
| Rate limiting | `/resources/rate-limiting` | `/api/overview`, `/security/developer-hub` |
| Error codes | `/api/errors` | `/api/overview`, `/resources/common-errors` |
| API endpoint list | `/api/overview` + OpenAPI YAMLs | No other page lists endpoints |
| Payment creation code | `/resources/code-examples` | `/developer/quickstart`, all SDK pages |

## Page frontmatter guidelines

Every page requires frontmatter:

```yaml
---
title: "Page Title"  # H1, required — generates the page heading automatically
sidebarTitle: "Short Title"  # Sidebar display, required
description: "One sentence description for search engines"  # 120-160 chars
keywords: ["ownpay", "payment", "gateway"]  # 4-8 terms
---
```

- **NEVER add a manual H1** — Mintlify generates it from the `title` frontmatter
- Use `boost: 3-5` in frontmatter for high-value SEO pages
- Use `searchable: false` only for pages that should be hidden from in-product search
- Diataxis classification per page: Tutorial, How-to, Reference, or Explanation

## Writing rules

1. **Second person** ("you") — never first person plural ("we") or third person
2. **Active voice** — "Click Save" not "The Save button should be clicked"
3. **Sentence case headings** — "Getting started" not "Getting Started"
4. **Short sentences** — max 25 words; break complex ideas
5. **Intent-oriented headings** — "Create a brand" not "Brands"
6. **Minimum 300 words** per page; reference pages minimum 200 words
7. **Code examples** must be complete and runnable (not pseudocode)
8. **Tables** for structured data; **bullet lists** for unstructured items
9. **No orphan headings** — every heading must have content under it
10. **Root-relative links** (e.g., `/quickstart`) — do NOT use `/docs` prefix
11. **Every page** ends with a `## Related Pages` section linking to 3-5 relevant pages

## Mintlify components to use

| Page Type | Components |
|-----------|------------|
| Installation | `<Steps>`, `<Tabs>` (platform), `<Callout>` |
| How-to | `<Steps>`, `<Note>`/`<Warning>`, `<CodeGroup>` |
| Concept/Explanation | `<Accordion>`, `<Mermaid>`, `<Card>`+`<Columns>` |
| API reference | `<RequestExample>`, `<ResponseExample>` |
| Plugin docs | `<Tree>`, `<Badge>` |
| Quick Start | `<Card>`+`<Columns>`, `<Steps>` |
| FAQ/Troubleshooting | `<Accordion>`, `<AccordionGroup>` |

## Variables available

- `{{version}}` — current version (0.2.0)
- `{{github}}` — GitHub repo URL
- `{{website}}` — ownpay.org URL
- `{{docsUrl}}` — documentation URL
- `{{supportEmail}}` — support email

## Files that are auto-synced from main repo

DO NOT edit these files directly — changes will be overwritten:
- `resources/features.mdx` (from docs/FEATURES.md)
- `resources/architecture.mdx` (from docs/ARCHITECTURE.md)
- `resources/roadmap.mdx` (from ROADMAP.md)
- `resources/contributing.mdx` (from CONTRIBUTING.md)
- `resources/local-setup.mdx` (from docs/LOCAL_SETUP.md)
- `resources/changelog.mdx` (from CHANGELOG.md)
- `developer/translations.mdx` (from docs/TRANSLATIONS.md)

## Diataxis framework

| Type | User Goal | Example Pages |
|------|-----------|---------------|
| **Tutorial** | Learn through practice | `/quickstart`, `/developer/quickstart`, `/developer/webhook-integration` |
| **How-to** | Solve a specific task | All `/payments/`, `/gateways/`, `/system/` pages |
| **Reference** | Find precise info | `/api/authentication`, `/api/errors`, `/resources/rate-limiting` |
| **Explanation** | Understand a concept | All `/fundamentals/` pages, `/resources/architecture` |

## MCP servers

All MCP servers are configured in `.mcp.json`:
- `mintlify` — Edit OwnPay docs content and settings via Mintlify dashboard
- `mintlify-docs` — Query Mintlify documentation for component syntax and features
- `mintlify-guides` — Advanced documentation patterns and best practices

## Key technical details about OwnPay

- **Stack**: PHP 8.3, MySQL 8, Redis, Twig 3, vanilla JS, custom framework (NOT Laravel/Symfony)
- **Money**: bcmath extension, all amounts as strings to avoid float precision issues
- **Encryption**: AES-256-GCM for PII (API keys, gateway credentials, customer data)
- **Webhooks**: HMAC-SHA256 signature, retry schedule: immediate, 1m, 5m, 30m, 2h, 6h
- **Auth**: Bearer API key with scopes (read, write, admin)
- **Multi-tenancy**: Brands are isolated tenants with own gateways, domains, branding, staff, ledger
- **Plugins**: 4 types (gateway, addon, theme, integration), sandbox-scanned, manifest-based
- **Companion App**: Android app for SMS auto-verification of mobile money payments
- **License**: AGPL-3.0, zero transaction fees