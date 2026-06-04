# Replanteo de arquitectura — hacia Guidelines v4.0
> Junio 2026 — Decisiones tomadas punto por punto sobre guidelines v3.1, plantillas y ligier-app.
> Sistema de dos repos: `Mailchimp` (fuente de verdad de diseño/copy) + `ligier-app` (generación e inyección).

---

## A. DECISIONES

### B1 — Contrato app ↔ plantillas

| # | Decisión | Impacto |
|---|----------|---------|
| B1.1 | El total del pack 6×5 **se lee siempre del carrito real** de Magento. Activar `getCartTotal()` (hoy código muerto) y eliminar el cálculo `subtotal − botellas gratis`. El guideline ya lo decía; ahora la app lo cumple. | `api/generate-campaign.js` |
| B1.2 | **La condición del 6×5 es por botellas, no por productos**: suma de `qty` del carrito ≥ 6. Un email puede mostrar 3 etiquetas × 2 unidades. Si la suma es < 6, la app **elimina** banner promo + botón pack (nunca más un "$0"). | `api/generate-campaign.js` |
| B1.3 | Wine Club, Experiencias y Gift Cards dejan de reusar la plantilla de vinos: **plantillas vivas propias** + rama "sin productos" en la app (hoy aborta con `products.length === 0`). | plantillas nuevas + app |
| B1.4 | **Contrato formal de marcadores**: migrar a anclajes explícitos `<!-- INJECT:... -->` en todas las plantillas y documentarlos completos en el guideline como sección "API de inyección". Se eliminan los anclajes implícitos por comentarios de sección (`<!-- ── 4b. ── -->`). | plantillas + app + guideline |
| B1.5 | El eyebrow del hero se ancla **por clase** (`class="hero-eyebrow"`), no por "primer `color:#666` del documento". | plantillas + app |

### B2 — Tipos de email

| # | Decisión |
|---|----------|
| B2.2 | **Quitar del guideline** la sección de recetas de cóctel de espirituosas (nunca existió en HTML). Espirituosas = plantilla whisky. |
| B2.3 | **Incorporar el tipo REGALOS completo**: plantilla viva + tipo en el wizard (1 regalo, foto grande, detalle de componentes, CTA "Regalá esta selección"). |

### B3 — Estructura

| # | Decisión |
|---|----------|
| B3.1 | **Orden fijo e inmutable** de secciones por tipo. La rigidez es la marca. |
| B3.3 | Accesorio: **solo manual (URL) o ninguno**. Se elimina el modo "auto" (defaults hardcodeados violaban "stock verificado"). |

### B4 — Promos y precios

| # | Decisión |
|---|----------|
| B4.1 | 6×5 **exclusivo de vinos** (regla sagrada). Eliminar del wizard los campos decorativos `tienePromo` y `rango` que el servidor ignora. |
| B4.2 | **Mantener** la presentación: tachado + precio ×5/6 + label "C/U COMPRANDO 6". |

### B5/B6 — Identidad visual

| # | Decisión |
|---|----------|
| B5.1 | **Arial sigue siendo ley en email.** La serif editorial (Fraunces / fallback Georgia) queda documentada como recurso de marca **solo para piezas web** (landings, gráfica de eventos). Referencia: `landing/ligier-experience-8.html`. |
| B5.2/B6.1 | **Monocromo plano se mantiene**: paleta de 8 colores, sin border-radius, sin sombras, sin gradientes. Sin acentos nuevos. |

### B7 — Copy

| # | Decisión |
|---|----------|
| B7.2 | **Fuente única de copy**: `copy-library.json` en este repo (junto a guidelines y plantillas). La app la consume vía GitHub raw y se eliminan los dos juegos duplicados (`src/copy-library.js` + defaults del servidor). |
| B7.3 | **Validación programática del H1 en el wizard**: máx 3 líneas × 6 palabras, sin punto final, sin precio/promo, sin superlativos prohibidos. |
| B7.4 | La bajada con "Llevá 6, pagá 5" deja de estar hardcodeada en el servidor: sale de `copy-library.json`. |

### B8 — Técnico / deliverability

| # | Decisión |
|---|----------|
| B8.2 | **Botones bulletproof en todos los botones**: padding en `<td bgcolor>`, no en `<a>` (plantillas + bloques generados por la app). |
| B8.3 | **Scaffolding MSO**: `xmlns:v/o`, `OfficeDocumentSettings`, `mso-line-height-rule:exactly`. |
| B8.4 | **VML para el hero de Guardados** (la imagen de cava hoy no se ve en Outlook). |
| B8.5 | **Accesibilidad**: `role="presentation"` en tablas de layout + tap targets de pills ≥ 44px. |
| B8.6 | **Assets dark mode**: regenerar logo e íconos sobre fondo blanco sólido. |
| B8.8 | 🐛 Fix: URL raw con capitalización real del repo (`Mailchimp`, no `mailchimp`). |

### B9 — Automatizaciones

| # | Decisión |
|---|----------|
| B9.1 | **Construir el puente de carrito abandonado** Magento → Mailchimp e-commerce API (`POST /carts`). Es el gap que mantiene la automatización diseñada pero inactiva. |
| B9.2 | Post-compra: **queda para una fase posterior** (requiere evento de orden entregada). |

### B10 — Operativo / analítica

