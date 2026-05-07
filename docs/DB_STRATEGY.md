# Database Strategy & Multi-tenant

## 1. Choix technologique
Nous recommandons **PostgreSQL** comme moteur principal en raison de sa gestion exceptionnelle du JSONB et de sa robustesse.

### ORM vs Query Builder
- **Drizzle ORM** est privilégié pour :
  - Son typage TypeScript "SQL-first".
  - Son absence de runtime overhead.
  - Sa compatibilité parfaite avec l'Edge Computing (Serverless).
- **Prisma** est proposé comme adapter alternatif pour les équipes préférant le schéma-first.

---

## 2. Multi-tenant
NexusCore supporte deux stratégies de multi-tenant :

### Stratégie A : Shared Database (Default)
- Une colonne `tenant_id` sur chaque table.
- Utilisation de **RLS (Row Level Security)** au niveau de PostgreSQL pour garantir l'étanchéité totale des données.
- Scalabilité facile, maintenance simplifiée.

### Stratégie B : Schema-per-tenant
- Un schéma SQL par client.
- Idéal pour les besoins "Enterprise" nécessitant une isolation physique ou des migrations décalées.

---

## 3. Migrations
- Les migrations du Core sont gérées par Drizzle/Prisma.
- Les plugins peuvent injecter leurs propres migrations via un système de `PluginMigrationManager` intégré au Core.
- Support des **Seeders** pour initialiser les données par défaut d'un nouveau tenant.
