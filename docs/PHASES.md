# Roadmap Détaillée (NexusCore)

## PHASE 0 — Recherche & Architecture (2 semaines)
- [ ] Finalisation de la spécification technique détaillée.
- [ ] Benchmarking des solutions existantes (Medusa, Vendure, Payload).
- [ ] Définition des contrats d'interface Core/Plugins.

## PHASE 1 — Core Engine (3 semaines)
- [ ] Initialisation du Monorepo (Turborepo + PNPM).
- [ ] Création du `Kernel` : Plugin Manager et Dependency Injection.
- [ ] Implémentation du système de cycle de vie des plugins.
- [ ] Mise en place de la validation globale via Zod.

## PHASE 2 — Product System (4 semaines)
- [ ] Définition du modèle de données `Product` et `Variant`.
- [ ] Support des options de produits et des attributs dynamiques.
- [ ] Création des services CRUD de base.

## PHASE 3 — Plugin System (4 semaines)
- [ ] API d'enregistrement des plugins.
- [ ] Système d'extension de schéma (Dynamic Schema Merging).
- [ ] Plugin CLI pour aider les développeurs tiers.

## PHASE 4 — Feature Flags & Capabilities (2 semaines)
- [ ] Moteur de flags en mémoire.
- [ ] Système de "Capabilities" pour l'activation dynamique de features par tenant.

## PHASE 5 — Database Layer (3 semaines)
- [ ] Implémentation de l'adapter Drizzle (Default).
- [ ] Gestion des migrations automatiques.
- [ ] Support du Multi-tenant au niveau DB (RLS).

## PHASE 6 — Next.js Integration (4 semaines)
- [ ] Package `@nexus-core/next`.
- [ ] Server Actions pour toutes les mutations.
- [ ] Helpers pour le cache et les métadonnées.

## PHASE 7 — Admin UI (6 semaines)
- [ ] Dashboard de base avec Next.js.
- [ ] Editeur de produit complexe avec support des plugins (Slots).
- [ ] Gestion des listes (TanStack Table) avec filtres avancés.

## PHASE 8 — Event System (3 semaines)
- [ ] Bus d'événements local.
- [ ] Intégration BullMQ pour les jobs asynchrones.
- [ ] Système de Webhooks.

## PHASE 9 — API & SDK (3 semaines)
- [ ] Génération automatique du client TypeScript.
- [ ] API REST pour les intégrations externes.
- [ ] Authentification via API Key.

## PHASE 10 — Multi-Tenant (3 semaines)
- [ ] Gestion des organisations et workspaces.
- [ ] Isolation stricte des données.
- [ ] Portail de billing (Integration Stripe).

## PHASE 11-15 — Testing, Docs & Marketplace (En continu)
- [ ] Couverture de tests unitaires > 80%.
- [ ] Documentation technique complète (TypeDoc + Guides).
- [ ] Lancement de la v1 Stable.

---
## PHASE 13 — Marketplace Plugins (4 semaines)
- [ ] Conception du portail développeur.
- [ ] Système de vérification et de signature des plugins.
- [ ] Mise en œuvre d'un système de versioning sémantique pour les plugins.

## PHASE 14 — Enterprise Features (En continu)
- [ ] Audit logs.
- [ ] SSO/SAML integration.
- [ ] High availability & disaster recovery.

## PHASE 15 — v1 Stable Release (Mois 10)
- [ ] Freeze des API.
- [ ] Lancement marketing.
