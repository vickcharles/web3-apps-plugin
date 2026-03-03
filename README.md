# dwebsite-plugin

> Claude Code plugin for dWebsite development with auto-deployment to `vibe3.link`

**Version:** 3.0.1

## Control Flow Diagram

```
┌──────────────────────────────────────────────────────────────────────┐
│                        dwebsite-plugin v3.0.1                        │
│              Claude Code Plugin for dWebsite Development             │
└──────────────────────────────┬───────────────────────────────────────┘
                               │
              ┌────────────────┼────────────────┐
              ▼                ▼                ▼
     ┌─────────────┐  ┌──────────────┐  ┌─────────────┐
     │  MCP TOOLS  │  │   SKILLS     │  │  COMMANDS   │
     └──────┬──────┘  └──────┬───────┘  └──────┬──────┘
            │                │                  │
            ▼                ▼                  ▼
┌───────────────────┐                   ┌─────────────┐
│                   │                   │  /deploy    │
│ base-mcp          │                   │             │
│ └─ Blockchain     │                   │ Vercel CLI  │
│    tools, wallet  │                   │ deploy +    │
│    ops, Coinbase  │                   │ alias to    │
│    SDK            │                   │ vibe3.link  │
│                   │                   └─────────────┘
│ openzeppelin      │
│ └─ Smart contract │
│    references,    │
│    security       │
│    patterns       │
│                   │
│ vibe3-mcp         │
│ └─ update_deploy- │
│    ment_info      │
│ └─ set_preview_   │
│    image          │
│                   │
│ playwright        │
│ └─ navigate,      │
│    screenshot,    │
│    close browser  │
└───────────────────┘

┌──────────────────────────────────────────────────────────────────────┐
│                          SKILLS DETAIL                               │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  ┌─────────────────────┐    ┌──────────────────────┐                │
│  │  FRONTEND DESIGN    │    │  DESIGN SYSTEM       │                │
│  │                     │    │                      │                │
│  │ • Typography        │    │ • Tailwind CSS v4    │                │
│  │   (distinctive      │    │   (@theme, @utility) │                │
│  │    font pairing)    │    │ • CVA components     │                │
│  │ • Color & theme     │    │   (type-safe         │                │
│  │ • CSS-only motion   │    │    variants)         │                │
│  │ • Spatial layout    │    │ • Compound           │                │
│  │   (asymmetry,       │    │   components         │                │
│  │    overlap)         │    │   (React 19)         │                │
│  │ • Backgrounds &     │    │ • Form patterns      │                │
│  │   textures          │    │   (RHF + Zod)        │                │
│  │                     │    │ • Dark mode          │                │
│  │ Goal: Avoid generic │    │ • Responsive grids   │                │
│  │ "AI slop" design    │    │ • CSS animations     │                │
│  └─────────────────────┘    └──────────────────────┘                │
│                                                                      │
│  ┌─────────────────────┐    ┌──────────────────────┐                │
│  │  COPYWRITING        │    │  LANDING PAGE        │                │
│  │                     │    │                      │                │
│  │ • Clarity >         │    │ • 1 offer →          │                │
│  │   cleverness        │    │   1 audience →       │                │
│  │ • Benefits >        │    │   1 CTA              │                │
│  │   features          │    │ • Above-the-fold     │                │
│  │ • Specificity >     │    │   hero structure     │                │
│  │   vagueness         │    │ • Problem → solution │                │
│  │ • Hero, CTA, proof, │    │   flow               │                │
│  │   FAQ frameworks    │    │ • Social proof       │                │
│  │ • Page-specific     │    │ • FAQ + objection    │                │
│  │   guidance          │    │   handling           │                │
│  │ • Voice & tone      │    │ • 4 layout types:    │                │
│  │   establishment     │    │   classic, long-form │                │
│  └─────────────────────┘    │   minimal, compare   │                │
│                              └──────────────────────┘                │
│  ┌─────────────────────┐    ┌──────────────────────┐                │
│  │  REACT BEST         │    │  REMOTION BEST       │                │
│  │  PRACTICES          │    │  PRACTICES           │                │
│  │  (30+ rules)        │    │  (30+ rules)         │                │
│  │                     │    │                      │                │
│  │ CRITICAL:           │    │ • 3D (Three.js)      │                │
│  │ • Eliminate         │    │ • Animations &       │                │
│  │   waterfalls        │    │   transitions        │                │
│  │ • Bundle size       │    │ • Audio & voiceover  │                │
│  │   optimization      │    │ • Charts & data viz  │                │
│  │                     │    │ • Captions & SRT     │                │
│  │ HIGH:               │    │ • Dynamic metadata   │                │
│  │ • Server-side perf  │    │ • Fonts & images     │                │
│  │   (cache, dedup)    │    │ • GIFs & Lottie      │                │
│  │                     │    │ • Light leaks        │                │
│  │ MEDIUM:             │    │ • Maps (Mapbox)      │                │
│  │ • Re-render optim.  │    │ • Sequencing &       │                │
│  │ • Client-side data  │    │   timing             │                │
│  │ • Rendering perf    │    │ • Tailwind in        │                │
│  │                     │    │   Remotion            │                │
│  │ LOW:                │    │ • Text animations    │                │
│  │ • JS micro-optim.   │    │ • Transparent video  │                │
│  │ • Advanced patterns │    │ • Audio viz          │                │
│  └─────────────────────┘    └──────────────────────┘                │
│                                                                      │
│  ┌─────────────────────┐                                            │
│  │  FOUNDRY            │                                            │
│  │                     │                                            │
│  │ • Forge             │                                            │
│  │   (build, test,     │                                            │
│  │    deploy Solidity)  │                                            │
│  │ • Cast              │                                            │
│  │   (interact with    │                                            │
│  │    EVM chains)      │                                            │
│  │ • Anvil             │                                            │
│  │   (local Ethereum   │                                            │
│  │    node)            │                                            │
│  │ • Chisel            │                                            │
│  │   (Solidity REPL)   │                                            │
│  │ • Fuzz & invariant  │                                            │
│  │   testing           │                                            │
│  │ • Fork testing      │                                            │
│  └─────────────────────┘                                            │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘

┌──────────────────────────────────────────────────────────────────────┐
│                       DEPLOY PIPELINE                                │
│                                                                      │
│  Generate slug ──► Vercel deploy ──► Alias to ──► Screenshot ──►    │
│  (2-4 words)       --prod --public   slug.        (Playwright)      │
│                                      vibe3.link                      │
│                                                  ──► Update VIBE3   │
│                                                      API + preview  │
│                                                                      │
│  Result: https://<slug>.vibe3.link                                  │
└──────────────────────────────────────────────────────────────────────┘
```

## MCP Tools

| Server | Purpose |
|--------|---------|
| `base-mcp` | Blockchain/Web3 capabilities via Coinbase SDK |
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
