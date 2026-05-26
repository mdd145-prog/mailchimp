# Ligier Email Guidelines — Reglas Absolutas
> Versión 2.0 — Formato estricto para Claude Code
> Cada regla es obligatoria. Lo que no está permitido, está prohibido.

---

## ⛔ REGLAS QUE NUNCA SE ROMPEN

1. Solo Arial como fuente — ❌ nunca Google Fonts, serif, monospace
2. Sin border-radius en ningún elemento — ❌ nunca esquinas redondeadas
3. Sin sombras ni gradientes — ❌ nunca box-shadow, text-shadow, gradient
4. Solo los colores de la paleta definida — ❌ nunca inventar colores
5. 9 secciones siempre en orden fijo — ❌ nunca omitir ni reordenar
6. 6 productos siempre — ❌ nunca 5, nunca 7
7. Productos solo de la categoría correcta — ❌ nunca mezclar categorías
8. ❌ Nunca calcular precios 6x5 manualmente
9. ❌ Nunca poner precio ni promo en el H1
10. ❌ Nunca usar logos de Instagram con gradiente de colores

---

## PALETA DE COLORES

| Variable | Hex | Uso exclusivo |
|----------|-----|---------------|
| Negro fondo | `#1a1a1a` | Hero · Categorías |
| Negro texto/botón | `#111` | Texto principal · Botones sobre blanco |
| Blanco | `#fff` | Header · Productos · CTA · Contacto · Footer |
| Crema | `#f4f1ec` | Fondo exterior · Accesorios |
| Gris medio | `#888` | Texto secundario · Descripciones |
| Gris claro | `#aaa` | Labels · Eyebrows |
| Gris borde | `#f0f0f0` | Separadores |
| Gris datos | `#555` | Dirección · Horarios |

---

## TIPOGRAFÍA

Fuente: `Arial, sans-serif` — única, sin excepciones.

| Elemento | Tamaño | Peso | Color | Extra |
|----------|--------|------|-------|-------|
| Eyebrow | 9–10px | 700 | `#aaa` | 3px spacing · UPPERCASE |
| H1 Hero | 34px / 26px mobile | 700 | `#fff` | -1px spacing · máx 3 líneas · máx 6 palabras/línea · sin punto final |
| H2 sección | 20–22px | 700 | `#111` | -0.5px spacing · sin punto final |
| Nombre producto | 14px | 700 | `#111` | — |
| Descripción producto | 13px | 400 | `#888` | line-height 1.5 · máx 2 líneas |
| Precio | 16px | 700 | `#111` | — |
| Botón | 10–11px | 700 | según botón | 1.5–2px spacing · UPPERCASE |
| Label contacto | 9–10px | 400 | `#aaa` | 1–2px spacing · UPPERCASE |
| Valor contacto | 13px | 700 | `#111` | — |

---

## BOTONES — 4 TIPOS, NO MÁS

### Botón 1 — Hero (sobre fondo oscuro)
```
background: #fff | color: #111 | padding: 13px 28px
font-size: 11px | font-weight: 700 | letter-spacing: 2px | UPPERCASE
```
✅ Solo en sección Hero

### Botón 2 — Primario (sobre fondo claro)
```
background: #111 | color: #fff | padding: 9px 18px (productos) / 14px 32–36px (pack/CTA)
font-size: 10–11px | font-weight: 700 | letter-spacing: 1.5–2px | UPPERCASE
```
✅ Botón "Comprar" · Botón Pack · Botón CTA central · Botón "APROVECHAR"

### Botón 3 — Outline (accesorio)
```
background: transparent | border: 1.5px solid #111 | color: #111 | padding: 9px 18px
font-size: 10px | font-weight: 700 | letter-spacing: 1.5px | UPPERCASE
```
✅ Solo en sección Accesorio · texto: "VER PRODUCTO"

### Botón 4 — Pill categoría (sobre fondo negro)
```
background: transparent | border: 1px solid #333 | color: #ccc | padding: 7–8px 14px
font-size: 10–11px | font-weight: 700 | letter-spacing: 1–1.5px | UPPERCASE
```
✅ Solo en sección Categorías

---

## ESTRUCTURA — 9 SECCIONES EN ORDEN FIJO

