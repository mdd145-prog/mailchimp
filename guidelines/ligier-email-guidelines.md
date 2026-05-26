# Guía de Diseño y Contenido — Emails Ligier
> Documento de referencia para la automatización de emails vía Mailchimp.
> Cada regla aquí definida es obligatoria. No se improvisa, no se omite, no se reemplaza.

---

## PARTE 1 — SISTEMA DE DISEÑO BASE

### 1.1 Paleta de colores

| Nombre | Hex | Uso |
|--------|-----|-----|
| Negro profundo | `#1a1a1a` | Fondo Hero · Fondo Categorías · Botón primario sobre fondo claro |
| Casi negro | `#111` | Texto principal · Botón sobre blanco |
| Blanco | `#ffffff` | Fondo Header · Fondo Productos · Fondo CTA · Fondo Contacto · Fondo Footer |
| Crema | `#f4f1ec` | Fondo general exterior · Fondo sección Accesorios |
| Gris medio | `#888` | Texto secundario · Descripción de productos |
| Gris claro | `#aaa` | Labels · Eyebrows · Precio 6x5 |
| Gris borde | `#f0f0f0` | Separadores entre secciones · Divisores en productos |
| Gris oscuro texto | `#555` | Datos de contacto (dirección, horarios) |

**Regla:** No usar ningún color fuera de esta paleta. No agregar colores de acento, no usar gradientes, no usar colores de marca de terceros en el layout.

---

### 1.2 Tipografía

**Fuente única:** `Arial, sans-serif` — en todos los elementos, sin excepción.

| Elemento | Tamaño | Peso | Espaciado | Color | Transformación |
|----------|--------|------|-----------|-------|----------------|
| Eyebrow / Label | 9–10px | 700 | 2–3px | `#aaa` o `#666` | UPPERCASE |
| H1 Hero | 34px desktop / 26px mobile | 700 | -1px | `#fff` | Normal |
| H2 Sección | 20–22px | 700 | -0.5px | `#111` | Normal |
| Nombre producto | 14px | 700 | normal | `#111` | Normal |
| Bajada Hero | 15px | 400 | normal | `#aaa` | Normal |
| Descripción producto | 13px | 400 | normal | `#888` | Normal, line-height 1.5 |
| Precio principal | 16px | 700 | normal | `#111` | Normal |
| Precio 6x5 unitario | 11px | 400 | normal | `#aaa` | Normal |
| Precio total pack | 11px | 400 | normal | `#888` | Normal |
| Texto botón | 10–11px | 700 | 1.5–2px | según botón | UPPERCASE |
| Label contacto | 9–10px | 400 | 1–2px | `#aaa` o `#888` | UPPERCASE |
| Valor contacto | 13px | 700 | normal | `#111` | Normal |
| Footer tagline | 11–12px | 400 | normal | `#888` | Normal |
| Footer unsub | 10–11px | 400 | normal | `#bbb` | Normal |

---

### 1.3 Botones

Hay exactamente **4 tipos de botón**. No crear variantes nuevas.

#### Botón 1 — Primario sobre fondo oscuro (Hero)
```
Background: #ffffff
Color texto: #111111
Padding: 13px 28px
Font-size: 11px | Font-weight: 700 | Letter-spacing: 2px | UPPERCASE
Sin border-radius (esquinas rectas)
```
Uso: Sección Hero únicamente.

#### Botón 2 — Primario sobre fondo claro
```
Background: #111111
Color texto: #ffffff
Padding: 9px 18px (productos) / 14–15px 32–36px (CTA central y pack)
Font-size: 10–11px | Font-weight: 700 | Letter-spacing: 1.5–2px | UPPERCASE
Sin border-radius
```
Uso: Botón "Comprar" en productos · Botón "Llevá el pack completo" · Botón CTA central.

