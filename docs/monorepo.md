# Monorepo Guide

This project uses a **Bun-based monorepo** with workspaces to organize multiple packages and applications in a single repository.

## Structure

```
tedx-2026/
├── apps/              # Applications
├── packages/          # Shared packages
└── [config files]     # Root-level configuration
```

## How Workspaces Work

Workspaces are linked using the `workspace:*` protocol in package.json:

```json
{
  "dependencies": {
    "@tedx-2026/tsconfig": "workspace:*"
  }
}
```

This allows packages to reference each other locally without publishing to npm. Bun handles workspace resolution automatically.

## Workspace Catalog

The root `package.json` defines a catalog for shared dependencies:

```json
{
  "workspaces": {
    "catalog": {
      "typescript": "^5.9.3"
    }
  }
}
```

This ensures consistent versions of common dependencies across all workspaces.

## Adding New Workspaces

To add a new app:
1. Create a directory in `apps/`
2. Add a `package.json` with `"name": "app-name"`
3. Run `bun install` from the root directory to link workspaces

To add a new package:
1. Create a directory in `packages/`
2. Add a `package.json` with `"name": "@tedx-2026/package-name"`
3. Export what other workspaces need
4. Run `bun install` from the root directory to link workspaces
