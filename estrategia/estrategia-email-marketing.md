# Estrategia de Email Marketing — Vinoteca Ligier
**CRM Lifecycle · Retención · Deliverability (óptica de negocio)**
*Versión 1.0 — Junio 2026. Documento accionable. Voz de marca según `guidelines/ligier-email-guidelines.md`.*

---

## 0. Diagnóstico de partida (lo que hoy existe)

| Hoy | Problema de negocio |
|-----|---------------------|
| Subject fijo: `Nueva selección {mes} — Ligier` para TODA campaña | El subject no refleja el contenido (vinos, whisky, guardados rinden igual de invisibles). Mata apertura y mata la lectura de qué temática funciona. |
| Sin preheader | Mailchimp rellena el preview con el alt del logo o "View in browser". Se desperdicia el segundo activo más visible del inbox. |
| Solo campañas "regular" (batch & blast) | Cero automatización. No hay carrito abandonado, bienvenida, post-compra ni win-back. El 100% de la facturación por email depende de envíos manuales. |
| Audiencia única, sin segmentos | Mismo email al cliente nuevo, al de wine club y al dormido hace 8 meses. Riesgo de fatiga y de daño a deliverability. |
| `analyze.js` lee solo open/click/revenue agregado | No mide por segmento, no compara contra control, no detecta dormidos ni mide deliverability (bounce/unsub/spam). |

La buena noticia: el stack ya resuelve lo difícil. Hay **API de Magento por SKU y `url_key`**, **carritos compartidos** (`compartircarrito`), **biblioteca de copy con voz validada** y **conexión Mailchimp**. Falta orquestar lifecycle y subjects.

---

## 1. Líneas de asunto y preheader

### 1.1 Principios (derivados de la guía de voz)
- **El subject informa, no vende.** Sin superlativos, sin exclamaciones, sin `¡`/`¿`.
- **El preheader complementa, nunca repite el subject.** Es la "bajada" del inbox.
- **Promo nunca en el subject principal de la versión A.** El 6x5 va en el preheader o en la variante B.
- **Sin emojis.**

### 1.2 Criterios de longitud
| Campo | Objetivo | Límite duro | Por qué |
|-------|----------|-------------|---------|
| Subject | 28–42 caracteres | 50 | Mobile corta ~40 char. Lo decisivo va al principio. |
| Preheader | 40–90 caracteres | 100 | Apple/Gmail muestran ~90. Cargarlo SIEMPRE explícito. |
| Front-load | Primeras 25 char | — | "Malbecs de Altamira" antes que "Selección de…". |

### 1.3 Sistema de subjects + preheaders por tipo

**VINOS (con 6x5)**
| Subject (A) | Preheader |
|-------------|-----------|
| `Seis tintos para esta semana` | `Elegimos uno por uno. Llevá 6, pagá 5.` |
| `Malbecs de Altamira y Gualtallary` | `Nuestra selección de junio. Podés mezclar etiquetas.` |
| `La selección de vinos de junio` | `Seis etiquetas que conocemos de memoria. Llevá 6, pagá 5.` |

**WHISKY**
| Subject | Preheader |
|---------|-----------|
| `Single malts de Escocia y Japón` | `Destilados con procedencia. Elegidos uno por uno.` |
| `Whisky para tomar sin apuro` | `Años de añejamiento en cada botella.` |

**ESPIRITUOSAS**
| Subject | Preheader |
|---------|-----------|
| `Para armar tu barra en serio` | `Gin, ron y destilados de autor. Con qué empezar.` |
| `Lo que le falta a tu barra` | `Botellas con carácter para mezclar o tomar solas.` |

**VINOS GUARDADOS**
| Subject | Preheader |
|---------|-----------|
| `Cosechas que ya no se consiguen` | `Botellas que el tiempo hizo irrepetibles.` |
| `Vinos guardados por años` | `Lo que quedó de esas añadas. Hasta 6 cuotas sin interés.` |

**WINE CLUB**
| Subject | Preheader |
|---------|-----------|
| `El club que curó la cava` | `Cada mes, vinos que no encontrás. Cuatro membresías.` |
| `Vinos elegidos para vos, cada mes` | `Acceso a lo que aún no salió a la venta.` |

**EXPERIENCIAS**
| Subject | Preheader |
|---------|-----------|
| `Una velada curada por Ligier` | `Maridajes, fecha y lugar. Cupos limitados.` |

**GIFT CARDS**
| Subject | Preheader |
|---------|-----------|
| `El regalo para quien sabe elegir` | `La elección queda en sus manos.` |

> **Estacional** (Navidad, Día del Padre, Día del Amigo): anclar la ocasión en el subject (`Para la mesa de las Fiestas`) manteniendo voz curadora. Nunca "¡Ofertón navideño!".

