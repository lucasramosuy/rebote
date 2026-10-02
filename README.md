# rebote.

Breakout con luz propia. Un dedo, una pelota y todo lo que brilla cuando algo se rompe.

Juego estático en un solo archivo (`index.html`), WebGL2 sin dependencias y sin paso de build. Pensado primero para iPhone (un dedo, arrastrar) y después para escritorio.

## Cómo se juega

- Arrastrá para mover la paleta (touch o mouse). Teclado: flechas o A/D.
- Tocá (o `Espacio`) para lanzar la pelota. `Espacio` o `Esc` pausan.
- Cada ladrillo seguido, sin tocar la paleta, sube la racha: más puntos y más brillo de fondo.
- Tres vidas. Al limpiar el tablero se pasa de nivel (más rápido, con otro diseño).

## Efectos

| Modo | Qué hace |
|---|---|
| Brillo | Bloom en dos escalas, estela, partículas, onda expansiva con aberración cromática, fondo reactivo a la racha, scanlines, viñeta. Resolución hasta 2x. |
| Ligero | Un solo bloom de baja resolución, sin aberración ni scanlines, resolución hasta 1.25x. Para equipos lentos. |

Si el sistema pide menos movimiento (`prefers-reduced-motion`), arranca en Ligero y sin vibración de pantalla.

## Datos locales

Solo `localStorage` del navegador: `rebote.record` (récord) y `rebote.fx` (modo). Nada sale del dispositivo, sin cuentas ni analítica.

## Identidad

Sigue el brand kit del dominio: wordmark `rebote.` con el punto en el acento lima lavado `#c9dc7a`, Space Grotesk + DM Mono (Fontsource, embebidas en base64 dentro del HTML, sin fuentes del sistema ni Google Fonts), modo oscuro por ser herramienta. Pendiente de registrar en BRAND.md: acento lima `#c9dc7a`, base `#0b0d0c`.

## Despliegue

Es un archivo estático: servirlo como `/rebote/` (por ejemplo desde GitHub Pages) y agregar la entrada en /links. No necesita build.

## Desarrollo

El HTML es autocontenido; el JS vive al final del archivo. Para depurar, abrir con `#debug` en la URL expone `window.__rebote`.
