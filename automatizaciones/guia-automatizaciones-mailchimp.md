# Guía de Automatizaciones — Mailchimp Customer Journeys (Ligier)

Cómo poner en producción los flujos de **carrito abandonado**, **encuesta post-compra**, **bienvenida** y **win-back**. Cada flujo reutiliza la voz de marca de `guidelines/ligier-email-guidelines.md` y los datos que ya expone Magento.

> **Plantillas listas en este repo:**
> - `automatizaciones/carrito-abandonado/01-carrito-1h.html`, `02-carrito-24h.html`, `03-carrito-72h.html`
> - `automatizaciones/post-compra/01-nps-resena-3dias.html`, `02-resena-recompra-10dias.html`

---

## 0. Requisito base: conectar la tienda (Magento → Mailchimp)

Los triggers de e-commerce (carrito, compra, entrega) necesitan que Mailchimp **reciba eventos de la tienda**. Dos caminos:

1. **Conector Magento ↔ Mailchimp** (Mailchimp for Magento / MailChimp4Magento): sincroniza clientes, productos, carritos y órdenes automáticamente. Es el camino recomendado si existe el módulo para la versión de Magento del sitio.
2. **API e-commerce de Mailchimp** (si no hay módulo): postear los eventos desde el backend.
   - Crear store: `POST /ecommerce/stores`
   - Carrito: `POST /ecommerce/stores/{store_id}/carts` (con `customer.email_address`, `lines[]`, `checkout_url`)
   - Orden: `POST /ecommerce/stores/{store_id}/orders`
   - El parser `parseMagentoProduct` de `ligier-app/api/generate-campaign.js` ya devuelve `sku, name, price, image, url, inStock` — la misma forma que necesitan los `lines[]`.

**Autenticación de dominio (bloqueante para deliverability):** confirmar SPF, DKIM y DMARC del dominio de envío en Mailchimp → Settings → Domains. Requisito de Gmail/Yahoo desde 2024.

---

## 1. Carrito abandonado

**Tipo:** Customer Journey → trigger **"Abandoned cart"** (aparece cuando la tienda está conectada).

### Pasos en Mailchimp
1. **Create → Customer Journey → Start from scratch.**
2. **Starting point:** *Abandoned cart* (o *Cart activity*). Define "abandonado" = carrito sin checkout por X tiempo.
3. **Email 1 — esperar 1 h** → `01-carrito-1h.html`. Subject: `Dejaste botellas en el carrito`.
4. **Delay 24 h** + **branch "¿compró?"**: si compró → exit. Si no →
5. **Email 2** → `02-carrito-24h.html`. Subject: `Sobre los vinos que dejaste`.
6. **Delay 48 h** (→ 72 h desde el inicio) + branch "¿compró?": si no →
7. **Email 3** → `03-carrito-72h.html`. Subject: `Tu carrito sigue abierto`.
8. **Exit rules globales:** salir del journey al completar una compra (Mailchimp lo trae nativo con el trigger de e-commerce).

### Placeholders a mapear en las plantillas
| Placeholder | De dónde sale |
|-------------|---------------|
| `{{CART_URL}}` | `checkout_url` del carrito, o link de carrito compartido reconstruido con los SKUs (`compartircarrito/index/share/data/[BASE64]`). |
| Bloque entre `<!-- CART_PRODUCTS_START -->` y `<!-- CART_PRODUCTS_END -->` | Ítems del carrito. Con el conector, usar el **bloque de carrito** nativo de Mailchimp; con HTML propio, repetir el sub-bloque por ítem con `{{PRODUCT_IMG/NAME/LABEL/PRICE/URL}}` y `{{PRODUCT_NOTE}}` (nota de cata, del `short_description` de Magento). |

### Reglas que NO se rompen
- **Sin descuento en el toque 1 y 2.** El 80% se recupera sin quemar margen.
- **Toque 3, incentivo sin costo:** vinos → recordar el **6×5 que ya existe** (bloque incluido). Whisky/espirituosas/guardados → reemplazar ese bloque por **3 cuotas sin interés** o **envío sin cargo**. Cupón de % solo si la analítica prueba que sin él se pierde la venta, con tope y vencimiento 48 h.
- **Solo carritos con email.**
- **Frequency cap:** quien está en el flujo de carrito no recibe el newsletter masivo ese día (el carrito tiene prioridad).
- **Supresión por stock 0:** no recuperar un ítem sin stock (`inStock`).

---

## 2. Encuesta post-compra / post-entrega

**Tipo:** Customer Journey → trigger ideal **"Order delivered"** (o "Placed an order" + delay que cubra el SLA de envío si no hay evento de entrega).

