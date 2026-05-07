# Admin UI System

L'interface d'administration est modulaire et extensible par les plugins.

## 1. Stack UI
- **Framework** : Next.js.
- **Styling** : Tailwind CSS + CSS Variables pour le thèming par tenant.
- **Components** : Radix UI via Shadcn/ui.
- **Tables** : TanStack Table (filtres complexes, tri, pagination).
- **Forms** : React Hook Form + Zod.

---

## 2. Extension Points (Slots)
Le dashboard expose des "Slots" où les plugins peuvent injecter leurs composants.
```tsx
<AdminLayout>
  <ProductForm>
    <GeneralSection />
    {/* Injection dynamique ici */}
    <PluginSlot name="product-editor-tabs" />
  </ProductForm>
</AdminLayout>
```

## 3. Dynamic Field Registry
Les plugins peuvent enregistrer de nouveaux types de champs (ex: sélecteur de fichier S3, sélecteur de couleur, éditeur JSON).