| # | Decisión |
|---|----------|
| B10.2 | Defaults operativos se mantienen (prueba dayanmartin@gmail.com · reply-to ventas@ligier.com.ar · 10:30 GMT-3). |
| B10.3 | 🐛 Fix: conversión de timezone explícita en la programación (no offset fijo +3h que asume server UTC). |
| B10.4 | **A/B de subjects vía campañas `variate`**: el wizard pide subject A y B, la app crea el A/B test en Mailchimp. |
| B10.5 | `analyze.js` suma las 4 dimensiones faltantes: subjects/preheaders, performance de flujos, detección de dormidos, tendencia temporal. |

---

## B. CONTRATO DE INYECCIÓN v4 (propuesta de marcadores)

Toda plantilla viva DEBE contener estos anclajes. Son la API entre los dos repos — intocables sin versionar el contrato.

| Marcador | Inyecta | Obligatorio en |
|----------|---------|----------------|
| `<p class="hero-eyebrow">` | eyebrow `TIPO · MES AÑO` | todas |
| `<h1 class="hero-h1">` | título (\n → `<br>`) | todas |
| `<p class="hero-bajada">` | bajada | todas |
| `<div class="preheader">` | texto de preview | todas |
| `<!-- INJECT:PRODUCTS_START -->` / `<!-- INJECT:PRODUCTS_END -->` | bloque de productos | vinos, whisky, guardados, regalos |
| `<!-- INJECT:ACC_START -->` / `<!-- INJECT:ACC_END -->` | accesorio (o se elimina) | tipos con productos |
| `<p class="pack-total">` | total real del carrito | solo vinos |
| `<!-- INJECT:PROMO_START -->` / `<!-- INJECT:PROMO_END -->` | banner 6×5 (se elimina si qty < 6) | solo vinos |
| URL `compartircarrito/...` | link del carrito compartido | solo vinos |
| `IMAGEN_SILVER/GOLD/PLATINUM/BLACK` | imágenes Magento de membresías | guardados, wine-club |

Reglas del contrato:
1. Cambiar un marcador = cambio coordinado en ambos repos, mismo PR/día.
2. Toda plantilla nueva se valida contra esta tabla antes de pasar a `templates/`.
3. La app nunca depende de comentarios de sección decorativos ni de colores como anclaje.

---

## C. PLAN DE TRABAJO POR FASES

### Fase 1 — Contrato v4 + bugs (sincroniza ambos repos, base de todo)
- [ ] Plantillas: migrar anclajes a `INJECT:*` + `hero-eyebrow` por clase (3 vivas)
- [ ] Guideline: sección "API de inyección" con la tabla del contrato
- [ ] App: `getCartTotal()` activo, condición `Σqty ≥ 6`, eliminar banner/pack si no califica
- [ ] App: fix URL raw (`Mailchimp`) + fix timezone explícito

### Fase 2 — Tipos completos
- [ ] `base-email-experiencias.html` (base: `campanas/2026-08-ligier-experience-8.html`)
- [ ] `base-email-wineclub.html` · `base-email-giftcards.html` · `base-email-regalos.html`
- [ ] App: rama sin productos (experiencias/wine-club/gift-cards) + tipo regalos en wizard
- [ ] Guideline: quitar recetas de espirituosas; actualizar mapa tipo→plantilla

### Fase 3 — Limpieza de wizard y copy
- [ ] `copy-library.json` en este repo como fuente única (subjects/preheaders/títulos/bajadas por tipo)
- [ ] App: consumir el JSON vía raw; eliminar `src/copy-library.js` y defaults del servidor
- [ ] Wizard: quitar accesorio "auto" y campos `tienePromo`/`rango`; validación de H1

### Fase 4 — Técnico email (solo plantillas + bloques generados)
- [ ] Botones bulletproof en las plantillas y en `buildProductBlock`/`buildAccessoryBlock`
- [ ] Scaffolding MSO + VML hero guardados + `role="presentation"` + tap targets ≥ 44px
- [ ] Regenerar assets (logo/íconos) sobre fondo blanco sólido

### Fase 5 — Automatización y analítica
- [ ] Puente carrito abandonado Magento → Mailchimp (`POST /carts`) en `api/`
- [ ] Campañas A/B `variate` desde el wizard
- [ ] `analyze.js`: subjects/preheaders, flujos, dormidos, tendencia temporal
- [ ] (Posterior) puente post-compra cuando exista evento de orden

---

## D. CAMBIOS AL GUIDELINE (v3.1 → v4.0)

1. §107-110: ya correcto ("se lee del carrito") — ahora la app lo cumple. Agregar: "la condición del 6×5 es Σ cantidades ≥ 6 botellas, no cantidad de etiquetas".
2. §9 y nueva sección: reemplazar lista parcial de marcadores por la tabla del contrato v4.
3. §147: eliminar sección de recetas de cóctel de espirituosas.
4. §160-164 (REGALOS): pasa de "definido sin plantilla" a tipo vivo con plantilla y wizard.
5. §166-178: Wine Club / Experiencias / Gift Cards referencian sus plantillas propias.
6. §283-286 (accesorio): "lo elige el usuario (URL) o no hay accesorio" — eliminar referencia a defaults.
7. Nueva sección "Identidad web": serif editorial (Fraunces/Georgia) permitida SOLO en piezas web; Arial sigue siendo ley en email. Referencia: `landing/ligier-experience-8.html`.
8. §322-328 (backlog): los ítems A3/A4/M3/M4/M5/A2 pasan de backlog a obligatorios en v4.