```
1. HEADER
2. HERO
3. PROMO BANNER 6×5
4. PRODUCTOS (6 vinos)
4b. BOTÓN PACK
5. ACCESORIO
6. CTA CENTRAL
7. CATEGORÍAS
8. CONTACTO
9. FOOTER
```

---

## ESPECIFICACIONES POR SECCIÓN

### 1. HEADER
```
background: #fff
padding: 24px 32–40px
contenido: logo centrado, width=140px, link a vinotecaligier.com
border-bottom: 1px solid #f0f0f0
logo URL: https://mcusercontent.com/9e298a0f4024c9f23fd6646af/images/3dc5a20a-d835-346a-d331-56796a1934b6.png
```

### 2. HERO
```
background: #1a1a1a
padding: 48px 40px 40px desktop / 32px 24px 28px mobile
alineación: izquierda
```
Estructura interna (en orden):
1. Eyebrow: `[CATEGORÍA] · [MES AÑO]` — 10px · 3px spacing · UPPERCASE · `#666`
2. H1: máx 3 líneas · máx 6 palabras/línea · sin punto · sin promo · sin precio
3. Bajada: 15px · `#aaa` · máx 2 líneas · la promo se menciona acá, no en el H1
4. Botón 1

**H1 — ejemplos aprobados:**
- ✅ "Esta semana, / elegimos seis."
- ✅ "Difícil / quedarse / con uno solo."
- ✅ "Seis etiquetas / que conocemos / de memoria."

**H1 — ejemplos prohibidos:**
- ❌ Cualquier título con punto final
- ❌ Cualquier título que mencione precio o promo
- ❌ Cualquier título que empiece con NO, ¡ o ¿
- ❌ Títulos de más de 3 líneas o más de 6 palabras por línea

### 3. PROMO BANNER 6×5
```
background exterior: #1a1a1a
padding exterior: 0 40px 32px
caja interior: background #fff · padding 16–20px 20–24px
layout: 2 columnas — texto izquierda · botón derecha (alineado verticalmente al centro)
```
Columna izquierda:
- Label: "PROMOCIÓN ACTIVA" — 9–10px · 2px spacing · UPPERCASE · `#888`
- Título: "Llevá 6, pagá 5" — 16–18px · 700 · `#111`
- Descripción fija: "Válido en toda la selección de vinos. Podés mezclar etiquetas." — 13px · `#888`

Columna derecha:
- Botón 2: texto "APROVECHAR" · link al carrito compartido de los 6 productos

❌ Nunca poner ejemplos de precio con productos específicos
❌ Nunca poner el botón debajo del texto — siempre a la derecha

### 4. PRODUCTOS
```
background: #fff
padding: 32px 32px 8px
cantidad: exactamente 6 productos
separador: border-bottom: 1px solid #f0f0f0 · padding-bottom: 24px · margin-bottom: 24px
el último producto no lleva separador inferior
```
Estructura de cada producto:
1. Imagen: `width=140px` · columna de 150px · `height: auto` · `display: block`
2. Label: `[Cepa] · [Región] · [Provincia]` — 9px · 2px spacing · UPPERCASE · `#aaa`
3. Nombre: 14px · 700 · `#111`
4. Descripción: 13px · `#888` · line-height 1.5 · máx 2 líneas
5. Precio — layout aprobado (opción A):
   - Línea 1: precio original tachado — 12px · `#aaa` · `text-decoration:line-through`
   - Línea 2: precio promo 6x5 — 22px · 700 · `#111` · `line-height:1` — protagonista visual
   - Línea 3: label — 9px · 700 · 1px spacing · UPPERCASE · `#888` — texto fijo: `"c/u comprando 6"`
   - Cálculo precio promo: `redondear(precio × 5 / 6)` con punto como separador de miles
   - Solo aplica en emails con promo 6x5 (vinos, whisky, espirituosas)
6. Botón 2 pequeño: "COMPRAR"

❌ Nunca mostrar total de 6 botellas calculado — ese valor se lee del carrito
❌ Nunca incluir productos sin stock o sin imagen
❌ Nunca mostrar precio 6x5 en Vinos Guardados, Wine Club, Experiencias o Gift Cards

