# Dynatrace ESA App Template

A reusable Dynatrace Gen3 AppEngine template for building presentation-style and dashboard-style apps with:
- React + TypeScript UI (`ui/app`)
- Dynatrace App Functions (`src/functions`)
- Strato Design System components
- Optional externalized markdown content workflow

This repository is intended as a starter template. Use it to create a new app, then replace the sample branding, content, and environment configuration.

## What this template generates

When used as a starting point, you get:
- App manifest and runtime configuration (`app.config.json`)
- Local development and deployment scripts (`dt-app` based)
- Frontend shell with routing, shared components, and styles
- Backend function examples for Grail queries, entities, and metrics
- Content and documentation scaffolding for knowledge-heavy app experiences

## Repository structure

```text
.
├── app.config.json
├── package.json
├── main.tsx
├── src/
│   ├── functions/
│   │   ├── query-grail.ts
│   │   ├── get-metrics.ts
│   │   └── get-entities.ts
│   └── assets/
├── ui/
│   ├── index.html
│   └── app/
│       ├── App.tsx
│       ├── index.tsx
│       ├── components/
│       ├── pages/
│       ├── hooks/
│       ├── services/
│       ├── data/
│       ├── config/
│       └── styles/
├── content/placeholders/
└── docs/
```

## How the template works

1. `dt-app` runs the local app runtime and bundles frontend + app functions.
2. `app.config.json` defines app identity, scopes, runtime host/port, and build settings.
3. The UI calls app functions through SDK wrappers in `ui/app/utils/appFunctions.ts`.
4. Content can be loaded from local data and can be extended to external sources (for example SharePoint, documented in `docs/SHAREPOINT_SETUP.md`).

## Prerequisites

- Node.js `>=20`
- npm
- Access to a Dynatrace environment with Gen3 apps enabled
- Permissions matching the scopes configured in `app.config.json`

## Setup

```bash
npm install
```

Then review and update at minimum:
- `app.config.json` (`environmentUrl`, `app.id`, `app.name`, `app.description`, scopes)
- `package.json` (`name`, `description`)

## Development, validation, build, and deployment

```bash
# Start local development server
npm run dev

# Lint
npm run lint

# Type checking
npm run type-check

# Build production package
npm run build

# Deploy to Dynatrace environment
npm run deploy

# Scaffold additional artifacts via dt-app
npm run generate
```

## Testing and linting notes

- Linting and static type checking are configured (`npm run lint`, `npm run type-check`).
- There is currently no dedicated automated unit/integration test suite configured in this template.

## Configuration reference

Primary configuration file: `app.config.json`
- `environmentUrl`: target Dynatrace environment
- `app.id`: globally unique app identifier
- `app.name` / `app.description` / `app.version`: app metadata
- `app.scopes`: runtime permissions
- `app.icon`: app icon asset path
- `server.port` / `server.host`: local dev runtime settings

Related configuration points:
- `ui/app/config/sharepoint.ts` for optional external content mapping
- `tsconfig.json` for TypeScript compiler settings
- `.eslintrc.json` for linting rules

## Extension points

Common customizations:
- Add or modify pages in `ui/app/pages`
- Add reusable UI components in `ui/app/components`
- Add backend capabilities in `src/functions`
- Update navigation/shell behavior in `ui/app/App.tsx`
- Replace placeholder markdown content in `content/placeholders`
- Extend services in `ui/app/services`

## Update and migration guidance

When reusing this template for a new app:
1. Create a clean copy/clone for the new project.
2. Rename app identity (`app.id`, app/package names, descriptions).
3. Review all requested scopes and remove unneeded permissions.
4. Replace sample/demo content and branding (including default passwords if used in your forked app).
5. Re-run lint/type-check/build before first deployment.

When syncing from this template into an existing app:
- Diff and merge selectively (prefer keeping your app-specific data/services/pages).
- Prioritize updates to shared shell patterns, config hardening, and docs.
- Validate scope changes and deployment behavior in a non-production environment first.

## Troubleshooting

- **`npm run dev` fails**: ensure Node 20+ and reinstall dependencies.
- **Scope/permission errors**: verify `app.config.json` scopes and environment permissions.
- **Deployment issues**: review `DEPLOYMENT.md` and confirm `environmentUrl` is correct.
- **Content not loading from SharePoint**: verify URLs, access permissions, and setup in `docs/SHAREPOINT_SETUP.md`.

## Contributing

1. Create focused, minimal changes.
2. Keep template behavior generic and reusable.
3. Run `npm run lint` and `npm run type-check` before submitting.
4. Document user-facing behavior changes in this README or linked docs.
5. Follow repository check-in expectations in `CHECK_IN_POLICY.md`.

## Additional documentation

- `QUICKSTART.md`
- `DEPLOYMENT.md`
- `EXAMPLES.md`
- `docs/TechnicalArchitecture.md`
- `docs/SHAREPOINT_SETUP.md`

## License status

No repository license file is currently present.

If this template is intended for public reuse, add an explicit license in a follow-up change after confirming the correct legal choice with the repository owner. Until then, licensing remains undefined.