### 1.4 A/B testing de subject
- **Tamaño:** mínimo ~1.000 destinatarios por variante. Si el segmento es menor, NO testear.
- **Una variable por vez:** o subject, o preheader, o from-name.
- **Métrica ganadora:** newsletters de catálogo → **click rate** (no open, inflado por Apple MPP). Flujos transaccionales → **revenue/conversión**.
- **Ventana:** 4 h de test → envío automático del ganador.
- **Roadmap de hipótesis:** (1) categoría concreta vs. genérico, (2) promo en preheader vs. sin promo, (3) región/cepa vs. beneficio, (4) from-name.

> **Cambio en `generate-campaign.js`:** el subject está hardcodeado. Parametrizar `subject` y agregar `preview_text` dentro de `settings`. Agregar `SUBJECTS`/`PREHEADERS` por tipo en `copy-library.js`, igual que `TITULOS`/`BAJADAS`, y un paso "Asunto" en el wizard.

---

## 2. Carrito abandonado (Abandoned Cart)

Flujo de mayor ROI en e-commerce, hoy inexistente. En Mailchimp: **Customer Journey → trigger "Abandoned cart"** (requiere conexión de tienda) o, dado que el sitio es **Magento**, vía e-commerce connector / API que postee carritos a Mailchimp.

### 2.1 Requisito de datos (Magento → Mailchimp)
Por carrito: `email`, líneas (`sku`, nombre, precio, qty, url, imagen), `cart_total`, `cart_url` (idealmente el link de carrito compartido que ya genera la app), `timestamp`.
El parser `parseMagentoProduct` ya devuelve nombre/precio/imagen/url/stock. Falta el **puente de evento de carrito** (Mailchimp e-commerce API: `POST /ecommerce/stores/{id}/carts`).

### 2.2 El flujo: 3 toques, sin quemar margen
| # | Timing | Objetivo | Incentivo |
|---|--------|----------|-----------|
| 1 | **1 h** | Recordatorio / fricción técnica | **NINGUNO** |
| 2 | **24 h** | Reforzar curaduría + reducir riesgo percibido | **NINGUNO** |
| 3 | **72 h** | Último toque | **Incentivo condicional** |

**Por qué:** el 80% de la recuperación se logra sin descuento. Quemar margen en el toque 1 entrena a la lista a abandonar a propósito.

Copy completo en `automatizaciones/` (templates HTML) y `automatizaciones/guia-automatizaciones-mailchimp.md`.

### 2.3 Reglas operativas
- **Exit por compra** (nativo en el trigger de e-commerce).
- **Frequency cap:** carrito tiene prioridad sobre el masivo; pausar batch para quien está en flujo activo.
- **Solo carritos identificados** (con email).
- **Supresión por stock 0** (usar `inStock` del parser).
- **Incentivo del toque 3:** para vinos NO es un descuento nuevo, es **recordar el 6x5 que ya existe** y empujar a completar el pack (margen intacto). Para whisky/espirituosas/guardados: envío sin cargo o 3 cuotas antes que %.

---

## 3. Encuesta post-compra / post-entrega

Objetivo doble: **reseñas/NPS** (prueba social + engagement) y **datos para recompra**.

### 3.1 Requisito de datos
Trigger ideal: **entrega confirmada**, no "compra". Evento `order.delivered` (o aproximar con compra + SLA de envío). Datos: `email`, `order_id`, líneas compradas, fecha de entrega.

### 3.2 El flujo: 2 toques
| # | Timing desde entrega | Objetivo |
|---|----------------------|----------|
| 1 | **+3 días** | NPS de 1 pregunta + invitación a reseñar |
| 2 | **+10 días** *(solo si NPS alto y/o sin reseña)* | Empujar reseña + sembrar recompra |

### 3.3 Branching por NPS (Customer Journey)
- **9–10 (promotores):** pedir reseña pública → tag `promoter`.
- **7–8 (pasivos):** "¿Algo que mejorar?" → reply abierto.
- **0–6 (detractores):** NO mandar a reseña pública → "queremos entender qué pasó" → reply directo / WhatsApp. Recuperación 1-a-1.

### 3.4 Cómo conecta con el negocio
Reseñas → prueba social en el sitio y en newsletters. NPS → KPI trimestral de retención. Promotores → candidatos a Wine Club y referidos. "Volver a pedir" → primera piedra del flujo de reposición.

---

## 4. Segmentación y lifecycle

### 4.1 Segmentos (sobre la audiencia única, vía tags + merge fields)
| Segmento | Definición | Tag |
|----------|------------|-----|
| Nuevos / no compradores | Suscripto, 0 órdenes | `lead` |
| Primera compra | 1 orden | `first-order` |
| Recurrentes | 2+ órdenes | `recurrente` |
| Alto ticket | AOV o CLV top 20% | `high-value` |
| Wine Club | Membresía activa | `wineclub` + nivel |
| Dormidos | Sin compra ni click 90–180 d | `dormido` |
| Churned / win-back | Sin actividad 180+ d | `winback` |
| Promotores | NPS 9–10 | `promoter` |