### 4b. BOTÓN PACK
```
background: #fff
padding: 8px 32px 32px
alineación: centrado
```
- Botón 2 grande: "LLEVÁ EL PACK COMPLETO · 6 BOTELLAS"
- href: link de carrito compartido generado con los 6 SKUs
- Debajo del botón: "Total 6x5: $[VALOR_REAL] · pagás 5, llevás 6" — 11px · `#aaa`

**Cómo obtener el valor real:**
1. Generar el link de carrito con los 6 SKUs
2. Navegar ese link en el sitio
3. Leer el total que muestra Magento en el resumen del carrito
4. **Navegar el link una segunda vez** para confirmar que el valor es el mismo
5. Usar ese número exacto en el email

❌ Nunca poner un valor estimado o calculado
❌ Nunca dejar el campo vacío o con un placeholder como "$XXX.XXX"
❌ Si el carrito no muestra el total, intentarlo 2 veces más antes de reportar el problema
❌ El valor debe incluir el descuento 6x5 aplicado por Magento — si los 6 precios individuales suman más que el total del carrito, está bien, eso es la promo aplicada

**Cómo generar el link de carrito:**
```
JSON = [{"sku":"SKU1","qty":1},{"sku":"SKU2","qty":1},... hasta 6]
LINK = https://vinotecaligier.com/compartircarrito/index/share/data/ + btoa(JSON) + /
```

### 5. ACCESORIO
```
background: #f4f1ec
padding: 32px
label: "COMPLEMENTÁ TU EXPERIENCIA" — 10px · 2px spacing · UPPERCASE · #888
cantidad: 1 producto
layout: imagen izquierda (140px) + info derecha
```
Estructura:
1. Imagen: `width=140px` · `height: auto`
2. Label: `[Categoría] · [Marca]` — 9px · UPPERCASE · `#aaa`
3. Nombre: 14px · 700 · `#111`
4. Descripción: 13px · `#888` · máx 2 líneas
5. Precio: 16px · 700 · `#111`
6. Botón 3: "VER PRODUCTO"

**Regla de selección:**
- Navegar `/cristaleria` o `/accesorios`
- Elegir el producto más afín a los vinos del email:
  - Tintos Mendoza → copas para tintos (Cabernet, Burgundy)
  - Blancos → copas para blancos o champagne
  - Whisky → vasos Glencairn o old fashioned
  - Espirituosas → herramientas coctelería
  - Guardados → copas premium de colección

### 6. CTA CENTRAL
```
background: #fff
padding: 36–40px 32–40px
alineación: centrado
```
1. Label: "TODA LA SELECCIÓN" — 10px · 2px spacing · UPPERCASE · `#888`
2. H2: 20–22px · 700 · `#111` · sin punto final
3. Botón 2 grande

### 7. CATEGORÍAS
```
background: #1a1a1a
padding: 28–32px 32–40px
alineación: centrado
label: "TAMBIÉN TENEMOS" — 9px · 2px spacing · UPPERCASE · #555
```
Lista fija — exactamente estas 10, en este orden, con estos links:

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

❌ Nunca omitir ninguna categoría
❌ Nunca agregar categorías fuera de esta lista

### 8. CONTACTO
```
background: #fff
padding: 32px
título: "CONTACTO" — 9px · 3px spacing · UPPERCASE · #aaa · centrado
layout: 2 columnas — border-right: 1px solid #f0f0f0
mobile: columna única — border-bottom: 1px solid #f0f0f0
```
Columna izquierda:
1. Ícono WhatsApp oficial (SVG verde `#25D366`, 28px) + "WhatsApp" + link `https://wa.me/5491170546060`
2. Ícono teléfono (círculo `#1a1a1a`, 28px) + "Teléfono" + link `tel:+541120401252`
3. Dos íconos Instagram **monocromáticos negros**, cada uno en su propia fila con label y handle:
   - Ícono: `https://img.icons8.com/ios-filled/48/111111/instagram-new--v1.png` — 28×28px
   - Fila 1: label "INSTAGRAM" + `@ligier` → `https://www.instagram.com/ligier`
   - Fila 2: label "VINOS GUARDADOS" + `@vinosguardados` → `https://www.instagram.com/vinosguardados`
   - Separación entre filas: `margin-bottom: 14px`

