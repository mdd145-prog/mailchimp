# Mailchimp Automation — Ligier

Repositorio de automatización de emails para [Vinoteca Ligier](https://vinotecaligier.com).
La app que genera y programa las campañas vive en [`ligier-app`](https://github.com/mdd145-prog/ligier-app) y consume estas plantillas vía GitHub raw.

---

## Estructura

```
mailchimp/
├── guidelines/
│   └── ligier-email-guidelines.md      # Documento maestro de diseño, copy y reglas (v4.0)
├── templates/                          # Plantillas VIVAS (las que usa la app)
│   ├── base-email-vinos.html           # Vinos con 6×5 (plantillas propias para otros tipos: Fase 2)
│   ├── base-email-whisky.html          # Whisky y espirituosas
│   └── base-email-guardados.html       # Vinos Guardados + Wine Club
├── campanas/                           # Campañas puntuales armadas a mano
│   └── 2026-08-ligier-experience-8.html  # Evento Experience #8 (base de la futura plantilla experiencias)
├── landing/
│   └── ligier-experience-8.html        # Landing del evento — referencia de identidad web (serif de display)
├── automatizaciones/                   # Flujos de Customer Journeys (Mailchimp)
│   ├── carrito-abandonado/             # 3 toques: 1h · 24h · 72h
│   ├── post-compra/                    # NPS + reseña + recompra
│   └── guia-automatizaciones-mailchimp.md
├── estrategia/
│   ├── replanteo-arquitectura-v4.md    # ⭐ Decisiones v4, contrato de inyección y plan de 5 fases
│   ├── estrategia-email-marketing.md   # Subjects/preheaders, lifecycle, calendario, KPIs
│   └── auditoria-diseno-plantillas.md  # Auditoría técnica de HTML email + backlog
├── archive/                            # Plantillas legacy (no usar)
├── prompts/
│   ├── instrucciones-claude.md
│   └── prompt-generar-email.md
└── README.md
```

---

## Documento maestro

Antes de generar o modificar cualquier email, leer:
**`guidelines/ligier-email-guidelines.md`** (v4.0)

Contiene el sistema de diseño, reglas de responsividad/calidad, voz y copy, tipos de email, técnico obligatorio (preheader, dark mode) y la **API DE INYECCIÓN** (contrato de marcadores `INJECT:*` con la app).

> **Replanteo v4 — estado:** Fase 1 completada (contrato `INJECT:*` en plantillas + ligier-app
> desplegada con 6×5 por botellas y total real del carrito). **Próximo paso: Fase 2** — plantillas
> propias para experiencias / wine-club / gift-cards / regalos + rama sin productos en la app.
> Decisiones y plan completo: `estrategia/replanteo-arquitectura-v4.md`.

---

## Plantillas vivas

| Archivo | Tipo | Estado |
|---------|------|--------|
| `templates/base-email-vinos.html` | Vinos (promo 6×5) | ✅ Listo |
| `templates/base-email-whisky.html` | Whisky · Espirituosas | ✅ Listo |
| `templates/base-email-guardados.html` | Vinos Guardados · Wine Club | ✅ Listo |

> Las plantillas `vinos-v1.html` y `vinos-miercoles-28mayo.html` están en `archive/` — son legacy y no deben usarse (violan reglas duras o son snapshots, no bases).

---

## Automatizaciones (Customer Journeys)

| Flujo | Carpeta | Estado |
|-------|---------|--------|
| Carrito abandonado (1h · 24h · 72h) | `automatizaciones/carrito-abandonado/` | ✅ Plantillas listas |
| Encuesta post-compra (NPS + reseña + recompra) | `automatizaciones/post-compra/` | ✅ Plantillas listas |
| Bienvenida · Win-back | `automatizaciones/guia-automatizaciones-mailchimp.md` | 🔜 A montar |

Cómo ponerlas en producción: **`automatizaciones/guia-automatizaciones-mailchimp.md`**.

---

## Reglas operativas rápidas

| Parámetro | Valor |
|-----------|-------|
| Correo de prueba | dayanmartin@gmail.com |
| Reply-to | ventas@ligier.com.ar |
| Hora de envío | 10:30 AM (GMT-3, Argentina) |
| Logo | 140px (solo header) |

---

## Cambios recientes (v3.1 — junio 2026)

Auditoría supervisada por un especialista en email marketing y uno en diseño de HTML email. Resumen en `estrategia/`.

**Fixes críticos de integración con la app** (la inyección de contenido fallaba en silencio):
- Vinos: agregado `class="pack-total"` → ahora se inyecta el total real del 6×5.
- Whisky/Espirituosas: agregado `class="hero-bajada"` y marcadores `ACC_START/ACC_END` → la bajada y el accesorio ahora se inyectan; quitada la promo 6×5 del fallback (no corresponde fuera de vinos).
- Guardados: marcadores de accesorio + resuelta la colisión del eyebrow `#666` que pisaba el bloque "EXCLUSIVO LIGIER" del Wine Club.

**Mejoras de deliverability/diseño en las 3 plantillas vivas:**
- Preheader oculto (texto de preview) en todas.
- Meta de dark mode (`color-scheme: light only`).
- `white-space:nowrap` en los pills de categorías (no se rompen en mobile).

Todos los fixes verificados con los regex reales de `ligier-app/api/generate-campaign.js`.