### Pasos en Mailchimp
1. **Starting point:** *Order delivered* (preferido) o *Made a purchase*.
2. **Delay 3 días** → **Email 1** → `01-nps-resena-3dias.html`. Subject: `¿Cómo estuvo tu pedido?`.
3. **Branch por score** (cada número linkea a `{{NPS_URL}}?score=N`; usar *"clicked a link"* o una Survey de Mailchimp para ramificar):
   - **9–10 (promotores):** aplicar **tag `promoter`** → enviar a pedir reseña pública (`{{REVIEW_URL}}`).
   - **7–8 (pasivos):** email corto "¿algo que mejorar?" → reply abierto.
   - **0–6 (detractores):** **NO** mandar a reseña pública → email "queremos entender qué pasó" con reply directo a `ventas@ligier.com.ar` / WhatsApp. Recuperación 1-a-1.
4. **Delay 10 días desde la entrega** + condición "NPS ≥ 7 y sin reseña" → **Email 2** → `02-resena-recompra-10dias.html`. Subject: `¿Te gustó alguno en particular?`.

### Placeholders
| Placeholder | De dónde sale |
|-------------|---------------|
| `{{NPS_URL}}` | Landing/Survey de Mailchimp o endpoint propio que registre el score. |
| `{{REVIEW_URL}}` | Página de reseña del producto en Magento. |
| `{{REORDER_URL}}` | Link de carrito compartido reconstruido con los SKUs de la orden. |
| Bloques `ORDER_PRODUCTS_*` | Ítems de la orden entregada. |

### Por qué este diseño
Pide la reseña pública **solo a quien ya está contento** (9–10). A los detractores los lleva a un canal privado **antes** de que la mala experiencia se convierta en una reseña de 1 estrella. Los promotores quedan etiquetados como candidatos naturales a Wine Club y referidos.

---

## 3. Bienvenida (quick win #3)

**Tipo:** Customer Journey → trigger **"Signs up to a list / tag"**. 3 emails (a crear; usar `templates/base-email-vinos.html` como base visual, recortando productos).

1. **Inmediato:** quiénes somos, cómo curamos, las 10 categorías. CTA suave a `/vino`. Sin venta dura.
2. **+3 días:** cómo funciona el **6×5** y cómo armar un pack mezclando etiquetas (educa el mecanismo que más factura).
3. **+7 días:** Wine Club y Experiencias como "siguiente paso".

Incentivo de welcome opcional: **envío gratis en la 1ª compra** antes que un % (protege margen y posiciona premium).

---

## 4. Win-back (dormidos)

**Tipo:** Customer Journey → trigger **"Tag added: dormido"** o segmento "sin compra ni click en 90 días".

1. **90 d:** "Volvimos a actualizar la cava" → novedades, **sin descuento**.
2. **120 d:** "Lo que te estás perdiendo" → 3–4 etiquetas top del trimestre.
3. **180 d:** último toque + **incentivo real** (envío gratis o cuotas). Si no abre/clickea → mover a **sunset** (suprimir de envíos masivos).

---

## 5. Segmentos y tags a crear

| Tag | Cuándo se aplica |
|-----|------------------|
| `lead` | Suscripto, 0 órdenes |
| `first-order` | 1 orden |
| `recurrente` | 2+ órdenes |
| `high-value` | AOV/CLV top 20% |
| `wineclub` (+ nivel) | Membresía activa |
| `dormido` | Sin compra ni click 90–180 d |
| `winback` | Sin actividad 180+ d |
| `promoter` | NPS 9–10 |

Mailchimp e-commerce calcula CLV, nº de órdenes y fecha de última compra out-of-the-box; usar esos campos para construir los segmentos.

---

## 6. Checklist de puesta en producción

- [ ] Tienda Magento conectada (conector o API e-commerce) y enviando carritos/órdenes.
- [ ] SPF/DKIM/DMARC verificados en el dominio de envío.
- [ ] Carrito abandonado: 3 emails cargados, branches "¿compró?" y exit por compra.
- [ ] Post-compra: trigger de entrega, branch por NPS, tag `promoter`.
- [ ] Placeholders mapeados (`CART_URL`, `NPS_URL`, `REVIEW_URL`, `REORDER_URL`, bloques de producto).
- [ ] Prueba de cada email a `dayanmartin@gmail.com` antes de activar.
- [ ] Frequency cap: flujos transaccionales tienen prioridad sobre el masivo.
- [ ] Medición: revisar performance de cada journey en Mailchimp + sumar al análisis de `analyze.js` (ver `estrategia/estrategia-email-marketing.md` §6.3).
