# Intégration Next.js & React

NexusCore est "Next.js native", tirant parti de toutes les fonctionnalités modernes du framework de Vercel.

## 1. App Router & RSC (React Server Components)
Le package `@nexus-core/next` fournit des helpers pour :
- **Fetching de données** : Utilisation de fonctions `async` directement dans les RSC avec cache dédupliqué via `React.cache`.
- **SEO** : Génération automatique des Metadata dynamiques à partir des produits.
- **Streaming** : Support du chargement progressif des composants (ex: liste de produits d'abord, prix/stock ensuite via Suspense).

## 2. Server Actions
Toutes les mutations (création de produit, mise à jour de stock) sont exposées via des **Server Actions** sécurisées.
- Validation automatique via Zod.
- Gestion des permissions intégrée.
- Revalidation instantanée du cache via `revalidatePath`.

## 3. Client-side Hooks
Pour les parties interactives (panier, filtres dynamiques) :
- `useProduct()` : Accès aux données d'un produit avec mise à jour temps réel.
- `useInventory()` : Hook optimiste pour la gestion des stocks.

---

## 4. Middleware & Auth
- Intégration avec **NextAuth.js** ou **Clerk**.
- Middleware pour la détection du `tenant_id` basé sur le sous-domaine ou le header custom.
