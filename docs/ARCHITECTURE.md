# Vision Globale & Architecture Technique

## 1. Vision du Projet
Le projet, baptisé **"NexusCore Product Engine"**, est un framework headless conçu pour être le "Linux de la gestion de produits ecommerce". Il ne s'agit pas d'une simple application, mais d'un moteur extensible capable de s'adapter à n'importe quel business model : de la simple boutique Shopify-like à une marketplace complexe, en passant par du SaaS B2B ou de la vente de services digitaux.

### Piliers Fondamentaux
- **Plugin-First** : Absolument tout ce qui n'est pas "l'ID d'un produit" est potentiellement un plugin.
- **Headless & Agnostique** : Le Core ne connaît pas le Web. Il expose des interfaces.
- **Type-Safety Extrême** : Utilisation de TypeScript avancé pour garantir que les plugins respectent les contrats sans sacrifier la flexibilité.
- **Scale-Ready** : Conçu pour le multi-tenant dès le premier jour (Shared Database avec Row Level Security ou Database-per-tenant).

---

## 2. Architecture Globale (High-Level)

NexusCore repose sur une **Architecture Hexagonale (Ports & Adapters)** modifiée pour supporter un système de plugins à chaud.

### Couches de l'Application
1.  **Core (Domain)** : Contient les entités fondamentales (Product, Identity) et les interfaces des services. Il n'a aucune dépendance externe.
2.  **Kernel (Infrastructure)** : Gère le cycle de vie des plugins, l'injection de dépendances, le registre d'événements et le moteur de Feature Flags.
3.  **Plugins (Features)** : Extensions du domaine (Inventory, Pricing, Subscriptions). Chaque plugin définit ses propres schémas de données et hooks.
4.  **Adapters (Persistence/IO)** : Implémentations concrètes pour la DB (Prisma, Drizzle), le Cache (Redis), ou les Providers (Stripe, AWS S3).
5.  **Interfaces (Delivery)** : Next.js App Router, SDK TypeScript, API REST/GraphQL.

---

## 3. Stack Technique Recommandée

| Composant | Technologie | Justification |
| :--- | :--- | :--- |
| **Monorepo** | PNPM + Turborepo | Gestion efficace des dépendances et du build cache. |
| **Langage** | TypeScript | Incontournable pour la robustesse et l'expérience développeur. |
| **Validation** | Zod | Single source of truth pour les types et la validation runtime. |
| **Framework Web** | Next.js 14+ (App Router) | Optimisation SEO, SSR, et simplicité des Server Actions. |
| **ORM / Query Builder** | Drizzle ORM | Pour la légèreté, le support Edge, et le typage SQL-like. |
| **Database** | PostgreSQL | Robustesse, JSONB pour les schémas dynamiques, support Multi-tenant. |
| **UI Kit** | Shadcn/ui + Tailwind CSS | Composants accessibles et hautement personnalisables. |
| **Event Bus** | BullMQ + Redis | Robustesse des jobs asynchrones et des événements. |
| **Testing** | Vitest + Playwright | Rapidité et tests E2E robustes. |

---

## 4. Stratégie de Scalabilité

- **Horizontal Scaling** : Le Core est stateless. Les sessions et caches sont déportés sur Redis.
- **Database Scaling** : Utilisation intensive de JSONB pour les champs extensibles afin d'éviter les `ALTER TABLE` fréquents. Support natif du sharding via les adapters.
- **Edge Compatibility** : Le SDK et les Adapters légers (Drizzle) permettent une exécution sur les Edge Functions de Vercel/Cloudflare.

