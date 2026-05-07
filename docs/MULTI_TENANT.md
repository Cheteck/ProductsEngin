# Stratégie Multi-Tenant Détaillée

## 1. Isolation
- **Logical Isolation** : Utilisation d'un `tenant_id` global.
- **Middleware de Sécurité** : Injection automatique du filtre tenant dans toutes les requêtes SQL via l'adapter.

## 2. Personnalisation
Chaque tenant peut :
- Activer/Désactiver des plugins spécifiques.
- Configurer ses propres Feature Flags.
- Personnaliser l'UI via un `Theme Engine` (CSS Variables).

## 3. Provisionnement
- Processus automatisé de création de compte.
- Setup de la structure de base (Categories, Taxes par défaut).