**URLs de íconos aprobadas (mcusercontent — no cambiar):**
- WhatsApp: `https://mcusercontent.com/14b7b2be6d99dcac6ed81f35c/images/5660aedf-265a-c31e-44e8-721cc53da96f.png`
- Teléfono: `https://mcusercontent.com/14b7b2be6d99dcac6ed81f35c/images/f346b0f0-d6be-eac4-b520-541808d693dc.png`
- Instagram: `https://mcusercontent.com/14b7b2be6d99dcac6ed81f35c/images/4f18a0b0-eb4d-9ed9-9c1a-bcaf9dd32a1c.png`

❌ Nunca usar SVG inline — Mailchimp los elimina
❌ Nunca usar servicios externos (icons8, mailchimp CDN social-block) — se bloquean
✅ Siempre usar las URLs de mcusercontent de arriba

Columna derecha:
- Email: `ventas@ligier.com.ar`
- Dirección: `J. D. Perón 1621, C.A.B.A.`
- Horarios: `Lun–Vie 10:00–18:00 · Sáb 10:00–13:00`

### 9. FOOTER
```
background: #fff
padding: 24px 32px
alineación: centrado
border-top: 1px solid #f0f0f0
```
1. Tagline: "Tu vinoteca online de confianza" — 11–12px · `#888`
2. Link desuscripción: `*|UNSUB|*` — 10–11px · `#bbb` · subrayado

❌ No repetir el logo en el footer

---

## PROMO 6×5 — QUÉS Y EN QUÉ CATEGORÍAS APLICA

| Tipo | URL | Promo 6×5 |
|------|-----|-----------|
| Vinos | /vino | ✅ SÍ |
| Whisky | /whisky | ✅ SÍ |
| Espirituosas | /espirituosas | ✅ SÍ |
| Vinos Guardados | /vinos-guardados | ❌ NO |
| Wine Club | /contenido-wineclub | ❌ NO |
| Experiencias | /contenido-experiencias | ❌ NO |
| Gift Cards | /gift-card-ligier.html | ❌ NO |

---

## RESPONSIVIDAD — OBLIGATORIA

Usar `@media only screen and (max-width: 480px)` con estas reglas mínimas:

```css
.outer-table { padding: 0 !important; }
.main-table { width: 100% !important; }
.header-cell { padding: 20px 24px !important; }
.hero-cell { padding: 32px 24px 28px !important; }
.hero-title { font-size: 26px !important; }
.products-cell { padding: 20px 16px !important; }
/* Productos en mobile: imagen MÁS CHICA pero SIGUE al costado — NUNCA apilar */
.prod-img-col { width: 90px !important; padding-right: 12px !important; }
.prod-img-col img { width: 80px !important; }
/* Accesorio en mobile: igual, imagen al costado */
.acc-img-col { width: 100px !important; padding-right: 12px !important; }
.acc-img-col img { width: 90px !important; }
/* Columnas de contacto: apiladas en mobile */
.cnt-left { display: block !important; width: 100% !important; border-right: none !important; border-bottom: 1px solid #f0f0f0 !important; padding-right: 0 !important; padding-bottom: 20px !important; margin-bottom: 20px !important; }
.cnt-right { display: block !important; width: 100% !important; padding-left: 0 !important; }
.footer-cell { padding: 20px 24px !important; }
```

---

## COPY — REGLAS

1. El email no vende — informa sobre lo que Ligier seleccionó
2. H1 máx 3 líneas × máx 6 palabras — tono curador, no vendedor
3. Sin promo ni precio en el H1
4. Sin superlativos: ❌ increíble · ❌ espectacular · ❌ imperdible · ❌ único · ❌ el mejor
5. Sin exclamaciones
6. Descripciones de productos: máx 2 líneas, directo al carácter del vino
7. La promo se menciona en la bajada del Hero y en el banner — no en el H1

---

## OPERATIVO — OBLIGATORIO EN CADA ENVÍO

| Parámetro | Valor |
|-----------|-------|
| Correo de prueba | dayanmartin@gmail.com — SIEMPRE antes del envío final |
| Reply-to | ventas@ligier.com.ar |
| Hora de envío | 10:30 AM hora Argentina (GMT-3) |

