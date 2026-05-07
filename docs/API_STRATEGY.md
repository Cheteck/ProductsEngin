# API & SDK Strategy

## 1. SDK-First Approach
Nous privilégions le SDK TypeScript. L'API (REST/GraphQL) n'est qu'un transport.
```typescript
import { NexusCore } from '@nexus-core/sdk';

const nexus = new NexusCore({
  apiKey: process.env.NEXUS_API_KEY,
  tenantId: 'my-tenant'
});

const product = await nexus.products.create({ ... });
```

## 2. API Types
- **tRPC** : Recommandé pour l'application Admin interne (Type-safety de bout en bout).
- **REST** : Pour l'interopérabilité externe (Webhooks, intégrations tierces).
- **GraphQL (Optionnel)** : Fourni via un plugin pour les besoins complexes de fetching (Storefronts).

---

## 3. Sécurité (ACL)
Système de permissions granulaire :
- `Role-Based Access Control (RBAC)` : Admin, Manager, Editor, Viewer.
- `Attribute-Based Access Control (ABAC)` : Ex: "L'utilisateur peut modifier les prix seulement si le produit appartient à sa catégorie".
