# Auditoría de Plantillas — Vinoteca Ligier
*Diseño y desarrollo de HTML email · render, deliverability técnica, dark mode, accesibilidad.*
Fecha: 2026-06-02. Alcance: 5 plantillas en `templates/` + app de inyección `ligier-app/api/generate-campaign.js`.

> **Estado:** los hallazgos CRÍTICOS (C1–C5) y los ALTOS de mayor impacto (A1 preheader, A2 dark mode, A6 pills) ya fueron **aplicados** a las plantillas vivas. Los ítems de Outlook/MSO/botones bulletproof (A3, A4, M3) quedan como backlog v3.1 documentado abajo.

---

## CRÍTICO (aplicados ✅)

### C1 — Whisky/Espirituosas: faltaba `class="hero-bajada"` → la bajada del hero nunca se inyectaba
`base-email-whisky.html`. El regex de la app busca `class="hero-bajada"`. Sin la clase, salía siempre el texto fijo, que además mencionaba "Llevá 6, pagá 5" (promo prohibida fuera de Vinos). **Fix aplicado:** clase agregada + quitado el "Llevá 6, pagá 5" del fallback.

### C2 — Whisky y Guardados: faltaban marcadores `<!-- ACC_START -->` / `<!-- ACC_END -->` → el accesorio nunca se reemplazaba ni se eliminaba
`base-email-whisky.html`, `base-email-guardados.html`. La app reemplaza/elimina la sección de accesorio entre esos marcadores. Sin ellos, salía siempre el accesorio fijo (una copa de **vino** en whisky, inconsistente). **Fix aplicado:** marcadores envolviendo la sección, igual que en vinos.

### C3 — Vinos: faltaba `class="pack-total"` → el total real del 6×5 nunca se inyectaba
`base-email-vinos.html`. El `<p>` del pack decía solo "pagás 5, llevás 6"; el regex no encontraba nada y el total calculado se descartaba. **Fix aplicado:** bloque de pack con `<p class="pack-total">` + label "Total 6×5".

### C4 — Guardados: el regex del eyebrow `color:#666` pisaba "EXCLUSIVO LIGIER" del Wine Club
`base-email-guardados.html`. `injectIntoTemplate` corre el reemplazo de `color:#666` sobre el **primer** match, que en guardados era la etiqueta "EXCLUSIVO LIGIER". **Fix aplicado:** cambiado ese eyebrow a `color:#777` para no colisionar (el hero real usa `rgba(255,255,255,0.5)`).

### C5 — `vinos-miercoles-28mayo.html`: cart link sin padding base64 válido
Snapshot legacy. **Resuelto archivando** la plantilla (ver A5/M1).

---

## ALTO

### A1 — Preheader / preview text oculto (aplicado ✅ en las 5 vivas)
Ninguna plantilla tenía preheader → el preview lo armaba Mailchimp con el alt del logo. **Fix aplicado:** `<div class="preheader">` oculto justo después de `<body>`, con caracteres de relleno para que Gmail no arrastre texto del cuerpo. Texto por defecto por tipo; se puede hacer inyectable desde la app (reemplazo análogo al de la bajada).

### A2 — Dark mode (aplicado ✅)
Sin `color-scheme` el cliente auto-oscurece `#fff`/`#111` y el logo/íconos PNG negros transparentes pueden desaparecer. **Fix aplicado:** `<meta name="color-scheme" content="light only">` + `supported-color-schemes` + `:root { color-scheme: light only; }`. **Pendiente de assets:** servir logo e íconos sobre fondo blanco sólido (no transparente) para blindar Apple Mail/Gmail dark.

### A3 — Outlook ignora `padding` en `<a>` → botones sin caja (BACKLOG v3.1)
Todos los CTA usan `<a style="...padding...">`. Outlook desktop los renderiza como texto sin altura. **Fix recomendado:** envolver cada botón en `<table><td bgcolor style="padding">`. No aplicado aún por ser un cambio transversal que también toca los botones que genera la app; se prioriza por share de Outlook desktop en la audiencia (bajo en B2C AR). Patrón bulletproof documentado en `guidelines`.

### A4 — Scaffolding MSO ausente (BACKLOG v3.1)
Falta `xmlns:v/o`, bloque `<!--[if mso]><o:OfficeDocumentSettings>`, `mso-line-height-rule:exactly`. Recomendado para fijar el render en Outlook.

### A5 — `vinos-v1.html` viola reglas duras (archivado ✅)
Íconos SVG/CDN externo (Mailchimp los bloquea), `border-radius` prohibido, Instagram con gradiente, logo en footer, placeholders propios incompatibles con la app. **Movido a `archive/`.**

### A6 — Pills sin `white-space:nowrap` (aplicado ✅)
Violaba guideline §225 (el texto se rompe letra por letra en mobile). **Fix aplicado:** `white-space:nowrap` en los pills de las plantillas vivas.

---

## MEDIO

### M1 — `vinos-miercoles-28mayo.html` es un snapshot, no una base (archivado ✅)
Productos hardcodeados, sin `hero-bajada`/`pack-total`/ACC markers. **Movido a `archive/`.** Sirvió de referencia visual para el fix C3.

### M3 — Hero de Guardados con `background-image` en `<div>` + margins negativos no renderiza en Outlook (BACKLOG)
Fallback `#1a1a1a` plano es aceptable. Recomendado: VML `<v:image>` o simplificar overlay. No bloqueante.

### M4 — Tablas de layout sin `role="presentation"` (BACKLOG menor)
Accesibilidad: lectores de pantalla las anuncian como tablas de datos.

### M5 — Tap targets de pills < 44px en mobile (BACKLOG menor)
Subir padding vertical en la media query mobile.

---

## BAJO
- **B2 — Peso HTML:** todas < 35KB, muy por debajo del clip de Gmail (~102KB). Sin acción.
- **B3 — `<title>` de vinos hardcodeado** a campaña vieja. No afecta render (Mailchimp gestiona el subject). Menor.

---

## Plantillas vivas tras la limpieza
- `base-email-vinos.html` — vinos (6×5), también base de wine-club/experiencias/gift-cards según la app.
- `base-email-whisky.html` — whisky y espirituosas.
- `base-email-guardados.html` — vinos guardados.

Las legacy `vinos-v1.html` y `vinos-miercoles-28mayo.html` salieron del pipeline (`archive/`).

---

## Backlog v3.1 (no bloqueante, mejora incremental de render Outlook/accesibilidad)
1. Botones bulletproof (padding en `<td>`, no en `<a>`).
2. Scaffolding MSO (`xmlns`, OfficeDocumentSettings, `mso-line-height-rule`).
3. VML para el fondo del hero de Guardados.
4. `role="presentation"` en todas las tablas de layout.
5. Tap targets de pills ≥ 44px en mobile.
6. Assets de logo/íconos sobre fondo blanco sólido para dark mode.