---

## AUTOEVALUACIÓN — CORRER ANTES DE GUARDAR EL ARCHIVO

Antes de guardar el HTML, verificar cada punto. Si alguno falla, corregirlo antes de guardar.

### Estructura
- [ ] 9 secciones en orden correcto
- [ ] 6 productos exactos
- [ ] 1 accesorio
- [ ] 10 categorías completas y con links correctos

### Diseño
- [ ] Logo 140px en header (no en footer)
- [ ] Sin border-radius en ningún elemento
- [ ] Sin sombras ni gradientes
- [ ] Solo Arial
- [ ] Fondo exterior #f4f1ec
- [ ] Íconos WhatsApp e Instagram (monocromáticos)
- [ ] @ligier y @vinosguardados presentes

### Productos
- [ ] Todos de la categoría correcta para el tipo de email
- [ ] Todos con stock verificado
- [ ] Todos con imagen verificada
- [ ] Precios individuales sin cálculos 6x5
- [ ] Link de carrito generado con los 6 SKUs
- [ ] Total del pack obtenido navegando el carrito (no calculado)

### Copy
- [ ] H1: máx 3 líneas · máx 6 palabras · sin punto · sin promo · sin precio
- [ ] Sin superlativos vacíos
- [ ] Sin exclamaciones
- [ ] Descripciones en máx 2 líneas

### Técnico
- [ ] @media max-width: 480px con todas las reglas mobile
- [ ] *|UNSUB|* en footer
- [ ] Reply-to: ventas@ligier.com.ar
- [ ] Todos los links de productos correctos y funcionales


---

## ⛔ REGLA CRÍTICA — GENERACIÓN DE EMAILS

**Claude Code NUNCA genera el HTML desde cero.** Siempre parte del template de referencia.

### Flujo obligatorio:
1. Leer `templates/vinos-malbec-26mayo.html` como base
2. Copiar TODA la estructura HTML, CSS y media queries exactamente
3. Reemplazar SOLO el contenido variable: productos, precios, links, SKUs, hero copy
4. No modificar ningún estilo, clase CSS ni estructura de tablas
5. No reescribir secciones que no cambian (contacto, footer, categorías)

❌ Nunca reescribir el CSS desde cero
❌ Nunca cambiar las clases mobile definidas en el template
❌ Nunca "mejorar" o "simplificar" la estructura de tablas

---

## REGLAS MOBILE CRÍTICAS

### Categorías — pills
```css
/* OBLIGATORIO — sin esto el texto se rompe letra por letra */
a { white-space: nowrap !important; }
.cat-pad a { 
  display: inline-block;
  white-space: nowrap !important;
  padding: 6px 10px;
  margin: 3px;
  font-size: 9px !important;
}
```
❌ Nunca omitir `white-space: nowrap` en los pills de categorías
❌ En mobile los pills deben fluir en múltiples filas pero NUNCA romper el texto

### Banner promo — mobile
```css
.promo-txt { 
  display: block !important; 
  width: 100% !important; 
  padding-right: 0 !important; 
  padding-bottom: 14px !important; 
}
.promo-btn { 
  display: block !important; 
  width: 100% !important; 
  text-align: center !important; 
}
.promo-btn a { width: 100% !important; display: block !important; }
```

### H1 mobile
- Font-size: 26px en mobile (no más grande)
- El título no puede superar el ancho de pantalla
- Verificar que ninguna línea se corte

### H2 CTA
- Máx 6 palabras por línea también en el H2
- En mobile no puede tener más de 2 líneas

---

## VERIFICACIÓN MOBILE OBLIGATORIA

Antes de guardar el archivo Claude Code debe verificar mentalmente:

- [ ] Pills de categorías: ¿tienen `white-space: nowrap`?
- [ ] Banner promo: ¿el botón APROVECHAR se apila correctamente en mobile?
- [ ] H1: ¿26px en mobile? ¿Ninguna línea cortada?
- [ ] Productos: ¿imagen al costado (no apilada)?
- [ ] Contacto: ¿columnas apiladas correctamente?
- [ ] Íconos: ¿usando las URLs de mcusercontent definidas?
