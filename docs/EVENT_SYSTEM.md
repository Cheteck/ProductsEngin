# Event Driven Architecture

Le système de communication entre le Core et les plugins repose sur un **Event Bus** robuste.

## 1. Types d'événements

### Synchronous Hooks (Blocking)
Utilisés pour la validation ou la transformation de données avant persistance.
- `product.beforeCreate`
- `inventory.validate`

### Asynchronous Events (Non-blocking)
Utilisés pour les effets de bord (emails, notifications, analytics).
- `product.created`
- `order.placed`
- `price.updated`

---

## 2. Implémentation technique

- **Internal Bus** : `EventEmitter2` pour les opérations en mémoire ultra-rapides.
- **Distributed Bus** : `BullMQ` (Redis) pour les tâches asynchrones persistantes et la reprise sur erreur.

### Exemple de Middleware Pipeline
NexusCore utilise un système de pipeline similaire à celui de Koa/Express pour transformer les objets au vol :
```typescript
engine.use('product.fetch', async (context, next) => {
  await next();
  // Le plugin Pricing ajoute les prix convertis au résultat final
  context.result.price_converted = convert(context.result.price, context.currency);
});
```

---

## 3. Webhooks & Realtime
- **Webhooks** : Interface sortante pour notifier des systèmes tiers (Shopify, CRM). Signature HMAC obligatoire.
- **Realtime** : Support natif pour diffuser les changements d'inventaire via SSE (Server-Sent Events) ou WebSockets.