#### Botón 3 — Outline (Accesorios)
```
Background: transparent
Border: 1.5px solid #111111
Color texto: #111111
Padding: 9px 18px
Font-size: 10px | Font-weight: 700 | Letter-spacing: 1.5px | UPPERCASE
Sin border-radius
```
Uso: Sección de accesorio / cristalería únicamente.

#### Botón 4 — Pill de categoría (sobre fondo negro)
```
Background: transparent
Border: 1px solid #333333
Color texto: #cccccc
Padding: 7–8px 14px
Font-size: 10–11px | Font-weight: 700 | Letter-spacing: 1–1.5px | UPPERCASE
Sin border-radius
```
Uso: Sección Categorías únicamente.

---

### 1.4 Estructura de secciones — orden fijo y obligatorio

El email siempre tiene estas 9 secciones en este orden. No se omite ninguna, no se agrega ninguna fuera de este esquema.

```
1. HEADER
2. HERO
3. PROMO BANNER (6×5)
4. PRODUCTOS (6 vinos)
4b. BOTÓN PACK COMPLETO
5. ACCESORIO / CRISTALERÍA
6. CTA CENTRAL
7. CATEGORÍAS
8. CONTACTO
9. FOOTER
```

---

### 1.5 Especificaciones por sección

#### Sección 1 — HEADER
- Background: `#ffffff`
- Padding: `24px 32–40px`
- Contenido: Logo Ligier centrado
- **Tamaño del logo: 140px de ancho** (height: auto)
- URL logo: `https://mcusercontent.com/9e298a0f4024c9f23fd6646af/images/3dc5a20a-d835-346a-d331-56796a1934b6.png`
- Border-bottom: `1px solid #f0f0f0`
- El logo es un link a `https://vinotecaligier.com`

#### Sección 2 — HERO
- Background: `#1a1a1a`
- Padding: `48px 40px 40px` (desktop) / `32px 24px 28px` (mobile)
- Alineación: izquierda
- Estructura interna (en orden):
  1. Eyebrow: 9–10px, 3px letter-spacing, UPPERCASE, color `#666`
  2. H1: ver reglas de tipografía y copy
  3. Bajada: 15px, color `#aaa`, line-height 1.6, máx 2 líneas
  4. Botón primario sobre oscuro

**Reglas del Eyebrow:**
- Formato: `[CATEGORÍA/CONTEXTO] · [MES AÑO]` — Ej: `Selección Mayo 2026 · Alta Gama`
- Siempre en mayúsculas y con separador `·`

#### Sección 3 — PROMO BANNER 6×5
- Background exterior: `#1a1a1a`
- Padding exterior: `0 40px 32–40px`
- Caja interior: background `#ffffff`, padding `16–20px 20–24px`
- Layout: **2 columnas** — texto a la izquierda, botón a la derecha (alineado al centro vertical)

**Columna izquierda:**
  1. Label: 9–10px, 2px letter-spacing, UPPERCASE, `#888` — texto: `"PROMOCIÓN ACTIVA"`
  2. Título "Llevá 6, pagá 5": 16–18px, 700, `#111`
  3. Descripción: 13px, `#888` — texto fijo: `"Válido en toda la selección de vinos. Podés mezclar etiquetas."`

**Columna derecha:**
  - Botón tipo 2: texto `"APROVECHAR"`, fondo `#111`, color `#fff`
  - El botón linkea al **mismo link de carrito compartido** de los 6 productos del email

**Reglas:**
- **No poner ejemplos de precio** con productos específicos
- **No poner el botón debajo** — siempre a la derecha en la misma línea
- En mobile: el botón se apila debajo del texto

#### Sección 4 — PRODUCTOS
- Background: `#ffffff`
- Padding: `32–40px 32–40px 8px`
- Cantidad fija: **6 productos siempre**
- Separador entre productos: `border-bottom: 1px solid #f0f0f0`, `padding-bottom: 24px`, `margin-bottom: 24px`
- El último producto no lleva separador inferior

