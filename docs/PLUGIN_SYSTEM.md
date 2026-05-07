# Plugin System Architecture

NexusCore est conçu avec une mentalité **Plugin-First**. Le Core est un orchestrateur minimal qui délègue la majorité des fonctionnalités à des plugins.

## 1. Architecture des Plugins

### Lifecycle des Plugins
Chaque plugin passe par plusieurs phases :
1.  **Discovery** : Scan du dossier `plugins/` ou du `package.json`.
2.  **Registration** : Enregistrement des métadonnées et des schémas.
3.  **Bootstrap** : Initialisation des services internes du plugin.
4.  **Ready** : Le plugin est actif et peut répondre aux événements.

### Dependency Injection
Le Core fournit un `PluginContext` à chaque plugin lors de l'initialisation :
- Accès au DB Adapter.
- Accès au Event Bus.
- Accès au Feature Flag Engine.
- Possibilité d'enregistrer de nouveaux "Capability" (ex: `can_calculate_tax`).

---

## 2. API des Plugins (Exemple)

```typescript
import { createPlugin } from '@nexus-core/core';

export const PricingPlugin = createPlugin({
  id: 'pricing-advanced',
  version: '1.0.0',
  capabilities: ['multi-currency', 'tier-pricing'],
  
  // Extension du schéma Product
  schemaExtensions: (schema) => {
    return schema.extend({
      basePrice: z.number(),
      currency: z.string().default('USD'),
      tiers: z.array(z.object({
        minQuantity: z.number(),
        discount: z.number()
      })).optional()
    });
  },

  // Enregistrement des Hooks
  setup: ({ hooks, db }) => {
    hooks.on('product.beforeCreate', async (product) => {
      // Logique de validation de prix
    });

    hooks.on('product.afterUpdate', async (product) => {
      // Invalidation de cache ou notification
    });
  },

  // UI Extensions
  ui: {
    productSlots: {
      'pricing-section': PricingFormFields
    }
  }
});
```

---

## 3. Runtime vs Build-time
- **Build-time** : Génération des types TypeScript consolidés pour les schémas étendus.
- **Runtime** : Enregistrement dynamique des handlers et validation Zod.

## 4. Isolation & Sécurité
- Les plugins tiers peuvent être exécutés dans des **Worker Threads** (en option) pour éviter de bloquer l'event loop.
- Système de permissions strict pour limiter l'accès aux données sensibles par un plugin.
