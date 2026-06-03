# Ligier — Guía de Emails
> Versión 3.1 — Documento único y coherente. Reemplaza todas las versiones anteriores.
> Cada regla es obligatoria. Lo que no está permitido, está prohibido.

> **Novedades v3.1 (junio 2026):**
> - Toda plantilla lleva **preheader oculto** (texto de preview en la bandeja) y **meta de dark mode** (`color-scheme: light only`). Ver "TÉCNICO OBLIGATORIO".
> - **Plantillas vivas:** `base-email-vinos.html`, `base-email-whisky.html` (whisky + espirituosas), `base-email-guardados.html`. Las legacy `vinos-v1.html` y `vinos-miercoles-28mayo.html` se movieron a `archive/` (no usar).
> - **Estrategia y automatizaciones:** ver `estrategia/` (estrategia de email marketing + auditoría de diseño) y `automatizaciones/` (carrito abandonado, post-compra, guía de Customer Journeys).
> - **Marcadores de inyección** que la app (`ligier-app`) necesita y que NO se deben tocar: `class="hero-bajada"`, `class="pack-total"` (solo vinos), `<!-- ACC_START -->`/`<!-- ACC_END -->`, `<!-- Producto 1 -->`, eyebrow con `color:#666` (oscuro) o `rgba(255,255,255,0.5)` (sobre imagen). El eyebrow `#666` debe ser el primero del documento.

---

## ⛔ REGLAS QUE NUNCA SE ROMPEN

1. Solo Arial como fuente — nunca Google Fonts, serif, monospace
2. Sin border-radius — nunca esquinas redondeadas
3. Sin sombras ni gradientes — nunca box-shadow, text-shadow, gradient
4. Solo los colores de la paleta definida
5. Las secciones van siempre en el orden fijo definido para cada tipo
6. Productos solo de la categoría correcta — nunca mezclar categorías
7. Nunca poner precio ni promo en el H1
8. Nunca usar logos de Instagram con gradiente de colores
9. Todo producto incluido debe tener stock e imagen verificados
10. El diseño debe verse perfecto en desktop Y en mobile

---

## PALETA DE COLORES

| Nombre | Hex | Uso |
|--------|-----|-----|
| Negro fondo | `#1a1a1a` | Hero · Categorías · Secciones oscuras |
| Negro texto/botón | `#111` | Texto principal · Botones sobre claro |
| Blanco | `#fff` | Header · Productos · CTA · Contacto · Footer |
| Crema | `#f4f1ec` | Fondo exterior · Accesorio |
| Gris medio | `#888` | Texto secundario · Descripciones |
| Gris claro | `#aaa` | Labels · Eyebrows · Precio tachado |
| Gris borde | `#f0f0f0` | Separadores |
| Gris datos | `#555` | Dirección · Horarios |

---

## TIPOGRAFÍA

Fuente: `Arial, sans-serif` — única, sin excepciones.

| Elemento | Tamaño desktop / mobile | Peso | Color |
|----------|------------------------|------|-------|
| Eyebrow | 9–10px | 700 | `#aaa` o `#666` sobre oscuro |
| H1 Hero | 34px / 26px | 700 | `#fff` |
| H2 sección | 20–22px | 700 | `#111` |
| Nombre producto | 14px | 700 | `#111` |
| Descripción producto | 13px | 400 | `#888` |
| Precio individual | 18px | 700 | `#111` |
| Precio tachado (6x5) | 12px | 400 | `#aaa` |
| Precio promo (6x5) | 22px | 700 | `#111` |
| Botón | 10–11px | 700 | según botón |

H1: máx 3 líneas, máx 6 palabras por línea, sin punto final, sin precio, sin promo.

---

## BOTONES — 4 TIPOS

| Tipo | Estilo | Uso |
|------|--------|-----|
| 1 — Hero | fondo `#fff`, texto `#111`, padding 13px 28px | Solo Hero |
| 2 — Primario | fondo `#111`, texto `#fff`, padding 9–14px | Comprar · Pack · CTA · Aprovechar |
| 3 — Outline | transparente, borde 1.5px `#111`, texto `#111` | Solo Accesorio |
| 4 — Pill | transparente, borde 1px `#333`, texto `#ccc` | Solo Categorías |

