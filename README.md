# Catacomb — versión web (jugable en iPad)

Reimplementación web del taco roguelike en **HTML5 Canvas + JavaScript**, en un solo archivo
(`index.html`), sin dependencias ni build. Corre en cualquier navegador moderno, **incluido Safari
del iPad**, con **controles táctiles**.

## Controles
- **Táctil (iPad):** joystick izquierdo (mitad izquierda de la pantalla) = mover; joystick derecho
  (mitad derecha) = apuntar y disparar.
- **Teclado/mouse (PC):** WASD o flechas = mover; mouse = apuntar; mantener clic = disparar.
- Juntá todas las gemas → aparece el **portal** → andá al remolino para pasar de nivel.
- Disparale a los enemigos; te curás con los corazones verdes que sueltan.

## Probar en la PC (rápido)
Doble clic en `index.html` (se abre en el navegador). Listo.

## Conseguir el LINK para el iPad (sin servidor, elegí uno)

### Opción A — Netlify Drop (la más fácil, SIN cuenta)
1. Entrá a **https://app.netlify.com/drop**
2. Arrastrá la **carpeta `Catacomb-Web`** entera a la página.
3. Te da una **URL pública al instante** (ej. `https://algo-random.netlify.app`).
4. Abrí esa URL en **Safari del iPad** y jugá. (Tip: "Compartir → Agregar a inicio" para que quede
   como una app a pantalla completa.)

### Opción B — itch.io (página de juego)
1. Comprimí la carpeta en un `.zip` (que `index.html` quede en la raíz del zip).
2. En itch.io: *Upload new project* → *Kind = HTML* → subí el zip → marcá "This file will be played
   in the browser" → guardá. Te da un link público.

### Opción C — GitHub Pages (link estable que crece con el proyecto)
1. Subí esta carpeta a un repo de GitHub.
2. *Settings → Pages → Deploy from branch → main → /root*.
3. Tu link queda en `https://TU-USUARIO.github.io/REPO/`.

## Nota
Es un **slice jugable** (mover, esquivar, juntar gemas, disparar, jefes-bloque, niveles, vida, récord
local). No tiene todavía todo lo de la versión de escritorio (portales de inglés, skins, daily,
power-ups, jefe grande), pero se le va sumando. La versión completa sigue siendo la de C#/MonoGame
para PC.
