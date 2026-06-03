# Paso a paso — Recorrido de Encuesta Post-Compra (Mailchimp)

> Objetivo: cuando un cliente recibe su pedido, le preguntamos cómo estuvo (1 sola pregunta, escala 0–10). A los contentos les pedimos reseña; a los que no, los atendemos en privado antes de que dejen una mala reseña.
> Tiempo de armado: ~15 minutos.

---

## Antes de empezar (una sola vez)
- La tienda tiene que estar **conectada** a Mailchimp (igual que para el carrito).
- Lo ideal es disparar el recorrido cuando el pedido **se entrega**. Si Mailchimp no recibe el evento de "entregado", se usa "compró" + una espera que cubra el tiempo de envío.

---

## Armado del recorrido

1. **Create** → **Customer Journey** → **Start from scratch**. Nombre: `Encuesta post-compra` → **Begin**.
2. **Punto de inicio:** "Add a starting point" → elegí **Order delivered** (Pedido entregado). Si no existe esa opción, usá **Made a purchase** (Hizo una compra).
3. **Espera 3 días:** **+** → **Delay** → **3 days**.
4. **Email 1 (la encuesta):** **+** → **Send email** → pegá el HTML de `post-compra/01-nps-resena-3dias.html`.
   - Subject: `¿Cómo estuvo tu pedido?`
   - En el email, cada número del 0 al 10 es un link a `{{NPS_URL}}?score=N`. Reemplazá `{{NPS_URL}}` por:
     - una **encuesta de Mailchimp** (Mailchimp tiene bloques de Survey), o
     - una página simple que registre el puntaje (la arma el desarrollador).
5. **Ramificación por puntaje (lo importante):** después del email, **+** → **If/Else** según en qué número hizo clic:
   - **Clic en 9 o 10 (promotores):**
     - Aplicá una **etiqueta (tag)** `promoter` al contacto: **+** → **Tag/Update contact**.
     - Mandá un email corto pidiendo **reseña pública** (link a la reseña del producto).
   - **Clic en 7 u 8 (pasivos):** email corto "¿algo que mejorar?" con respuesta abierta.
   - **Clic en 0 a 6 (detractores):** **NO** los mandes a reseña pública. Email "queremos entender qué pasó" con respuesta directa a `ventas@ligier.com.ar` / WhatsApp.
6. **Email 2 (a los 10 días, opcional):** **+** → **Delay** → **7 days** (suma 10 desde la entrega) → **If/Else**: solo a quienes pusieron 7+ y **no dejaron reseña** → **Send email** → HTML de `02-resena-recompra-10dias.html`. Subject: `¿Te gustó alguno en particular?`. Trae botón "Volver a pedir".
7. **Probar** cada email (Send a test) y **Activar** (Turn on).

---

## Por qué está armado así
- La **reseña pública se le pide solo a quien ya está contento** (9–10). Sube las reseñas buenas.
- A los **descontentos se los atiende en privado** antes de que la mala experiencia se vuelva una reseña de 1 estrella.
- Los **promotores** quedan etiquetados → son los candidatos naturales al **Wine Club** y a referidos.
- El **"Volver a pedir"** del email 2 es la semilla de la recompra (usa el carrito compartido con los mismos vinos que compró).

---

## Qué reemplazar en los emails
- `{{NPS_URL}}` → tu encuesta/landing que guarda el puntaje.
- `{{REVIEW_URL}}` → la página de reseña del producto.
- `{{REORDER_URL}}` → link de carrito compartido con los productos que compró.
- Bloques entre `<!-- ORDER_PRODUCTS_START -->` y `<!-- ORDER_PRODUCTS_END -->` → los productos de la orden (con el conector de tienda se llena solo).