Sin border-radius en ninguno.

---

## PROMO 6×5 — SOLO EN VINOS

| Tipo | Categoría | Promo 6×5 | Botón pack | Banner promo |
|------|-----------|-----------|------------|--------------|
| **Vinos** | /vino | ✅ SÍ | ✅ SÍ | ✅ SÍ |
| Whisky | /whisky | ❌ NO | ❌ NO | ❌ NO |
| Espirituosas | /espirituosas | ❌ NO | ❌ NO | ❌ NO |
| Vinos Guardados | /vinos-guardados | ❌ NO | ❌ NO | ❌ NO |
| Wine Club | /contenido-wineclub | ❌ NO | ❌ NO | ❌ NO |
| Experiencias | /contenido-experiencias | ❌ NO | ❌ NO | ❌ NO |
| Gift Cards | /gift-card-ligier.html | ❌ NO | ❌ NO | ❌ NO |

**El 6x5 aplica EXCLUSIVAMENTE a la categoría Vinos (/vino). Ningún otro tipo lo lleva.**

---

## CÓMO SE MUESTRA EL PRECIO

### En Vinos (con 6x5)
Cada producto muestra 3 líneas:
1. Precio original tachado — 12px · `#aaa` · `line-through`
2. Precio 6x5 — 22px · 700 · `#111` — calculado como `redondear(precio × 5/6)`
3. Label fijo — 9px · 700 · UPPERCASE · `#888` — texto: `"C/U COMPRANDO 6"`

> El cálculo precio×5/6 por producto es correcto porque el cliente puede comprar 6 botellas iguales.

### En todos los demás tipos (whisky, espirituosas, guardados, etc.)
Cada producto muestra solo el precio individual:
- Precio — 18px · 700 · `#111` — tal como figura en el sitio

### Total del pack (solo en Vinos)
El bloque del pack muestra el total REAL leído del carrito (donde la botella más barata va gratis):
- "Total 6x5: $[VALOR_REAL] · pagás 5, llevás 6"
- El valor se lee del carrito en `<tr class="grand totals">` → `<span class="price">`
- Nunca se calcula — siempre se lee del carrito

---

## CANTIDAD DE PRODUCTOS

Libre. La campaña define cuántos productos van (1, 2, 3… hasta 10). No hay número fijo.

---

## ESTRUCTURA POR TIPO

### VINOS (/vino) — estructura completa
```
1. Header (logo 140px)
2. Hero (fondo #1a1a1a)
3. Promo Banner 6x5
4. Productos (precio con 6x5)
5. Botón Pack (total real del carrito)
6. Accesorio
7. CTA Central
8. Categorías
9. Contacto
10. Footer
```

### WHISKY (/whisky)
Igual que Vinos PERO:
- Sin Promo Banner
- Sin Botón Pack
- Precio individual (sin 6x5)
- Accesorio: vasos Glencairn, old fashioned, sets de whisky
- Eyebrow: "WHISKY · [MES AÑO]"