### 4.2 Automatizaciones por segmento
- **Bienvenida (alta a la lista) — 3 emails:** quiénes somos/cómo curamos → cómo funciona el 6x5 → Wine Club y experiencias. Incentivo opcional: envío gratis 1ª compra antes que %.
- **Win-back (dormido 90 d) — 2–3 emails:** novedades sin descuento → top del trimestre → incentivo real (envío/cuotas); si no reacciona → **sunset**.
- **Reposición (compra + ventana 30–45 d):** "¿se terminó? volvé a pedir lo mismo" + 3 afines. No aplica a wine club (envío recurrente).
- **Cumpleaños / aniversario:** botella sugerida / curaduría retrospectiva.
- **Alto ticket / Wine Club:** menor frecuencia comercial, más curaduría, acceso anticipado.

---

## 5. Calendario de campañas

Cadencia base: **2 campañas masivas/semana** (martes + jueves). Tercera (sábado) solo en temporada alta. Más de 3/semana quema engagement.

| Día | Tipo | Racional |
|-----|------|----------|
| Lunes | — | Inbox saturado, bajo engagement. |
| **Martes** | Vinos (6x5) | Mayor apertura B2C + promo ancla. |
| Miércoles | Rotativo: Whisky / Espirituosas / Guardados | Diversifica catálogo. |
| **Jueves** | Vinos o Wine Club / Experiencias | Pre-fin de semana. |
| Viernes | — salvo estacional | Cae el engagement comercial. |
| Sábado | Solo temporada alta | Compra de regalo/impulso. |

**Cap por contacto:** máx 3 emails comerciales/semana (masivos + flujos). Transaccionales (carrito, post-compra) NO cuentan. Validar la grilla con `analyze.js` (`mejorDia`/`mejorHora`) cuando haya datos reales.

---

## 6. KPIs y medición

### 6.1 Métricas por flujo
| Flujo | Primaria | Secundarias |
|-------|----------|-------------|
| Newsletter | Click rate, revenue/email | CTOR, conversión, unsub |
| Carrito abandonado | Tasa de recuperación | Revenue recuperado, conv. por toque |
| Post-compra | Tasa de reseña, NPS | Respuesta, recompra atribuida |
| Bienvenida | % 1ª compra en 14 d | Open/click email 1 |
| Win-back | Reactivation rate | % a sunset |
| Reposición | Repeat purchase rate | CTR "Volver a pedir" |

### 6.2 Benchmarks (vino/retail premium, AR — ajustar con datos propios a 60 d)
| Métrica | Rango |
|---------|-------|
| Open rate (con MPP) | 30–45% |
| Click rate (newsletter) | 2–4% |
| CTOR | 8–14% |
| Recuperación carrito | 8–15% |
| Unsubscribe | < 0,3% (alerta > 0,5%) |
| Bounce | < 1% |
| Spam complaint | < 0,08% (límite Gmail/Yahoo 0,3%) |
| Reseña post-compra | 5–15% |

### 6.3 Qué agregar a `analyze.js`
1. **Deliverability:** `bounce_rate`, `unsubscribe_rate`, `abuse_rate` (ya vienen en el report, hoy se descartan).
2. **CTOR** = unique_clicks / unique_opens.
3. **Revenue por email** = revenue / emails_sent.
4. **Subject/preheader como dimensión** (cerrar el loop del A/B).
5. **Performance de flujos** (`/automations`, `/customer-journeys`, no solo `?status=sent`).
6. **Detección de dormidos** (since_last_open) → segmentos win-back/sunset.
7. **Tendencia temporal** (período vs. período).
8. **Significancia mínima** (≥3 campañas por grupo antes de afirmar un insight; hoy con ≥2 ya afirma).

### 6.4 Deliverability
- **Sunset policy:** sin engagement en 6 meses pese a win-back → suprimir de masivos.
- **Doble verificación de stock antes de enviar.**
- **Autenticación SPF/DKIM/DMARC** del dominio (requisito Gmail/Yahoo 2024+).

---

## 7. Quick wins priorizados (top 5)

| # | Acción | Esfuerzo | Impacto |
|---|--------|----------|---------|
| 1 | **Subject dinámico + preheader por tipo** (parametrizar en `generate-campaign.js` + `copy-library.js`). | Bajo | Alto |
| 2 | **Carrito abandonado (3 toques, sin descuento inicial).** | Medio | Muy alto |
| 3 | **Flujo de bienvenida (3 emails).** | Bajo-Medio | Alto |
| 4 | **Encuesta post-compra con NPS branching.** | Medio | Medio-Alto |
| 5 | **Upgrade `analyze.js`: deliverability + CTOR + revenue/email.** | Bajo | Medio |

**Secuencia:** Sem 1–2 → #1 y #5. Sem 3–5 → #3. Sem 6–10 → #2. En paralelo cuando haya evento de entrega → #4.

---
*Toda la copy respeta la guía de voz Ligier: tono curador, sin superlativos, sin exclamaciones, promo en bajada/preheader y nunca en el H1 ni en el subject principal.*