**Estructura de cada producto (de arriba a abajo):**
1. Imagen: 140px de ancho, `height: auto`, columna de 150px
2. Label de categoría: 9px, 2px letter-spacing, UPPERCASE, `#aaa` — formato: `[Cepa] · [Región] · [Provincia/País]`
3. Nombre del producto: 14px, 700, `#111`
4. Descripción: 13px, `#888`, line-height 1.5, máx 2 líneas
5. Precio individual: 16px, 700, `#111` — tal como figura en el sitio, sin cálculos
6. Botón "Comprar": Botón tipo 2 pequeño

**NUNCA mostrar precio unitario 6x5 calculado ni total de 6 botellas — el descuento lo aplica Magento en el carrito.**

### REGLA CRÍTICA — Cálculo de la promoción 6×5

**Claude NO debe calcular el precio 6x5 manualmente.** El descuento se aplica sobre la botella más barata del conjunto, no es una división simple de precio × 5/6.

**Regla:** Mostrar únicamente el **precio individual de cada producto** tal como aparece en el sitio. No calcular ni mostrar precios unitarios 6x5 ni totales de pack. El valor real del carrito lo calcula Magento automáticamente cuando el cliente hace clic en el link.

**En cada producto mostrar:**
- Precio individual: tal como figura en el sitio ✅
- ~~Precio unitario 6x5~~ ❌ No calcular
- ~~Total 6 botellas~~ ❌ No calcular

**Cómo funciona la promo 6x5:**
El descuento se aplica sobre la botella más económica del conjunto — no es una división lineal. Por eso Claude nunca calcula este valor manualmente.

**Cómo obtener el total real del pack:**
1. Generar el link de carrito con los 6 SKUs
2. Navegar ese link en el sitio
3. Leer el total que muestra Magento en el carrito
4. Usar ese número exacto en el email

**En el botón pack:**
- Texto: `"Llevá el pack completo · 6 botellas"`
- Debajo del botón: `"Total 6x5: $[VALOR_REAL_DEL_CARRITO] · pagás 5, llevás 6"`
- El valor debe ser el total real leído del carrito — nunca calculado

---

#### Sección 4b — BOTÓN PACK COMPLETO
- Background: `#ffffff`
- Padding: `8px 32px 32px`
- Alineación: centrado
- Botón tipo 2 grande: texto `"Llevá el pack completo · 6 botellas"`
- El href del botón es el **link de carrito compartido** (se genera por campaña)
- Debajo del botón: texto 11px, `#aaa` con el precio total del pack y la aclaración `pagás 5, llevás 6`

#### Sección 5 — ACCESORIO / CRISTALERÍA
- Background: `#f4f1ec`
- Padding: `32px`
- Label superior: `"COMPLEMENTÁ TU EXPERIENCIA"` — 10px, 2px letter-spacing, UPPERCASE, `#888`
- **1 solo producto accesorio**
- Mismo layout que productos: imagen izquierda (140px) + info derecha
- Label categoría: 9px, UPPERCASE, `#aaa`
- Nombre: 14px, 700, `#111`
- Descripción: 13px, `#888`, line-height 1.5
- Precio: 16px, 700, `#111`
- Botón: **Botón tipo 3 (Outline)** con texto `"Ver producto"`

**Regla de selección del accesorio:**
- Debe pertenecer a `/cristaleria` o `/accesorios`
- Debe ser afín a los vinos o bebidas del email — ej: si son tintos de Mendoza, una copa para vinos tintos; si es whisky, un vaso old fashioned
- No poner accesorios genéricos sin relación con el contenido del email

#### Sección 6 — CTA CENTRAL
- Background: `#ffffff`
- Padding: `36–40px 32–40px`
- Alineación: centrado
- Estructura:
  1. Label superior: 10px, 2px letter-spacing, UPPERCASE, `#888` — ej: `"TODA LA SELECCIÓN"`
  2. Título H2: 20–22px, 700, `#111`
  3. Botón tipo 2 grande

