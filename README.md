# OwnPay Documentation

Documentation for [OwnPay](https://ownpay.org) — the self-hosted, open-source payment orchestrator licensed under AGPL-3.0. Manage multiple brands, connect to 100+ payment gateways, and provide white-label checkout experiences. Free forever, no transaction fees.

**Live site:** [https://ownpay.org/docs](https://ownpay.org/docs)
**LLM summary:** [llms.txt](llms.txt) — Append `.md` to any page URL for clean Markdown (e.g. `https://ownpay.org/docs/quickstart.md`).
**Branch:** `docs/v2.0`

## Quick start

Install the [Mintlify CLI](https://www.npmjs.com/package/mintlify) and start the local preview:

```bash
npm i -g mintlify
mintlify dev
```
View your local preview at `http://localhost:3000`.

## Validation pipeline

Run these commands before committing changes:

```bash
# Validate MDX and docs.json configuration
mintlify validate

# Check for broken internal links
mintlify broken-links

# Check accessibility
mintlify a11y

# Auto-format MDX files
mintlify format

# Lint prose style (requires Vale)
vale .
```

## Deployment

Mintlify auto-deploys from the `docs/v2.0` branch on push. Nginx reverse-proxies `ownpay.org/docs` to the Mintlify deployment URL.

**Commit convention:** Every commit by an AI agent must include the co-author trailer:

```
Co-authored-by: OwnPay Bot <bot@ownpay.org>
```

## Project structure

```
ownpay-docs-repo/
├── docs.json                     # Mintlify configuration (theme, navigation, SEO, API playground)
├── llms.txt                       # LLM-readable documentation index
├── AGENTS.md                     # AI agent instructions
├── .vale.ini                     # Vale linter configuration
├── README.md                     # This file
│
├── introduction.mdx              # Documentation hub and feature overview
├── quickstart.mdx                # Accept your first payment in 5 minutes
├── installation.mdx              # Production deployment guide
│
├── fundamentals/                 # Core concepts (explanation content)
│   ├── how-ownpay-works.mdx      # End-to-end payment architecture
│   ├── brands.mdx                  # Multi-tenancy and brand isolation
│   ├── payment-flow.mdx           # Transaction lifecycle state machine
│   ├── gateways.mdx               # Gateway types and routing
│   ├── ledger.mdx                  # Double-entry bookkeeping
│   ├── plugins.mdx                # Plugin system architecture
│   └── domains.mdx                # Custom domain setup
│
├── people/                      # User management (how-to content)
│   ├── brands.mdx                  # Create and manage brands
│   ├── staff.mdx                   # Invite and manage team members
│   ├── roles.mdx                   # Permission matrix
│   └── customers.mdx               # Customer profiles and PII
│
├── payments/                    # Payment operations (how-to content)
│   ├── payment-links.mdx          # Shareable payment links
│   ├── transactions.mdx           # View and search transactions
│   ├── refunds.mdx                 # Issue and track refunds
│   ├── invoices.mdx                # Invoice creation
│   └── ledger.mdx                  # Ledger entries UI
│
├── gateways/                    # Gateway setup (how-to content)
│   ├── configuration.mdx           # Set up payment gateways
│   ├── manual-methods.mdx         # Offline/bank transfer methods
│   ├── currencies.mdx              # Multi-currency support
│   └── sms-verification.mdx        # Auto-confirm via SMS parsing
│
├── appearance/                  # UI customization (how-to content)
│   ├── branding.mdx                # Logo and colors
│   ├── themes.mdx                  # Checkout themes
│   └── landing-page.mdx           # Public landing page
│
├── notifications/               # Notification channels (how-to content)
│   ├── email.mdx                   # SMTP and templates
│   ├── webhooks.mdx                # Webhook endpoint management
│   ├── telegram.mdx                # Telegram push alerts
│   └── sms-center.mdx              # SMS log management
│
├── mobile/                      # Companion app (reference + how-to)
│   ├── companion-app.mdx           # Android SMS forwarding app
│   ├── devices.mdx                  # Paired device management
│   └── sms-templates.mdx           # Regex templates for SMS parsing
│
├── reports/                     # Reporting (reference + how-to)
│   ├── dashboard.mdx               # Key metrics and charts
│   ├── audit-log.mdx               # Compliance audit trail
│   ├── balance-verification.mdx    # Ledger reconciliation
│   └── disputes.mdx                # Chargeback management
│
├── system/                      # Admin operations (how-to content)
│   ├── settings.mdx                 # Application configuration
│   ├── domains.mdx                  # DNS and SSL per brand
│   ├── plugins.mdx                 # Plugin manager
│   ├── addons.mdx                  # Addon manager
│   ├── languages.mdx               # Multi-language management
│   └── system-update.mdx           # One-click updates
│
├── security/                    # Access control (how-to + reference)
│   ├── login.mdx                   # Authentication
│   ├── two-factor.mdx              # TOTP 2FA
│   ├── password-reset.mdx          # Password recovery
│   ├── api-keys.mdx                # API key management
│   ├── developer-hub.mdx           # Webhook/API request logs
│   └── my-account.mdx              # Personal settings
│
├── checkout/                    # End-user experience (explanation)
│   └── customer-experience.mdx     # What customers see at checkout
│
├── api/                         # API documentation (reference)
│   ├── overview.mdx                # Base URL, auth, format, rate limits
│   ├── authentication.mdx          # Bearer token and key scopes
│   ├── errors.mdx                  # Error codes and response format
│   ├── webhooks.mdx                # Event types, signatures, retries
│   ├── merchant_api.yaml           # OpenAPI 3.0 spec
│   ├── mobile_api.yaml             # OpenAPI 3.0 spec
│   └── admin_api.yaml             # OpenAPI 3.0 spec
│
├── developer/                   # Developer guide (tutorial + how-to)
│   ├── quickstart.mdx              # Build a payment form
│   ├── testing.mdx                 # Test cards and sandbox
│   ├── webhook-integration.mdx     # End-to-end webhook receiver
│   ├── translations.mdx            # i18n and translations
│   ├── integration/               # SDK guides
│   │   ├── php.mdx                    # Official PHP SDK
│   ├── laravel.mdx                # Laravel package
│   ├── nodejs.mdx                 # TypeScript SDK
│   ├── python.mdx                 # Python integration
│   ├── woocommerce.mdx            # WordPress/WooCommerce
│   └── whmcs.mdx                  # WHMCS payment gateway
│   ├── plugins/                    # Plugin development
│   │   ├── overview.mdx               # Plugin architecture
│   ├── directory-structure.mdx     # File layout
│   ├── manifest.mdx               # manifest.json reference
│   ├── hooks.mdx                   # Hook catalog
│   ├── events.mdx                  # Built-in events
│   ├── capabilities.mdx            # Capability enum
│   ├── lifecycle.mdx               # Install/activate/uninstall
│   └── plugin-types/              # Plugin type guides
│       ├── gateway.mdx                # Build a payment gateway
│       ├── addon.mdx                  # Build an addon
│       ├── theme.mdx                  # Build a checkout theme
│       └── integration.mdx           # Build a third-party integration
│   └── ai/                         # AI tools
│       ├── overview.mdx               # AI integration features
│       ├── mcp.mdx                     # Model Context Protocol server
│       └── skills.mdx                  # Documentation AI skills
│
├── resources/                   # Reference and community
│   ├── features.mdx                # Complete feature list
│   ├── architecture.mdx            # Technical architecture
│   ├── roadmap.mdx                 # Development roadmap
│   ├── ecosystem.mdx               # SDKs, plugins, community
│   ├── security-compliance.mdx     # Encryption, GDPR, PCI
│   ├── performance-scaling.mdx     # Optimization guide
│   ├── backup-export.mdx           # Backup and restore
│   ├── migration-guide.mdx         # Version upgrades
│   ├── rate-limiting.mdx           # API rate limit tiers
│   ├── common-errors.mdx           # Troubleshooting
│   ├── faq.mdx                     # Frequently asked questions
│   ├── debug-mode.mdx              # Debug mode
│   ├── contributing.mdx            # How to contribute
│   ├── code-of-conduct.mdx        # Community standards
│   ├── changelog.mdx               # Release history
│   ├── glossary.mdx                # Terminology
│   └── code-examples.mdx           # Multi-language code samples
│
├── zh/                          # Chinese translations
│   ├── introduction.mdx
│   ├── quickstart.mdx
│   ├── installation.mdx
│   └── fundamentals/
│
└── snippets/                    # Reusable MDX includes
    └── llms-directive.mdx
```

## Navigation tabs

The site uses 4 header tabs defined in `docs.json`:

| Tab | Description |
|-----|-------------|
| **Documentation** | Get Started, Fundamentals, People, Payments, Gateways, Appearance, Notifications, Mobile, Reports, System, Security, Checkout |
| **API Reference** | Overview, Authentication, Errors, Webhooks, plus auto-generated pages from 3 OpenAPI specs |
| **Developer** | Quick Start, Testing, Webhooks, SDK Integrations (PHP, Laravel, Node.js, Python, WooCommerce, WHMCS), Plugin System, AI Tools |
| **Resources** | Features, Architecture, Roadmap, Ecosystem, Security, Performance, Backup, Migration, Rate Limiting, Troubleshooting, FAQ, Community |

## Content framework

Documentation follows the [Diataxis framework](https://diataxis.fr):

- **Tutorials**: `quickstart.mdx`, `developer/quickstart.mdx`
- **How-to guides**: Most pages under people/, payments/, gateways/, system/, security/
- **Reference**: API docs, `payments/transactions.mdx`, `security/api-keys.mdx`, plugin manifest/hooks/events
- **Explanation**: `fundamentals/` pages, `checkout/customer-experience.mdx`

## Writing standards

This project enforces prose style linting with [Vale](https://vale.sh/) using the Microsoft and write-good style packs. Run `vale .` to check.

Key principles from the [Mintlify documentation guide](https://mintlify.com/guides/llms.txt):

- Be concise and use active voice
- Use clear, descriptive headings
- Keep pages self-contained with enough context
- Write for both humans and AI agents
- Use consistent terminology throughout
- Avoid colloquialisms and jargon without definition

## MCP server

OwnPay provides an MCP server for programmatic documentation queries:

- **URL:** `https://ownpay.org/docs/mcp`
- **Docs:** See [AI Tools](/developer/ai/mcp)

## Resources

- [Mintlify documentation](https://mintlify.com/docs)
- [Mintlify writing guide](https://mintlify.com/guides/llms.txt)
- [OwnPay GitHub](https://github.com/own-pay/OwnPay)
- [Support](mailto:ping@ownpay.org)