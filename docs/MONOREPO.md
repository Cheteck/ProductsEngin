# Structure du Monorepo

Nous utilisons **Turborepo** avec **PNPM Workspaces** pour une gestion optimale des dépendances et une isolation claire des packages.

## Architecture des dossiers

```text
/
├── apps/
│   ├── admin/              # Dashboard Admin (Next.js)
│   ├── docs/               # Documentation (Mintlify ou Docusaurus)
│   └── store-demo/         # Boutique exemple (Next.js + Core)
├── packages/
│   ├── core/               # Logique métier, interfaces, plugin manager
│   ├── next/               # SDK spécifique Next.js (Server Actions, Hooks, Providers)
│   ├── ui/                 # Design System (Shadcn/ui + Tailwind)
│   ├── sdk/                # SDK universel (TypeScript)
│   ├── adapter-prisma/     # Adapter pour Prisma ORM
│   ├── adapter-drizzle/    # Adapter pour Drizzle ORM
│   └── schema/             # Schémas Zod partagés et types globaux
├── plugins/
│   ├── inventory/          # Gestion des stocks
│   ├── pricing/            # Moteur de prix complexe (tiers, multi-devises)
│   ├── subscriptions/      # Logique de récurrence et SaaS
│   ├── digital-assets/     # Gestion des fichiers et licences
│   └── bundles/            # Gestion des produits groupés
├── examples/
│   ├── starter-next/       # Template de démarrage rapide
│   └── custom-plugin/      # Exemple d'implémentation d'un plugin tiers
├── scripts/                # Outils de build et CI
└── tests/                  # Tests d'intégration transversaux
```

## Configuration Recommandée

### PNPM Workspaces (`pnpm-workspace.yaml`)
```yaml
packages:
  - 'apps/*'
  - 'packages/*'
  - 'plugins/*'
  - 'examples/*'
```

### Turborepo (`turbo.json`)
```json
{
  "$schema": "https://turbo.build/schema.json",
  "pipeline": {
    "build": {
      "dependsOn": ["^build"],
      "outputs": ["dist/**", ".next/**"]
    },
    "test": {
      "dependsOn": ["^build"]
    },
    "lint": {},
    "dev": {
      "cache": false,
      "persistent": true
    }
  }
}
```

## Stratégie de Publication
- **Changesets** pour la gestion des versions et des changelogs automatiques.
- Publication sur **NPM** sous le scope `@nexus-core/`.