#### Sección 7 — CATEGORÍAS
- Background: `#1a1a1a`
- Padding: `28–32px 32–40px`
- Alineación: centrado
- Label superior: `"TAMBIÉN TENEMOS"` o `"EXPLORÁ TODA LA TIENDA"` — 9px, 2–3px letter-spacing, UPPERCASE, `#555`
- **Lista fija y completa de categorías (siempre en este orden):**

| Categoría | URL |
|-----------|-----|
| Vinos | https://vinotecaligier.com/vino |
| Guardados | https://vinotecaligier.com/vinos-guardados |
| Espumantes | https://vinotecaligier.com/espumantes |
| Whisky | https://vinotecaligier.com/whisky |
| Espirituosas | https://vinotecaligier.com/espirituosas |
| Regalos | https://vinotecaligier.com/regalos |
| Gift Cards | https://vinotecaligier.com/gift-card-ligier.html |
| Wine Club | https://vinotecaligier.com/contenido-wineclub |
| Experiencias | https://vinotecaligier.com/contenido-experiencias |
| Ofertas | https://vinotecaligier.com/ofertas |

- Cada categoría usa Botón tipo 4 (Pill)
- Margen entre pills: `4px`
- **No omitir ninguna categoría. No agregar categorías fuera de esta lista.**

#### Sección 8 — CONTACTO
- Background: `#ffffff`
- Padding: `32px`
- Título: `"CONTACTO"` — 9px, 3px letter-spacing, UPPERCASE, `#aaa`, centrado
- Layout: 2 columnas separadas por `border-right: 1px solid #f0f0f0`
- En mobile: columna única, separadas por `border-bottom: 1px solid #f0f0f0`

**Columna izquierda:**
1. WhatsApp — ícono oficial verde WhatsApp (28px) + label + número linkeado a `https://wa.me/5491170546060`
2. Teléfono — ícono oscuro (28px) + label + número linkeado a `tel:+541120401252`
3. Redes sociales — dos íconos Instagram oficiales en fila:
   - `@ligier` → `https://www.instagram.com/ligier`
   - `@vinosguardados` → `https://www.instagram.com/vinosguardados`

**Columna derecha:**
1. Email: `ventas@ligier.com.ar`
2. Dirección: `J. D. Perón 1621, C.A.B.A.`
3. Horarios: `Lun–Vie 10:00–18:00 · Sáb 10:00–13:00`

**Regla íconos:** Usar los íconos oficiales de cada plataforma. WhatsApp: círculo verde `#25D366`. Instagram: gradiente oficial. No reemplazar por letras ni formas genéricas.

#### Sección 9 — FOOTER
- Background: `#ffffff`
- Padding: `24px 32px`
- Alineación: centrado
- Border-top: `1px solid #f0f0f0`
- Estructura:
  1. Logo Ligier: 140px, linkeado a `https://vinotecaligier.com`
  2. Tagline: `"Tu vinoteca online de confianza"` — 11–12px, `#888`
  3. Link de desuscripción: `*|UNSUB|*` — 10–11px, `#bbb`, subrayado

---

### 1.6 Layout y responsividad

- **Ancho máximo del email:** 600px
- **Fondo exterior:** `#f4f1ec`, padding `20–24px 0`
- El email debe verse correctamente en mobile (max-width: 480px)
- En mobile, las columnas de productos se convierten en bloque único (imagen arriba, info abajo)
- En mobile, las columnas de contacto se apilan verticalmente
- En mobile, el padding lateral se reduce a 16–24px

---

### 1.7 Reglas generales de código

- No usar `border-radius` en ningún elemento (botones, cajas, imágenes) — **todo en esquinas rectas**
- No usar sombras (`box-shadow`, `text-shadow`)
- No usar gradientes
- No usar fuentes externas (Google Fonts, etc.) — solo Arial
- Todas las imágenes con `display:block` y `height:auto`
- Todos los links con `text-decoration:none`
- Ancho del email definido con `width:600px` y `max-width:600px`

---

