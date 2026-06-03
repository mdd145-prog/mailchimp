# Paso a paso — Recorrido de Carrito Abandonado (Mailchimp)

> Objetivo: cuando alguien deja vinos en el carrito y no compra, recibe 3 emails (1h, 24h, 72h) que lo invitan a volver. Sin descuento hasta el último toque.
> Tiempo de armado: ~15 minutos. Lo hace quien tenga el login de Mailchimp.

---

## Antes de empezar (una sola vez)
La tienda (vinotecaligier.com / Magento) tiene que estar **conectada** a Mailchimp para que Mailchimp "sepa" cuándo alguien abandona un carrito.
- En Mailchimp: **Integrations** → buscar **Magento** (o el conector de la tienda) → conectar.
- Si no aparece el conector, lo arma el desarrollador con la API de e-commerce de Mailchimp (ver `guia-automatizaciones-mailchimp.md`, sección 0). **Sin esto, el recorrido no se puede disparar.**

---

## Armado del recorrido

1. En Mailchimp, arriba a la izquierda: **Create** → **Customer Journey** → **Start from scratch**.
2. Ponele un nombre: `Carrito abandonado` → **Begin**.
3. **Punto de inicio (Starting point):** clic en el cartel "Add a starting point" → elegí **Abandoned cart** (Carrito abandonado). Confirmá.
4. **Email 1 (a la 1 hora):**
   - Debajo del inicio, clic en **+** → **Send email**.
   - Antes del email, agregá un **Delay (espera)** de **1 hora**: clic en **+** → **Delay** → 1 hour.
   - Abrí el email → **Design email** → pegá el HTML de `carrito-abandonado/01-carrito-1h.html`.
     - Subject: `Dejaste botellas en el carrito`
     - Si te lo pide, el preview/preheader ya viene dentro del HTML.
5. **Espera + Email 2 (24 h):**
   - Clic en **+** → **Delay** → **23 hours** (suma 24 h desde el inicio).
   - Antes de mandar, agregá una **condición**: **+** → **If/Else** → "¿Compró?" (condición: *placed an order* = no). Si compró → que salga del recorrido.
   - En la rama "no compró": **+** → **Send email** → HTML de `02-carrito-24h.html`. Subject: `Sobre los vinos que dejaste`.
6. **Espera + Email 3 (72 h):**
   - **+** → **Delay** → **48 hours** (suma 72 h).
   - Otra condición "¿Compró?" igual que antes.
   - En "no compró": **+** → **Send email** → HTML de `03-carrito-72h.html`. Subject: `Tu carrito sigue abierto`.
7. **Salida por compra (importante):** en los ajustes del recorrido, activá que **al concretar una compra el contacto salga del recorrido**. (Con el trigger de e-commerce, Mailchimp lo ofrece por defecto.)
8. **Probar:** mandate un test de cada email a vos mismo (botón **Send a test** en cada email).
9. **Activar:** arriba a la derecha → **Turn on** / **Continue**.

---

## Reglas que NO se rompen (ya están pensadas en los textos)
- **Email 1 y 2: sin descuento.** El 80% se recupera sin regalar margen.
- **Email 3 (vinos):** NO es un descuento nuevo — recuerda el **6×5 que ya existe** ("si llevás 6, pagás 5"). Margen intacto.
- **Email 3 (whisky/espirituosas/guardados):** en vez del 6×5, ofrecé **3 cuotas sin interés** o **envío sin cargo** (ese bloque está marcado en el HTML para reemplazar).
- Quien está en este recorrido **no debería recibir el newsletter masivo** ese día (el carrito tiene prioridad).

---

## Qué reemplazar en los emails (campos dinámicos)
Dentro de cada HTML hay marcas tipo `{{CART_URL}}` y un bloque de productos entre `<!-- CART_PRODUCTS_START -->` y `<!-- CART_PRODUCTS_END -->`.
- Con el **conector de tienda**, Mailchimp tiene un **bloque de "Productos del carrito"** que se llena solo: usalo en lugar de ese bloque.
- `{{CART_URL}}` = el link para volver al carrito (lo provee el conector, o se arma con el link de carrito compartido).
- Si algo queda sin reemplazar, se nota — revisá el test antes de activar.