### ESPIRITUOSAS (/espirituosas)
Igual que Whisky PERO:
- Precio individual (sin 6x5)
- Sección extra de recetas de cóctel después del accesorio (fondo #1a1a1a)
- Concepto "armá tu barra"
- Accesorio: herramientas de coctelería

### VINOS GUARDADOS (/vinos-guardados)
Igual que Whisky PERO:
- Hero con imagen de cava: `https://vinotecaligier.com/media/wysiwyg/fondo_banner_vg.jpg` con overlay oscuro
- Eyebrow: "VINOS GUARDADOS · LIGIER" (sin mes ni año)
- Sección de membresías Wine Club (complementaria) antes del CTA
- Sección de financiación antes del CTA
- Label de producto: `[CEPA] · [REGIÓN] · [AÑO COSECHA]`
- Descripciones más largas (hasta 3 líneas)

### REGALOS (/regalos-2026)
- 1 regalo, foto grande
- Detalle de los productos que componen el regalo
- Sin 6x5, sin pack
- CTA: "Regalá esta selección"

### WINE CLUB (/contenido-wineclub)
- Sin productos
- Hero del concepto del club
- 4 membresías (Silver/Gold/Platinum/Black)
- Financiación
- CTA fuerte a suscripción

### EXPERIENCIAS (/contenido-experiencias)
- Sin productos
- Hero de la experiencia
- Descripción (fecha, lugar, qué incluye)
- Financiación
- CTA a reserva

---

## COPY — VOZ DE LIGIER

1. El email no vende — informa sobre lo que Ligier seleccionó
2. Tono curador, no vendedor
3. Sin superlativos: increíble, espectacular, imperdible, único, el mejor
4. Sin exclamaciones
5. La promo va en la bajada del hero y el banner — nunca en el H1
6. Descripciones de producto: directo al carácter, máx 2 líneas (3 en guardados)

### Títulos por tipo (rotan por campaña)

**Vinos** — voz de curador, primera persona plural:
- "Esta semana, elegimos seis."
- "Difícil quedarse con uno solo."
- "Seis etiquetas que conocemos de memoria."

**Vinos Guardados** — tiempo, rareza, irreversibilidad. Máx 2 líneas × 5 palabras. Sin verbos de acción:
- "Algunos vinos no vuelven."
- "El tiempo hizo el trabajo."
- "Botellas que ya no se repiten."

---

## H1 — PROHIBIDO

- Punto final
- Precio o promo
- Empezar con NO, ¡ o ¿
- Superlativos
- Más de 3 líneas o más de 6 palabras por línea

---

## SECCIONES FIJAS (contenido idéntico en todos los emails)

### Categorías — 10 pills, este orden, estos links
| Texto | URL |
|-------|-----|
| VINOS | https://vinotecaligier.com/vino |
| GUARDADOS | https://vinotecaligier.com/vinos-guardados |
| ESPUMANTES | https://vinotecaligier.com/espumantes |
| WHISKY | https://vinotecaligier.com/whisky |
| ESPIRITUOSAS | https://vinotecaligier.com/espirituosas |
| REGALOS | https://vinotecaligier.com/regalos |
| GIFT CARDS | https://vinotecaligier.com/gift-card-ligier.html |
| WINE CLUB | https://vinotecaligier.com/contenido-wineclub |
| EXPERIENCIAS | https://vinotecaligier.com/contenido-experiencias |
| OFERTAS | https://vinotecaligier.com/ofertas |

Los pills DEBEN tener `white-space: nowrap` o el texto se rompe letra por letra en mobile.

### Contacto
- WhatsApp: `https://wa.me/5491170546060`
- Teléfono: `tel:+541120401252`
- Instagram @ligier: `https://www.instagram.com/ligier`
- Instagram @vinosguardados: `https://www.instagram.com/vinosguardados`
- Email: `ventas@ligier.com.ar`
- Dirección: `J. D. Perón 1621, C.A.B.A.`
- Horarios: `Lun–Vie 10:00–18:00 · Sáb 10:00–13:00`

### Íconos de contacto (PNGs de mcusercontent — Mailchimp bloquea SVG y CDNs externos)
- WhatsApp: `https://mcusercontent.com/14b7b2be6d99dcac6ed81f35c/images/5660aedf-265a-c31e-44e8-721cc53da96f.png`
- Teléfono: `https://mcusercontent.com/14b7b2be6d99dcac6ed81f35c/images/f346b0f0-d6be-eac4-b520-541808d693dc.png`
- Instagram: `https://mcusercontent.com/14b7b2be6d99dcac6ed81f35c/images/4f18a0b0-eb4d-9ed9-9c1a-bcaf9dd32a1c.png`

Instagram en negro monocromático. Cada cuenta en su propia fila.

### Footer
- Tagline: "Tu vinoteca online de confianza"
- `*|UNSUB|*`
- Sin logo

### Logo (solo header)
`https://mcusercontent.com/9e298a0f4024c9f23fd6646af/images/3dc5a20a-d835-346a-d331-56796a1934b6.png` — 140px

---

## WINE CLUB — 4 MEMBRESÍAS

| Plan | Precio/mes | URL |
|------|-----------|-----|
| Silver | $160.000 | https://vinotecaligier.com/wine-club-silver.html |
| Gold | $330.000 | https://vinotecaligier.com/wine-club-gold.html |
| Platinum | $470.000 | https://vinotecaligier.com/wine-club-platinum.html |
| Black | $750.000 | https://vinotecaligier.com/wine-club-black-1.html |

Black se destaca con fondo blanco. Las imágenes se obtienen de Magento por url_key.
Banner Wine Club: `https://vinotecaligier.com/media/wysiwyg/detalle_vg_wineclub.png`

---

## FINANCIACIÓN (Guardados, Wine Club, Experiencias)

- 3 cuotas sin interés: Visa, Mastercard y Amex bancarias
- 6 cuotas sin interés: American Express tarjetas propietarias

---

## ACCESORIO

- Lo elige el usuario (pega la URL del producto)
- 1 producto, layout imagen izquierda + info derecha
- Botón 3 (outline): "VER PRODUCTO"
- Debe ser afín al tipo de email

---

## RESPONSIVE — OBLIGATORIO

`@media only screen and (max-width: 480px)`:
- H1: 26px, ninguna línea cortada
- Productos: imagen al costado (80–90px), NUNCA apilada
- Accesorio: imagen al costado
- Contacto: columnas apiladas
- Pills: `white-space: nowrap`, fluyen en varias filas
- Banner promo: botón APROVECHAR se apila debajo del texto a full ancho

---

## TÉCNICO OBLIGATORIO (v3.1)

### Preheader (texto de preview en la bandeja)
Justo después de `<body>`, antes de la tabla `.wrap`:
```html
<div class="preheader" style="display:none; max-height:0; overflow:hidden; mso-hide:all; font-size:1px; line-height:1px; color:#f4f1ec; opacity:0;">
  [texto de preview — complementa el subject, no lo repite]
  &#847;&zwnj;&nbsp;&#847;&zwnj;&nbsp;&#847;&zwnj;&nbsp;&#847;&zwnj;&nbsp;
</div>
```
Los caracteres de relleno evitan que Gmail arrastre texto del cuerpo al preview.

### Dark mode
En `<head>`:
```html
<meta name="color-scheme" content="light only">
<meta name="supported-color-schemes" content="light only">
```
y en `<style>`: `:root { color-scheme: light only; supported-color-schemes: light only; }`
Pendiente de assets: servir logo e íconos sobre fondo blanco sólido (no transparente) para blindar Apple Mail/Gmail dark.

### Backlog v3.1 (mejora incremental, no bloqueante — ver `estrategia/auditoria-diseno-plantillas.md`)
- Botones bulletproof: padding en `<td bgcolor>`, no en `<a>` (Outlook ignora padding en links).
- Scaffolding MSO: `xmlns:v/o`, `<o:OfficeDocumentSettings>`, `mso-line-height-rule:exactly`.
- VML para el fondo del hero de Guardados.
- `role="presentation"` en todas las tablas de layout.
- Tap targets de pills ≥ 44px en mobile.

---

## OPERATIVO — CADA ENVÍO

| Parámetro | Valor |
|-----------|-------|
| Correo de prueba | el que indique el usuario (default dayanmartin@gmail.com) |
| Reply-to | ventas@ligier.com.ar |
| Hora de envío | la que indique el usuario (default 10:30 AM GMT-3) |

---

## CHECKLIST FINAL

### Estructura
- [ ] Secciones en orden correcto según el tipo
- [ ] Cantidad de productos según la campaña
- [ ] Accesorio (si corresponde)
- [ ] 10 categorías completas

### Diseño
- [ ] Logo 140px solo en header
- [ ] Sin border-radius, sombras ni gradientes
- [ ] Solo Arial
- [ ] Fondo exterior #f4f1ec
- [ ] Íconos mcusercontent, Instagram monocromático

### Precio
- [ ] Vinos: 6x5 por producto + total real del carrito
- [ ] Resto: precio individual limpio
- [ ] Total del pack leído del carrito, nunca calculado

### Copy
- [ ] H1 sin punto, sin promo, máx 3 líneas
- [ ] Sin superlativos ni exclamaciones

### Mobile
- [ ] Pills con white-space: nowrap
- [ ] Imágenes de producto al costado
- [ ] Banner promo apila bien