### 1.8 Responsividad — regla obligatoria

**Todo email debe verse perfecto en celular.** No es opcional ni secundario — la mayoría de los destinatarios abre desde el teléfono.

Reglas mínimas de responsividad:
- Usar `@media only screen and (max-width: 480px)` con overrides para cada sección
- En mobile, el email ocupa el 100% del ancho de pantalla
- Padding lateral en mobile: mínimo 16px, máximo 24px
- Las columnas de productos (imagen + info) se convierten en bloque único: imagen centrada arriba, info abajo
- Las 2 columnas de contacto se apilan verticalmente con separador horizontal
- El H1 Hero reduce a 26px en mobile
- Los botones mantienen su padding y son fácilmente tapeables (mínimo 44px de alto)
- Ningún texto queda cortado ni desbordado en pantallas angostas
- Las imágenes de productos escalan correctamente (`width: 100% !important` cuando corresponde)

---

### 1.9 Calidad y cuidado del diseño

El diseño de cada email debe estar **cuidado al máximo detalle**, como si fuera una pieza de comunicación de una marca premium. Esto implica:

- Alineaciones perfectas en todos los elementos
- Espaciados consistentes entre secciones y dentro de cada sección
- Ningún elemento desbordado, cortado ni desalineado
- Las imágenes de producto deben estar centradas verticalmente respecto al texto
- Los separadores entre productos deben ser uniformes
- El email completo debe tener coherencia visual de arriba a abajo
- Antes de finalizar cualquier email, revisar visualmente sección por sección

**Estándar:** si el email no se vería bien en la vidriera de una vinoteca premium, no está listo.

---

### 1.10 Reglas operativas — obligatorias en cada envío

#### Verificación de productos
Antes de incluir cualquier producto en el email:
1. **Verificar que el producto esté disponible para comprar** en el sitio — no incluir productos sin stock ni dados de baja
2. **Verificar que el producto tenga imagen** cargada y visible — no incluir productos sin imagen
3. Si un producto no cumple alguna de estas condiciones, reemplazarlo por otro de la misma categoría y rango de precio

#### Correo de prueba
- **Siempre enviar un correo de prueba a `dayanmartin@gmail.com` antes del envío final**
- El correo de prueba debe ser idéntico al correo final
- No enviar el correo a la lista hasta confirmar que la prueba se ve correcta

#### Configuración de respuesta
- **Reply-to de todos los correos: `ventas@ligier.com.ar`**
- Ningún email debe tener reply-to vacío ni apuntar a otra dirección

#### Horario de envío
- **Todos los correos se envían a las 10:30 AM hora Argentina (GMT-3)**
- Si el envío es programado, verificar que la zona horaria esté configurada correctamente en Mailchimp

---

## PARTE 2 — VOZ Y COPYWRITING

### 2.1 El cliente de Ligier

El destinatario **ya confía en Ligier**. Valora la trayectoria y el criterio de la marca por sobre todo. No necesita ser convencido de por qué el vino es bueno — necesita saber qué eligió Ligier esta vez y por qué vale su atención.

**El email no vende. Informa sobre lo que Ligier seleccionó.**

---

### 2.2 Las 6 reglas del copy Ligier

1. **Habla el curador, no el vendedor** — Ligier informa su selección con autoridad. Nunca implora, nunca urge artificialmente.

2. **Corto y seguro de sí mismo** — Máx 6 palabras por línea en el H1. Máx 3 líneas. Sin exclamaciones. Sin signos de urgencia.

3. **La promo nunca es el titular** — El H1 habla de la selección o de los vinos. La promo 6×5 se menciona en la bajada o en el banner dedicado, nunca en el H1.

4. **Cero superlativos vacíos** — Prohibido: "increíble", "espectacular", "imperdible", "único", "el mejor". Si algo es bueno, se describe. No se califica con adjetivos sin sustancia.

5. **Asumir que el lector sabe** — No explicar qué es un Malbec. Sí especificar región, terruño, carácter. El lector es un conocedor o está en camino de serlo.

