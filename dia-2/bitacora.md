# Bitácora · Semana 3 · Día 2 — Rueda Nocturna

## MiniReto 5 — Maquetación de la landing (escritorio)

- Estructura: `<header>`, `<main>` con una `<section>` por bloque (`#inicio`, `#rutas`, `#como-funciona`, `#inscripcion`) y `<footer>`. Los enlaces del encabezado llevan a cada `id`.
- Todas las secciones usan el mismo contenedor: `mx-auto max-w-6xl px-8`.
- Encabezado: `flex items-center justify-between`. El logo va a un lado y los enlaces más el botón al otro.
- Rutas: `grid grid-cols-3 gap-6`.
- Pie: `flex justify-between` con 3 bloques (Rueda Libre, Contacto, Horario).
- Los componentes (botones, card, campo) están copiados del kit sin cambiarles nada.

**¿Grid o flex para los 4 pasos?** Usé **grid** (`grid-cols-4`). Son 4 cajas iguales que tienen que medir lo mismo y alinearse en columnas. Con grid eso sale solo y además me sirve para cambiar a 1 o 2 columnas en el celular. Con flex tendría que dar un ancho a cada caja.

## MiniReto 6 — Responsive (mobile-first)

**Lo que se rompía a 360 px (landing del reto 5):**
1. La página tenía scroll horizontal: medía **550 px** de ancho en una pantalla de 360.
2. El encabezado se salía: la fila de enlaces más el botón llegaba hasta los **568 px**.
3. Las 3 cards de rutas quedaban de **83 px** de ancho cada una, ilegibles.
4. Los 4 pasos quedaban de **56 px** cada uno.
5. El título a 72 px no cabía (342 px de texto en 296 px de espacio).
6. El formulario de la franja se salía hasta los **470 px**.
7. El pie con 3 bloques en fila también se salía (425 px).

**Qué cambié:** las clases sin prefijo son para el celular y los prefijos agregan cosas a partir de cierto ancho.
- Rutas: `grid-cols-1 sm:grid-cols-2 lg:grid-cols-3`.
- Pasos: `grid-cols-1 sm:grid-cols-2 lg:grid-cols-4`.
- Encabezado: `flex-col` en el celular y `md:flex-row` desde 768 px.
- Enlaces del menú: `hidden md:block`. El botón "Inscríbete" siempre se ve.
- Título: `text-4xl sm:text-5xl lg:text-7xl`.
- Relleno de las secciones: `px-4 py-12 md:px-8 md:py-16 lg:py-24`.
- Franja y pie: en columna en el celular y en fila desde `lg` / `md`.

**Pruebas (modo dispositivo):**

| Ancho | Scroll horizontal | Encabezado | Menú | Rutas | Pasos | Título |
|---|---|---|---|---|---|---|
| 360 px | No | Apilado | Oculto (solo botón) | 1 columna | 1 columna | 36 px |
| 768 px | No | En fila | Visible | 2 columnas | 2 columnas | 48 px |
| 1024 px | No | En fila | Visible | 3 columnas | 4 columnas | 72 px |
| 1280 px | No | En fila | Visible | 3 columnas | 4 columnas | 72 px |

## MiniReto 7 — Tema de marca y modo oscuro

En `src/input.css`, con `@theme`, puse los mismos valores que usa el sitio de Rueda Libre:

| Nombre | Color | Utilidades |
|---|---|---|
| Verde Ruta | `#1B6B3A` | `bg-verde-ruta`, `text-verde-ruta` |
| Gris Asfalto | `#2B3035` | `bg-gris-asfalto`, `text-gris-asfalto` |
| Amarillo Señal | `#F2B705` | `bg-amarillo-senal` |
| Gris Niebla | `#E4E8E3` | `text-gris-niebla`, `border-gris-niebla` |
| Fondo | `#FAFAF7` | `bg-fondo` |
| Amarillo Farol (campaña) | `#FFD166` | `text-amarillo-farol` |

Fuentes: `--font-titulos` (Montserrat) y `--font-texto` (Open Sans), cargadas desde Google Fonts. Así se generan `font-titulos` y `font-texto`.

- Quité **todos** los colores de Tailwind (slate, amber, sky, emerald, rose) de la landing y del kit. Solo quedan los de la marca, más blanco y negro.
- Modo oscuro con `dark:` (sigue la preferencia del sistema). El fondo pasa a Gris Asfalto, las cards y las cajas a negro, los textos a Niebla o blanco, y el acento a Amarillo Farol.
- Niveles: Fácil en verde, Medio en amarillo y Difícil en asfalto (en oscuro, niebla). El texto siempre dice el nivel.

**Contraste (verificador WCAG, mínimo 4.5:1):**

