# Mailchimp Automation — Ligier

Repositorio de automatización de emails para [Vinoteca Ligier](https://vinotecaligier.com).

---

## Estructura

```
mailchimp/
├── guidelines/
│   └── ligier-email-guidelines.md   # Documento maestro de diseño, copy y reglas operativas
├── templates/
│   └── vinos-v1.html                # Template base para emails de vinos (con 6x5)
├── prompts/
│   └── instrucciones-claude.md      # Prompt para Claude — generación automática de emails
└── README.md
```

---

## Documento maestro

Antes de generar o modificar cualquier email, leer:
**`guidelines/ligier-email-guidelines.md`**

Contiene:
- Sistema de diseño completo (colores, tipografía, botones, secciones)
- Reglas de responsividad y calidad
- Voz y copywriting de la marca
- Tipos de email y sus particularidades
- Reglas operativas (prueba, reply-to, horario de envío)
- Checklist de validación

---

## Reglas operativas rápidas

| Parámetro | Valor |
|-----------|-------|
| Correo de prueba | dayanmartin@gmail.com |
| Reply-to | ventas@ligier.com.ar |
| Hora de envío | 10:30 AM (GMT-3, Argentina) |
| Productos por email | 6 vinos + 1 accesorio |
| Logo | 140px |

---

## Templates disponibles

| Archivo | Tipo | Estado |
|---------|------|--------|
| `templates/vinos-v1.html` | Vinos con promo 6×5 | ✅ Listo |
| `templates/whisky.html` | Whisky | 🔜 Próximamente |
| `templates/espirituosas.html` | Espirituosas | 🔜 Próximamente |
| `templates/wine-club.html` | Wine Club | 🔜 Próximamente |
| `templates/experiencias.html` | Experiencias | 🔜 Próximamente |
| `templates/vinos-guardados.html` | Vinos Guardados | 🔜 Próximamente |
| `templates/gift-cards.html` | Gift Cards | 🔜 Próximamente |
