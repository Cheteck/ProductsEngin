# Stratégie Domain Model

Le modèle de données doit être à la fois rigide (pour la performance) et extrêmement flexible (pour l'extensibilité).

## 1. Modèles de Base

### Product
L'entité centrale. Un produit est une abstraction qui possède :
- `id`, `slug`, `title`, `description`
- `status` (draft, active, archived)
- `type` (physical, digital, service, subscription)
- `metadata` (JSONB) : Stockage des champs ajoutés par les plugins.

### Variant
Un produit peut avoir plusieurs variantes (ex: Taille S, Couleur Rouge).
- Chaque variante possède son propre `sku`, `price`, et `inventory`.
- Les variantes héritent des propriétés du produit parent.

### ProductOption & ProductValue
- `Option` (ex: Taille, Couleur)
- `Value` (ex: Small, Medium, Red, Blue)

---

## 2. Extensions Thématiques (via Plugins)

- **Inventory** : Relation `1:N` avec `Warehouse`. Support multi-stocks.
- **Pricing** : Gestion des prix barrés, prix par volume, prix par groupe client.
- **Specification** : Caractéristiques techniques (Poids, Dimensions, Voltage) via un système de clés-valeurs typées.
- **Subscription** : Fréquence de facturation, période d'essai, type de renouvellement.
- **Digital** : Liens de téléchargement sécurisés, clés de licence.

---

## 3. Schémas Dynamiques vs Relationnel
Nous utilisons une approche hybride :
1.  **Colonnes SQL fixes** pour les données critiques (recherche, filtres, jointures).
2.  **JSONB (PostgreSQL)** pour les données spécifiques aux plugins afin d'éviter les migrations complexes.

**Exemple de structure JSONB pour un produit :**
```json
{
  "id": "prod_123",
  "name": "Super T-Shirt",
  "extensions": {
    "pricing": { "currency": "EUR", "base_price": 2500 },
    "shipping": { "weight": 0.2, "unit": "kg" },
    "seo": { "title": "...", "description": "..." }
  }
}
```

---

## 4. Performance
- Utilisation de **GIN Indexes** sur les colonnes JSONB pour permettre des recherches rapides.
- Dénormalisation sélective (ex: le prix min/max stocké sur le Product parent).
