# Prompt — Generar email Ligier
> Copiá y completá las variables antes de pegarlo en Claude Code.
> Siempre correr desde la carpeta `mailchimp/` con `git pull` previo.

---

## ⚠️ ANTES DE USAR ESTE PROMPT

1. `git pull origin main` para tener el repo actualizado
2. Claude Code SIEMPRE parte del template `templates/base-email-vinos.html`
3. Nunca genera HTML desde cero — copia la estructura y reemplaza el contenido

---

## PROMPT BASE

```
Leé los archivos guidelines/ligier-email-guidelines.md y prompts/instrucciones-claude.md completos antes de hacer cualquier cosa. Confirmame que los leíste y resumí las reglas críticas.

Luego leé también el template de referencia: templates/base-email-vinos.html — esta es la base que tenés que usar. Copiá toda la estructura HTML y CSS, y reemplazá solo el contenido variable (productos, precios, hero copy, links).

Generá un email con estos datos:

TIPO: [vinos / whisky / espirituosas / wine-club / experiencias / vinos-guardados / gift-cards]
CRITERIO: [por cepa / por zona / por rango de precio / por provincia / por país]
RANGO DE PRECIO: [20-30k / 30-40k / 40-60k / 60-90k / 90-120k / +120k]
MES Y AÑO: [ej: Mayo 2026]

PRODUCTOS: [dejá vacío para que Claude navegue el sitio, o pegá las URLs o el link del carrito]

Navegá https://vinotecaligier.com/[categoría] para seleccionar los 6 productos.
Verificá stock e imagen de cada uno antes de incluirlo.
Navegá https://vinotecaligier.com/cristaleria y https://vinotecaligier.com/accesorios para elegir el accesorio afín.
Generá el link de carrito compartido con los 6 SKUs.
Navegá el link del carrito para obtener el total real 6x5.

Guardá el resultado en templates/[nombre-descriptivo].html
```

---

## EJEMPLOS DE USO

### Modo automático — Claude elige los productos
```
Leé los archivos guidelines/ligier-email-guidelines.md y prompts/instrucciones-claude.md completos antes de hacer cualquier cosa. Confirmame que los leíste y resumí las reglas críticas.

Luego leé también el template de referencia: templates/base-email-vinos.html — esta es la base que tenés que usar. Copiá toda la estructura HTML y CSS, y reemplazá solo el contenido variable (productos, precios, hero copy, links).

Generá un email con estos datos:

TIPO: vinos
CRITERIO: Malbecs de Mendoza
RANGO DE PRECIO: 40-60k
MES Y AÑO: Mayo 2026

Navegá https://vinotecaligier.com/vino para seleccionar los 6 productos.
Verificá stock e imagen de cada uno antes de incluirlo.
Navegá https://vinotecaligier.com/cristaleria para elegir el accesorio afín a tintos.
Generá el link de carrito compartido con los 6 SKUs.
Navegá el link del carrito para obtener el total real 6x5.

Guardá el resultado en templates/vinos-malbec-mayo2026.html
```

### Modo manual — vos traés el carrito
```
Leé los archivos guidelines/ligier-email-guidelines.md y prompts/instrucciones-claude.md completos antes de hacer cualquier cosa. Confirmame que los leíste y resumí las reglas críticas.

Luego leé también el template de referencia: templates/base-email-vinos.html — esta es la base que tenés que usar. Copiá toda la estructura HTML y CSS, y reemplazá solo el contenido variable (productos, precios, hero copy, links).

Generá un email con estos datos:

TIPO: vinos
CRITERIO: selección curada
RANGO DE PRECIO: 40-70k
MES Y AÑO: Mayo 2026

PRODUCTOS (link de carrito): https://vinotecaligier.com/compartircarrito/index/share/data/[BASE64]/

Decodificá el BASE64 para obtener los SKUs.
Visitá cada producto para verificar stock, imagen, precio y descripción.
Navegá https://vinotecaligier.com/cristaleria para elegir el accesorio afín.
Navegá el link del carrito para obtener el total real 6x5.

Guardá el resultado en templates/vinos-seleccion-mayo2026.html
```

### Modo manual — vos traés URLs de productos
```
Leé los archivos guidelines/ligier-email-guidelines.md y prompts/instrucciones-claude.md completos antes de hacer cualquier cosa. Confirmame que los leíste y resumí las reglas críticas.

Luego leé también el template de referencia: templates/base-email-vinos.html — esta es la base que tenés que usar. Copiá toda la estructura HTML y CSS, y reemplazá solo el contenido variable (productos, precios, hero copy, links).

Generá un email con estos datos:

TIPO: vinos
CRITERIO: selección curada
MES Y AÑO: Mayo 2026

PRODUCTOS:
- https://vinotecaligier.com/producto-1.html
- https://vinotecaligier.com/producto-2.html
- https://vinotecaligier.com/producto-3.html
- https://vinotecaligier.com/producto-4.html
- https://vinotecaligier.com/producto-5.html
- https://vinotecaligier.com/producto-6.html

Visitá cada URL, verificá stock e imagen, extraé el SKU de cada producto.
Generá el link de carrito con los 6 SKUs.
Navegá https://vinotecaligier.com/cristaleria para elegir el accesorio afín.
Navegá el link del carrito para obtener el total real 6x5.

Guardá el resultado en templates/vinos-seleccion-mayo2026.html
```

---

## PROMPT DE CORRECCIONES

Para corregir un email ya generado sin rehacerlo desde cero:

```
Leé guidelines/ligier-email-guidelines.md antes de hacer cualquier cambio.

Corregí el archivo templates/[nombre].html con lo siguiente:

- [describí cada corrección en una línea]
- [describí cada corrección en una línea]

No tocar ninguna otra sección.
```

---

## CHECKLIST ANTES DE APROBAR

Antes de subir a Mailchimp, verificar:

- [ ] Se ve bien en desktop (abrir el HTML en el browser)
- [ ] Se ve bien en mobile (reducir el browser a 375px)
- [ ] 6 productos de la categoría correcta
- [ ] Precio tachado + precio promo + label "c/u comprando 6"
- [ ] Link del carrito funciona y abre los 6 productos
- [ ] Total 6x5 debajo del botón pack es el real del carrito
- [ ] Accesorio afín con botón outline
- [ ] 10 categorías completas
- [ ] Íconos de WhatsApp, teléfono e Instagram visibles
- [ ] Sin logo en el footer
- [ ] Correo de prueba enviado a dayanmartin@gmail.com
