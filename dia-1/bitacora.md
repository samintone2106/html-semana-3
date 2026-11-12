# Bitácora · Semana 3 · Día 1 — Rueda Nocturna

Rueda Nocturna es la campaña nocturna de Rueda Libre. Cada reto trae el sitio de Rueda Libre (v1.5) y la carpeta `nocturna/` con la landing en Tailwind.

## MiniReto 1 — Prototipo con Play CDN

**El botón "Inscríbete" en Bootstrap (semana 2):**
```html
<a href="#inscripcion" class="btn btn-warning btn-lg">Inscríbete</a>
```
Con tres clases ya estaba listo. Bootstrap decide el relleno, el radio, el color, el hover y el foco.

**El mismo botón en Tailwind (hoy):**
```html
<a href="#inscripcion" class="inline-block rounded-lg bg-amber-400 px-6 py-3 text-base font-semibold text-slate-950">Inscríbete</a>
```
Lo armé con utilidades: `px-6 py-3` (relleno), `rounded-lg` (radio), `bg-amber-400 text-slate-950` (colores) y `text-base font-semibold` (letra).

**Diferencia clave:** Bootstrap (componentes) te da la pieza terminada, y es rápido pero todo se parece. Tailwind (utility-first) te da propiedades sueltas y tú armas la pieza: hay más clases en el HTML, pero tienes control total sin escribir CSS.

## MiniReto 2 — Tailwind CLI y botones

```bash
npm install -D tailwindcss @tailwindcss/cli
npx @tailwindcss/cli -i ./src/input.css -o ./src/output.css --watch
```
- `src/input.css` solo tiene `@import "tailwindcss";`.
- `.gitignore` deja fuera `node_modules/`. `output.css` sí se sube, porque GitHub Pages no corre la CLI.

**Clase usada vs. no usada:**
- `bg-amber-400` (la uso): **sí** aparece en `output.css`.
- `bg-pink-500` (no la uso): **no** aparece.

Por qué: la CLI lee mis HTML y solo genera el CSS de las clases que encuentra.

**Botones:** principal, secundario y contorno. Todos tienen `hover:` y, como quité el contorno del navegador (`focus:outline-none`), le puse un anillo `focus:ring-4`. Los probé con Tab y los tres muestran el anillo.

## MiniReto 3 — Cards de rutas

- Las 3 cards tienen las mismas clases. Solo cambian los datos y el color de la etiqueta.
- El nivel va por color **y** por texto ("Nivel: Fácil / Medio / Difícil").
- Imagen: `h-48 w-full object-cover`, misma altura en todas.
- Datos: el nombre va pequeño y gris (`text-xs uppercase text-slate-400`) y el valor grande (`text-lg font-semibold`).
- Hover: solo cambian el color del borde y la sombra. No cambia el grosor ni hay `translate`, así que nada se mueve.

## MiniReto 4 — Kit de componentes v0.1

Página `nocturna/componentes.html`: 3 botones, card, 3 alertas y 2 campos.

**Reglas del kit:**

| Regla | Valor |
|---|---|
| Radio | `rounded-lg` en controles (botones, campos, etiquetas) · `rounded-2xl` en contenedores (cards, alertas) |
| Borde | `border-2` · alertas `border-l-4` |
| Espaciado | escala 1-2-3-4-6-8: botón `px-6 py-3`, campo `px-4 py-3`, card y alerta `p-6` |
| Colores | fondo `slate-950/900`, un acento `amber-400/300`, info `sky`, éxito `emerald`, advertencia `amber` |
| Foco | `focus:ring-4` + `focus:ring-offset-2` en todo lo que se puede usar con teclado |

- La alerta de éxito tiene `role="alert"`, así el lector de pantalla la anuncia.
- Cada campo tiene `<label for>` y su texto de ayuda va enlazado con `aria-describedby`.
