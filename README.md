# dwebsite-plugin

> Claude Code plugin for dWebsite development with auto-deployment to `vibe3.link`

**Version:** 3.0.1

## MCP Tools

| Server | Purpose |
|--------|---------|
| `openzeppelin-contracts` | Smart contract references and best practices |
| `vibe3-mcp` | VIBE3 backend integration (deployment info, preview images) |
| `playwright` | Headless browser for screenshots and testing |

## Skills

| Skill | Trigger | Purpose |
|-------|---------|---------|
| **copywriting** | "write copy for", "improve this copy" | Marketing content, CTAs, page copy |
| **design-system** | Building component libraries | Tailwind v4, CVA components, dark mode |
| **foundry** | Solidity development | Forge, Cast, Anvil, Chisel |
| **frontend-design** | "build web components", "create interface" | Distinctive, non-generic UI design |
| **landing-page** | Landing page design | High-conversion page structure |
| **react-best-practices** | Writing/reviewing React code | Performance optimization (30+ rules) |
| **remotion-best-practices** | Video creation in React | Remotion patterns (30+ rules) |

## Deploy Command

The `/deploy` command handles the full deployment pipeline:

```
Generate slug → Vercel deploy → Set alias → Screenshot → Update VIBE3 API
```

Deploys are aliased to `https://<slug>.vibe3.link` subdomains.

## File Structure

```
dwebsite-plugin/
├── .claude-plugin/
│   └── plugin.json          # Plugin manifest (name, version)
├── .mcp.json                # MCP server configurations
├── commands/
│   └── deploy.md            # /deploy command definition
└── skills/
    ├── copywriting/         # Marketing copy guidance
    ├── design-system/       # Tailwind v4 + component patterns
    ├── foundry/             # Solidity toolchain (Forge, Cast, Anvil)
    ├── frontend-design/     # UI/UX design principles
    ├── landing-page/        # Landing page optimization
    ├── react-best-practices/  # React/Next.js performance (30+ rules)
    └── remotion-best-practices/ # Video creation patterns (30+ rules)
```
