# Bitácora · Semana 3 · Día 3 — Contrarreloj y lanzamiento

## MiniReto 9 — Contrarreloj 1: inscripción

**Tiempo real:** ___ min (meta: 40 min)

- Sección `#inscripcion` con su título y un `<form>` agrupado en 3 `<fieldset>` con `<legend>`: Tus datos, Tu salida y Confirmación.
- Control elegido para cada dato:

| Dato | Control | Regla |
|---|---|---|
| Nombre completo | `input type="text"` | `required minlength="3"` |
| Correo | `input type="email"` | `required` |
| Celular | `input type="tel"` | `required pattern="3[0-9]{9}"` + `title` con la explicación |
| Ruta | `select` (3 rutas) | `required` (la primera opción va vacía) |
| Día de salida | 3 radios (jueves, viernes, sábado) | `required` |
| Acompañantes | `input type="number"` | `required min="0" max="3"` |
| Experiencia | `select` (principiante, intermedio, avanzado) | `required` |
| Bicicleta propia | 2 radios (sí, no) | `required` |
| Condiciones | `checkbox` | `required` |

- Cada control tiene su `<label for>`. Los radios van dentro de un `<fieldset>` con su pregunta en el `<legend>`.
- Los campos cortos van en `grid md:grid-cols-2`. Usan el estilo del campo del kit, con `dark:` y `focus:`.

**Pruebas:**
- Vacío: no se envía y marca los 9 datos.
- Con datos malos ("Al", "ana@", celular 2001234567, 5 acompañantes): no se envía y cada campo dice su error.
- Completo y **solo con teclado** (Tab, flechas en los select y espacio en radios y casilla): se envía. El foco se ve en todo momento.
- 360 px en oscuro y 1280 px en claro: se ve bien y no hay scroll horizontal.

**Pendiente:** ___

## MiniReto 10 — Contrarreloj 2: un solo ecosistema

**Tiempo real:** ___ min (meta: 40 min)

- Sitio v2.0 (Bootstrap): agregué "Rueda Nocturna" en la navbar de las 3 páginas (`nocturna/index.html` desde el inicio y `../nocturna/index.html` desde `paginas/`). También agregué una 4.ª diapositiva al carrusel con el botón "Conoce la campaña".
- Landing (Tailwind): el logo lleva a `../index.html`. Hay un botón "Reserva tu bici" que lleva a `../paginas/reservas.html`, y el pie tiene enlaces al sitio y a reservas.
- Marca igual en los dos productos:

| Color | `--bs-*` (Bootstrap) | `@theme` (Tailwind) |
|---|---|---|
| Verde Ruta | `#1B6B3A` | `#1B6B3A` |
| Gris Asfalto | `#2B3035` | `#2B3035` |
| Amarillo Señal | `#F2B705` | `#F2B705` |
| Gris Niebla | `#E4E8E3` | `#E4E8E3` |
| Fondo | `#FAFAF7` | `#FAFAF7` |
| Amarillo Farol | `#FFD166` | `#FFD166` |

  Fuentes: el mismo enlace de Google Fonts (Montserrat 700 + Open Sans 400/600). Contacto: el mismo correo, WhatsApp y dirección en los dos pies.
- Revisé 45 enlaces y recursos locales: 0 rotos y 0 errores 404. Se llega del sitio a la landing con un clic desde las 3 páginas y desde el carrusel. Desde la landing se llega al sitio y a reservas.
- Revisión en GitHub Pages: ___

## MiniReto 11 — Contrarreloj 3: planes

**Tiempo real:** ___ min (meta: 45 min)

- Sección `#planes`: `grid grid-cols-1 lg:grid-cols-3 items-stretch gap-6`. Agregué "Planes" al menú.
- Cada card es `flex flex-col gap-6` y el botón tiene `mt-auto`, así siempre queda abajo. Los beneficios van en `flex flex-col gap-3`.
- Pareja: borde Verde Ruta (en oscuro Amarillo Farol), fondo distinto y la etiqueta "★ Más elegido" arriba. Así se distingue por color **y** por texto.
- Para no mover las otras cards, **las tres** tienen `border-4` (las otras dos con un borde de color neutro). La etiqueta va con `absolute -top-4`, así que no empuja el contenido.

**Medidas en DevTools (Computed) a 1280 px:**

| Card | Ancho × alto | Relleno | Borde | Botón (desde arriba) |
|---|---|---|---|---|
| Individual | 347 × 373 px | 24 px | 4 px | 345 px |
| Pareja | 347 × 373 px | 24 px | 4 px | 345 px |
| Grupo | 347 × 373 px | 24 px | 4 px | 345 px |

A 360 px quedan en una columna y sin scroll horizontal. Contraste: el par más bajo es el texto secundario sobre el fondo de la card Pareja en modo claro (4.67:1). En modo oscuro el más bajo es Niebla 70 % sobre Gris Asfalto (6.14:1).

**Pendiente:** ___

## MiniReto 12 — Lanzamiento

- Lista de verificación completa: está en el README (`reto-12-lanzamiento/README.md`).
- Validador W3C: el inicio tenía 1 error (`aria-label` en el `div` del carrusel). Lo corregí con `role="region"`. Ahora la landing, reservas, el inicio, tarifas y el kit dan **0 errores**.
- El README tiene descripción, enlaces, páginas, tecnologías, recomendación, capturas, aprendizajes y autor.

### Guion de la demo (3 min)

1. **Contexto (30 s):** Rueda Libre alquila bicis en Medellín. Lanza Rueda Nocturna, una campaña para redes, así que casi todo llega desde el celular.
2. **Recorrido (1 min 45 s):** inicio del sitio → navbar "Rueda Nocturna" (o 4.ª diapositiva) → landing → rutas y planes → inscripción: enviar vacío (lo bloquea) y completar con teclado → vista a 360 px en DevTools → modo oscuro (Rendering → `prefers-color-scheme: dark`) → logo de vuelta al sitio → "Reserva tu bici".
3. **Dos decisiones técnicas (45 s):**
   - Marca en `@theme` con los mismos hex que `--bs-*`: un solo origen de colores para los dos productos, y Tailwind genera `bg-verde-ruta` y el resto.
   - Contraste medido: Verde Ruta sobre Gris Asfalto daba 2.04:1. Por eso en modo oscuro el acento de texto es Amarillo Farol (14.56:1).

**Ensayo con cronómetro:** ___ min ___ s
**Retroalimentación del compañero:**
- ___
- ___