| Combinación | Dónde | Resultado |
|---|---|---|
| Gris Asfalto sobre Fondo | textos en claro | 12.74:1 ✅ |
| Verde Ruta sobre Fondo | precios, acento en claro | 6.25:1 ✅ |
| Blanco sobre Verde Ruta | botón secundario, nivel Fácil | 6.54:1 ✅ |
| Gris Asfalto sobre Amarillo Señal | botón principal, nivel Medio | 7.33:1 ✅ |
| Gris Asfalto 70 % sobre blanco | datos secundarios en cards | 5.12:1 ✅ |
| Niebla sobre Gris Asfalto | textos en oscuro | 10.75:1 ✅ |
| Amarillo Farol sobre negro | precios en oscuro | 14.56:1 ✅ |
| Niebla 70 % sobre negro | datos secundarios en oscuro | 8.16:1 ✅ |
| **Verde Ruta sobre Gris Asfalto** | (lo descartado) | **2.04:1 ❌** |
| **Amarillo Señal sobre Fondo** | (lo descartado) | **1.74:1 ❌** |

Corrección: en modo oscuro el verde **no se usa como texto**, solo como fondo con texto blanco. El acento de texto pasa a Amarillo Farol. Y el Amarillo Señal en claro solo va de fondo con texto asfalto, nunca como texto. El placeholder tenía 3.81:1 con 60 % de opacidad, así que lo subí a 70 % (5.12:1).

Probado emulando `prefers-color-scheme: dark` en 360, 768, 1024 y 1280: todas las secciones cambian y el modo claro sigue igual.

## MiniReto 8 — Código legible y veredicto

**Listas de clases más repetidas (landing del reto 7):**

| Pieza | Veces | Clases |
|---|---|---|
| Botón principal | 6 | 21 clases cada uno |
| Nombre de dato (`dt`, etiquetas pequeñas) | 9 + 5 | 4 clases |
| Valor de dato (`dd`) | 9 | 4 clases |
| Texto secundario | 7 | 4 clases |
| Precio / número destacado | 7 | 5 clases |
| Caja de paso | 4 | 7 clases |
| Card de ruta | 3 | 13 clases |

- **@apply (solo 3 clases)** en `@layer components`: `.btn-primario`, `.btn-secundario` y `.btn-contorno`. Todos los botones de la landing y del kit las usan. Las demás piezas siguen con utilidades, porque las cards son marcado grande y las copio igual del kit.
- **Orden de clases** en cada elemento: layout → espaciado → tipografía → color/bordes → estados (`hover:`, `focus:`) → `dark:`.
- Comparé la landing antes y después en 360 y 1280, claro y oscuro: misma posición, tamaño y color en todos los elementos. Se ve igual.

**Tamaños medidos:**

| Archivo | Tamaño | Comprimido (gzip, lo que viaja) |
|---|---|---|
| Tailwind `output.css` sin minificar | 36.4 KB | 5.5 KB |
| **Tailwind `output.css` con `--minify`** | **29.1 KB** | **5.1 KB** |
| Bootstrap 5.3.3 `bootstrap.min.css` | 232.8 KB | 31.1 KB |
| Bootstrap 5.3.3 `bootstrap.bundle.min.js` | 80.7 KB | 23.7 KB |
| **Bootstrap total (CSS + JS)** | **313.5 KB** | **54.8 KB** |

El sitio v2.0 en Bootstrap carga unas **10 veces más** que la landing en Tailwind.

**Bootstrap vs Tailwind:**

| Criterio | Bootstrap (sitio v2.0) | Tailwind (Rueda Nocturna) |
|---|---|---|
| Curva de aprendizaje | Más fácil al inicio: `btn btn-warning` y listo. Toca aprender sus nombres (`row`, `col-md-6`, `card-body`). | Más lento al principio: hay que saber CSS (padding, flex, grid) y muchos nombres de utilidades. Luego es más rápido porque no cambio de archivo. |
| Personalización | Para usar mis colores tuve que pisar variables `--bs-*` y además las de cada botón (`--bs-btn-bg`, `--bs-btn-hover-bg`…) porque `--bs-primary` solo no cambia los botones. | Con `@theme` puse 6 colores y 2 fuentes, y salieron todas las utilidades (`bg-verde-ruta`, `font-titulos`). El modo oscuro sale con `dark:` sin JS. |
| Tamaño final | 313.5 KB (54.8 KB comprimido), aunque use pocos componentes. | 29.1 KB (5.1 KB comprimido): solo lo que uso. |
| Casos de uso | Paneles, prototipos rápidos, equipos que quieren componentes listos (carrusel, menú desplegable con JS). | Sitios con diseño propio de marca, landings, cuando importa la velocidad de carga. |

**Recomendación para Rueda Libre:** que la próxima versión de todo el sitio quede en **Tailwind**. Rueda Libre tiene una marca propia (6 colores y 2 fuentes) que en Tailwind se define una vez en `@theme`, carga unas 10 veces menos (importa porque casi todo el tráfico viene del celular) y ya tenemos el kit de componentes hecho. Lo único que da Bootstrap y Tailwind no trae es el JS del carrusel y del menú. Esas piezas se pueden reemplazar con un menú simple o con muy poco JS.
