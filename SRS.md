# SRS - rebote.

## 1. Propósito
Juego breakout web, estático y gratuito, con un tratamiento visual basado en shaders. Producto del dominio, con identidad propia según el brand kit.

## 2. Alcance
Una sola página (`index.html`). Sin backend, sin dependencias, sin build, sin cuentas.

## 3. Requisitos funcionales
- RF1. Pantalla de inicio con el juego corriendo solo (modo attract), récord, botones Jugar, Cómo se juega y selector Brillo/Ligero.
- RF2. Control con un dedo arrastrando, con mouse y con teclado (flechas, A/D).
- RF3. Lanzamiento con toque, clic o Espacio; pausa con botón, Espacio o Esc; pausa automática al perder foco.
- RF4. Puntaje, racha (combo), tres vidas y niveles con diseños distintos y velocidad creciente.
- RF5. Ladrillos de 1 o 2 golpes según el nivel.
- RF6. Récord persistente en `localStorage`; pantalla de fin con puntaje y aviso de récord nuevo.
- RF7. Modo Brillo y modo Ligero, recordado entre sesiones; Ligero por defecto si el sistema pide menos movimiento.
- RF8. Si no hay WebGL2, mensaje claro en lugar de pantalla en blanco.
- RF9. Enlace "← lucas." al dominio.

## 4. Requisitos no funcionales
- RNF1. Rendimiento: 60 fps objetivo en iPhone reciente en Brillo; Ligero para equipos lentos. Resolución de render limitada (2x y 1.25x).
- RNF2. Mobile primero: pantalla completa, sin zoom ni scroll, zonas táctiles de al menos 40 px, áreas seguras (notch) respetadas.
- RNF3. Sin fuentes del sistema ni de terceros: Space Grotesk y DM Mono embebidas.
- RNF4. Privacidad: sin apellido del autor, sin emails, sin analítica, sin red.
- RNF5. Accesibilidad: botones reales con foco visible, `aria-label` en controles sin texto, respeta `prefers-reduced-motion`.
- RNF6. Español rioplatense, voseo.

## 5. Arquitectura
- Render: WebGL2. Pasada de escena con instancias (ladrillos, partículas, estela, pelota, paleta) dibujadas con SDF en el fragment shader; extracción de brillo y desenfoque gaussiano en dos escalas (mitad y cuarto); composición final con fondo procedural (grilla y brillo por racha), distorsión por ondas con aberración cromática, scanlines y viñeta.
- Lógica: bucle con paso variable acotado, colisión pelota-ladrillo por círculo contra rectángulo con sub-pasos de 3 unidades de mundo. Mundo de 360 unidades de ancho; el alto depende del aspecto.
- UI: HTML/CSS sobre el canvas (HUD, overlays, botones). Estado en `data-state` del contenedor.

## 6. Verificación
Playtest en Chrome headless con WebGL2 (software) a 390 y 1280 px: arranque en attract, inicio de partida con toque y clic, arrastre del paleta, lanzamiento, pausa y reanudación (la pelota queda quieta), cambio a Ligero, fin de partida con récord persistente tras recargar.

## 7. Fuera de alcance
Sonido, multijugador, ranking en línea, instalación como app.