6. **El silencio vende más que el ruido** — Una frase que deja algo sin decir invita al click. Menos palabras = más confianza.

---

### 2.3 Fórmula del H1 Hero

```
Estructura: 2–3 líneas de 3–6 palabras cada una
Tono: curador con autoridad, no vendedor con urgencia
Nunca empieza con: NO / ¿ / ¡
Nunca menciona: precio, promo, descuento
Puede mencionar: la selección, el origen, el criterio de curaduría, el momento
```

**Ejemplos aprobados:**
- "Esta semana, / elegimos seis."
- "Difícil / quedarse / con uno solo."
- "Los que / guardamos / para vos."
- "Seis etiquetas / que conocemos / de memoria."

**Ejemplos rechazados:**
- "Vinos que dicen algo distinto en cada copa." ❌ (muy largo, muy lírico)
- "Seis vinos de bodega icónica. Pagás cinco." ❌ (precio en el titular)
- "No todos los vinos cuentan algo distinto." ❌ (empieza con NO)

---

### 2.4 Fórmula de la bajada Hero

```
Máx 2 líneas
Línea 1: contexto de la selección (orígenes, bodegas, carácter)
Línea 2: la promo, si aplica — mencionada sin exclamación
```

**Ejemplo:**
> Altamira, Valle de Uco, Cafayate.
> Etiquetas que conocemos y respaldamos. Llevá 6, pagá 5.

---

### 2.5 Descripciones de productos

- Máx 2 líneas
- Describir el carácter organoléptico con precisión: fruta, estructura, final
- No usar "es un vino" ni "se trata de" — ir directo al carácter
- No usar superlativos

**Ejemplo correcto:**
> Suelo calcáreo de altura. Concentración y profundidad tánica que solo Altamira puede dar.

**Ejemplo incorrecto:**
> Es un increíble vino de altura con notas frutales. Muy recomendado.

---

## PARTE 3 — TIPOS DE EMAIL

### REGLA CRÍTICA — Categorías y promoción 6x5

**La promo 6x5 NO existe en todas las categorías.** Aplicar incorrectamente esta promo es un error grave.

| Tipo de email | URL a navegar | Promo 6x5 |
|---------------|--------------|-----------|
| Vinos | https://vinotecaligier.com/vino | ✅ SÍ aplica |
| Whisky | https://vinotecaligier.com/whisky | ✅ SÍ aplica |
| Espirituosas | https://vinotecaligier.com/espirituosas | ✅ SÍ aplica |
| Vinos Guardados | https://vinotecaligier.com/vinos-guardados | ❌ NO aplica |
| Wine Club | https://vinotecaligier.com/contenido-wineclub | ❌ NO aplica |
| Experiencias | https://vinotecaligier.com/contenido-experiencias | ❌ NO aplica |
| Gift Cards | https://vinotecaligier.com/gift-card-ligier.html | ❌ NO aplica |

**Regla de navegación:** Para seleccionar productos, navegar ÚNICAMENTE la URL correspondiente al tipo de email. Nunca mezclar productos de categorías distintas en un mismo email.

---

### 3.1 Emails de vinos

**Rangos de precio:**
- Entrada: $20.000–$30.000
- Medio-bajo: $30.000–$40.000
- Medio: $40.000–$60.000
- Medio-alto: $60.000–$90.000
- Alto: $90.000–$120.000
- Premium: +$120.000

**Criterios de agrupación (se puede combinar):**
- Por cepa: Malbec, Cabernet Franc, Carmenere, Blend, Torrontés, etc.
- Por tipo: tintos, blancos, rosados, espumantes
- Por zona: Valle de Uco, Luján de Cuyo, Paraje Altamira, etc.
- Por provincia: Mendoza, San Juan, Salta, Neuquén
- Por país: Argentina, Chile, España, Italia, Francia

