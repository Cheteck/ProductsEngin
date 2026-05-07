# TypeScript Strategy

La puissance de NexusCore réside dans son typage.

## 1. Generics Avancés
Utilisation de génériques pour inférer les types étendus par les plugins.
```typescript
type ExtendedProduct<TPlugins extends Plugin[]> = Product & UnionToIntersection<TPlugins[number]['schema']>;
```

## 2. Inferred Schemas
Les types TypeScript sont automatiquement dérivés des schémas Zod, garantissant une synchronisation parfaite entre la validation runtime et les types de développement.

## 3. Plugin Type-Safety
Les plugins reçoivent des interfaces génériques qui leur permettent de s'enregistrer sans faire de `type casting` (as any).
