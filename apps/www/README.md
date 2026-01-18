# TEDX 2026 Website

The main website for TEDX UB 2026 (Universitas Brawijaya), built with Astro for optimal performance and developer experience.

## Tech Stack

- **Framework**: [Astro](https://astro.build) v5.16.11
- **Language**: TypeScript
- **Package Manager**: Bun
- **Deployment**: Static site (SSG)

## Prerequisites

Before working on this app, ensure you've set up the monorepo:

```bash
# From the project root
bun install
```

This will install all dependencies and link workspace packages.

## Development Commands

All commands should be run from **this directory** (`apps/www`):

### Start Development Server

```bash
bun run dev
```

- Opens dev server at `http://localhost:4321`
- Hot reload enabled for instant updates
- TypeScript checking in the editor

### Build for Production

```bash
bun run build
```

- Compiles site to static HTML/CSS/JS
- Output directory: `dist/`
- Optimizes assets and bundles
- Generates sitemap and RSS (when configured)

### Preview Production Build

```bash
bun run preview
```

- Serves the `dist/` folder locally
- Opens at `http://localhost:4321`
- Test production build before deployment

## Project Structure

```
apps/www/
├── src/
│   ├── pages/          # File-based routing (each .astro = route)
│   │   └── index.astro # Home page (/)
│   ├── components/     # Reusable Astro/React/Vue components (future)
│   ├── layouts/        # Page layouts and templates (future)
│   └── styles/         # Global CSS and style utilities (future)
├── public/             # Static assets (copied to dist/ as-is) (future)
├── dist/               # Build output (generated, not committed)
├── astro.config.mjs    # Astro configuration
├── tsconfig.json       # TypeScript config (extends workspace)
├── biome.jsonc         # Linting config (extends root + Astro rules)
└── package.json        # App dependencies and scripts
```

### Key Concepts

**Pages** (`src/pages/`)
- Each `.astro` file becomes a route
- `index.astro` → `/`
- `about.astro` → `/about`
- `blog/[slug].astro` → `/blog/dynamic-route`

**Components** (future: `src/components/`)
- Reusable UI components
- Can be Astro, React, Vue, Svelte, etc.
- Zero JS by default (Astro Islands architecture)

**Public Assets** (future: `public/`)
- Static files (images, fonts, favicon)
- Copied directly to `dist/` without processing
- Access via `/filename.ext` in code

## Environment Variables

Currently none required. When needed, create a `.env` file:

```bash
# .env (not committed)
PUBLIC_API_URL=https://api.example.com
SECRET_KEY=xyz123
```

- Prefix with `PUBLIC_` to expose to client-side code
- Access via `import.meta.env.PUBLIC_API_URL`
- Never commit `.env` files (already in `.gitignore`)

## Configuration

### Astro Config (`astro.config.mjs`)

Currently minimal. Common configurations to add:

```js
export default defineConfig({
  site: 'https://tedxub.com',            // Your production URL
  integrations: [react(), tailwind()],   // Framework integrations
  output: 'static',                      // Output mode (static/server/hybrid)
});
```

### TypeScript Config (`tsconfig.json`)

Extends two configs:
- `astro/tsconfigs/strict` - Astro's strict TypeScript settings
- `@tedx-2026/tsconfig/base.json` - Workspace shared config (ESNext target)

## Deployment

### Build Output

```bash
bun run build
```

Generates:
- Output directory: `dist/`
- All files are static (HTML, CSS, JS, assets)
- Ready to deploy to any static hosting

### Type Checking

```bash
# From project root
bunx tsc --noEmit
```

### Code Quality

All code is automatically formatted and linted via Ultracite:
- Pre-commit hook formats staged files
- Run `bun run lint:fix` from root to fix all issues

## Resources

- [Astro Documentation](https://docs.astro.build)
- [Astro Examples](https://astro.build/themes)
- [Monorepo Guide](../../docs/monorepo.md)
- [Development Guide](../../docs/development.md)