**Regla:** Cuando se hace una selección temática, el Eyebrow y la bajada del Hero deben reflejar ese criterio. Si son todos de Altamira, el Hero lo dice. Si son todos +$60.000, el Hero alude a esa categoría sin mencionar el precio explícitamente.

---

### 3.2 Emails de Whisky

- Misma estructura que vinos
- Rango mínimo de precio: $40.000–$60.000
- Criterios: Single Malt / Blend / Bourbon / Japonés / Irlandés / Escocés · por destilería · por región
- El accesorio sugerido debe ser afín: vasos Glencairn, old fashioned, set de whisky

---

### 3.3 Emails de Espirituosas / Bebidas de alta graduación

- URL categoría: `https://vinotecaligier.com/espirituosas`
- Misma estructura base
- Rango mínimo: $40.000–$60.000
- Contenido adicional: puede incluir sugerencias de cócteles con receta
- Concepto posible: "Armá tu barra" — selección para armar una barra completa en casa
- El accesorio sugerido debe ser herramientas de coctelería o cristalería apropiada

---

### 3.4 Emails de Wine Club

- URL: `https://vinotecaligier.com/contenido-wineclub`
- Objetivo principal: **convertir suscriptores**
- El Hero debe transmitir exclusividad y pertenencia, no urgencia
- Comunicar los beneficios del club con claridad
- No aplica la estructura de 6 productos — tiene estructura propia a definir
- Tono: club selecto, comunidad de conocedores, acceso preferencial

---

### 3.5 Emails de Experiencias

- URL: `https://vinotecaligier.com/contenido-experiencias`
- Uno de los rubros de mayor valor para Ligier
- Tono: experiencia única, curada, irrepetible
- No aplica estructura de productos estándar — estructura propia a definir
- La comunicación debe transmitir calidad y exclusividad en cada línea

---

### 3.6 Emails de Vinos Guardados

- URL: `https://vinotecaligier.com/vinos-guardados`
- **El segmento más selectivo y de mayor valor agregado de Ligier**
- La comunicación debe emanar calidad y excelencia en cada elemento: copy, diseño, selección
- Tono: máxima autoridad, máxima sobriedad — el precio no es el argumento, el origen y la rareza sí lo son
- No usar la promo 6×5 en estos emails — son productos de valor individual
- El accesorio debe ser de igual nivel de sofisticación

---

### 3.7 Emails de Gift Cards

- URL: `https://vinotecaligier.com/gift-card-ligier.html`
- Dos audiencias:
  - **Corporativa:** empresas que regalan a clientes o empleados — tono profesional, beneficios del regalo
  - **Personal:** clientes que quieren regalar — tono cálido, el regalo como gesto
- Estructura propia a definir según la ocasión

---

## PARTE 4 — CHECKLIST DE VALIDACIÓN

Antes de aprobar cualquier email generado, verificar:

### Diseño
- [ ] Logo en 140px
- [ ] 9 secciones presentes en el orden correcto
- [ ] 6 productos en la sección de vinos
- [ ] Botón pack presente y con link de carrito
- [ ] 1 accesorio afín en sección crema
- [ ] 10 categorías completas en sección negra
- [ ] Íconos reales de WhatsApp e Instagram
- [ ] Ambas cuentas de Instagram (@ligier y @vinosguardados)
- [ ] Sin border-radius en ningún elemento
- [ ] Sin sombras ni gradientes
- [ ] Solo Arial como fuente

### Copy
- [ ] H1 de máx 3 líneas, máx 6 palabras por línea
- [ ] H1 no menciona precio ni promo
- [ ] H1 no empieza con NO, ¡ ni ¿
- [ ] Sin superlativos vacíos
- [ ] Promo mencionada en bajada o banner, no en H1
- [ ] Descripciones de productos en máx 2 líneas

### Técnico
- [ ] Link de carrito compartido presente en botón pack
- [ ] Todos los links de productos correctos
- [ ] `*|UNSUB|*` en footer
- [ ] Responsive para mobile
