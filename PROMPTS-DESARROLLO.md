# TACO CITY — Prompts de Desarrollo Profesional (juego 100% autónomo)

> Objetivo: que cualquier estudio o IA pueda **diseñar, construir y pulir** este juego a nivel
> profesional sin depender de terceros. Stack actual: **un solo `index.html`** (HTML5 Canvas 2D +
> JS vanilla), PWA con Service Worker, sin servidor. Todo corre offline y se sirve como link estático.

---

## 0. Visión (pitch de una línea)
Un **roguelike educativo** donde sos un **taco humanoide** que recorre una **ciudad 3D top-down**
(manzanas, avenidas, tiendas), pelea, maneja autos, se viste/diseña, y **aprende idiomas + mate +
lógica** mientras juega. Pegajoso, “4D/5D”, jugable en cualquier celular por un link.

## 1. Pilares de diseño
1. **Educativo adictivo**: idioma (CEFR/HSK), matemática y lógica por edad; sistema “neural” que
   repite lo que fallás y avanza de nivel. Recompensa con cosméticos.
2. **Ciudad viva y real**: edificios extruidos con azotea/ventanas, calles con carriles y cebras,
   tiendas con toldo, faroles, árboles, flores, gente y autos. **Día/noche + clima + temperatura**.
3. **Personalización profunda**: el taco **arranca bebé y crece**; vestuario con equipos, caras,
   accesorios y vehículos; “diseñá tu taco” con preview en vivo.
4. **Multijugador local**: perfiles por dispositivo, cada uno con su progreso (resume de sesión).
5. **Juicy/“4D”**: partículas, screen-shake, flotantes, combos, glow, sonido sintetizado, háptica.

## 2. Especificación funcional (estado actual + objetivo)
- **Mundo**: grilla fija grande con cámara que sigue al taco. Generación tipo **ciudad en cuadras**:
  manzanas de edificios separadas por avenidas de 2–4 celdas, ~20% plazas abiertas para combate.
- **Combate twin-stick**: stick izq mueve (doble-toque = dash), stick der apunta/dispara.
  Armas: SALSA, ESCOPETA, RÁFAGA, LÁSER, PLASMA, **BAZUCA (explosiva, daño en área)**.
- **Misiones por nivel**: juntar gemas / derrotar N / rescatar 3. Al completar abre **portal** → quiz.
- **Quiz “neural”**: mezcla idioma (traducí es→idioma con voz), matemática (por edad) y lógica.
- **Tienda** (powerups) + **interiores de tienda** (entrar al edificio: estanterías, cajero, compras).
- **Vehículos**: mounts pagos (patines/patineta/scooter/bici) suben velocidad; **manejar autos** de la
  calle (atropellan enemigos).
- **Día/noche** (faroles encendidos de noche, sol/luna), **clima** (sol/nublado/lluvia) y **temperatura**.
- **Perfiles** locales con progreso, banco de monedas, desbloqueos, idioma y nivel por edad.

### Pendientes / roadmap (para llevar a 100%)
- [ ] **Resume de sesión**: guardar la partida en curso (nivel, score, vida, arma, pos) y “CONTINUAR”.
- [ ] **Interiores caminables** (free-roam) en lugar de modal.
- [ ] **Minijuegos intermedios**: ruleta de premios, UNO/memoria/cartas dentro del escenario.
- [ ] **Más trajes temáticos** (astronauta, ninja, superhéroe…) en la tienda.
- [ ] **Estaciones** (verano/invierno) que cambian paleta, clima y temperatura base.
- [ ] **Accesorios de noche** (linterna/lámpara que ilumina alrededor del taco).
- [ ] **Mapa/objetivos** y narrativa de misión (desbloquear barrios).

## 3. Arquitectura técnica
- **Loop**: `requestAnimationFrame`, `dt` clampeado (≤0.05). `update(dt)` + `render()` separados.
- **Estados**: `title | players | play | quiz | challenge | shop | interior | wardrobe | options | menu | over`.
- **Render en capas**: fondo screen-space → mundo bajo `ctx.translate(-camX,-camY)` (cache estático
  `dcanvas` por nivel) → overlay clima/día-noche → viñeta → HUD/sticks/botones.
- **Persistencia**: `localStorage`, namespaced por jugador `pl_<nombre>_<clave>`.
- **Audio**: WebAudio sintetizado (sin assets). **Voz**: `SpeechSynthesis` (idioma del item).
- **Responsivo**: `visualViewport` + safe-area insets; twin-stick táctil + teclado/mouse.
- **PWA**: `manifest.json` + `sw.js` network-first (evita caché viejo en GitHub Pages), íconos PNG.

## 4. Dirección de arte (todo vectorial en canvas, sin imágenes)
- Paleta por “dimensión”/mundo (caverna, bosque, volcán…). Edificios = versión apagada del color del
  mundo mezclada con gris. Sombras proyectadas abajo-derecha. Bisel claro arriba / sombra abajo.
- Personajes con **gradiente radial** (volumen), sombra elíptica, ojos que siguen objetivos.
- Decoración horneada en el cache: faroles (con glow nocturno), árboles en capas, jardineras de flores.

## 5. Prompts listos para usar (copiá/pegá a tu IA/equipo)

### 5.1 — Prompt maestro (build completo)
```
Construí un juego web educativo en UN SOLO archivo index.html (HTML5 Canvas 2D + JS vanilla, sin
dependencias, sin servidor, PWA offline). Es un roguelike top-down en una ciudad 3D donde el jugador
es un taco humanoide que pelea, recorre, maneja autos, entra a tiendas y APRENDE idiomas/mate/lógica.
Requisitos: twin-stick táctil + teclado; cámara que sigue al jugador; generación de ciudad en cuadras
con avenidas, plazas, tiendas y decoración (faroles/árboles/flores); ciclo día/noche con faroles que
encienden de noche; clima (sol/nublado/lluvia) y temperatura en HUD; armas múltiples incluida una
bazuca explosiva; misiones (gemas/derrotar/rescatar) que abren un portal de quiz “neural” que mezcla
idioma (es→idioma con pronunciación por voz), matemática por edad y lógica; tienda de powerups e
interiores de edificio; vestuario para DISEÑAR el taco (equipos, caras, accesorios, vehículos) con
preview en vivo; perfiles locales por dispositivo con progreso guardado en localStorage. El taco
arranca bebé y crece por nivel. Estética “juicy”: partículas, shake, combos, glow, audio sintetizado
y háptica. Entregá todo en index.html + manifest.json + sw.js (network-first) + íconos.
```

### 5.2 — Sistema educativo “neural”
```
Implementá un motor de aprendizaje adaptativo: ítems {es, idioma, pronunciación} por nivel CEFR/HSK.
Asigná el nivel inicial según la edad (siempre uno por encima). Ponderá la selección para repetir lo
que el jugador falla (racha=0 pesa más) y avanzar cuando domina. Generá quizzes de opción múltiple
es→idioma con voz (SpeechSynthesis), y problemas de matemática/lógica escalados por edad. Guardá
estadísticas por ítem (vistos/aciertos/racha) por jugador. Recompensá con monedas y desbloqueos.
```

### 5.3 — Ciudad 3D y decoración
```
Generá la ciudad como manzanas (rectángulos) separadas por avenidas de 2–4 celdas, con ~20% plazas.
Dibujá cada edificio extruido: sombra proyectada, paredes sur/este con ventanas iluminadas, azotea
con parapeto y detalles (AC/tanque/acceso), altura variable (skyline). Agregá veredas de hormigón,
líneas de carril, cruces peatonales, faroles (glow de noche), árboles, jardineras de flores y tiendas
con toldo a rayas + cartel + puerta. Horneá todo en un canvas estático por nivel para rendimiento.
```

### 5.4 — Día/noche + clima
```
Agregá un reloj continuo (ciclo ~3–4 min) que controla un valor noche 0..1. Oscurecé la escena de
noche, encendé los faroles (glow additive en sus posiciones), mostrá sol o luna cruzando el cielo, y
tintes cálidos en amanecer/atardecer. Elegí clima por nivel (sol/nublado/lluvia) con partículas de
lluvia en screen-space y mostrá la temperatura (varía por clima y hora) en el HUD.
```

### 5.5 — Personalización / vestuario
```
Creá un vestuario con pestañas: EQUIPOS, CARAS, ACCESORIOS, VEHÍCULOS. Equipos y vehículos se compran
con monedas; caras y accesorios se DESBLOQUEAN diciendo la expresión en el idioma (mini-reto con voz).
Mostrá un PREVIEW grande en vivo del taco que refleja la combinación. Guardá la selección por jugador.
El taco arranca pequeño (bebé) y crece con el nivel.
```

### 5.6 — Vehículos e interacción
```
Mounts (patines/patineta/scooter/bici) que suben la velocidad y se dibujan bajo el taco con ruedas que
giran. Permití SUBIR a los autos de la calle (botón contextual): el auto se maneja rápido y atropella
enemigos; BAJAR para salir. Edificios-tienda con puerta: botón ENTRAR abre un interior (estanterías,
cajero, compras). El portal se entra al tocarlo.
```

### 5.7 — Minijuegos intermedios (roadmap)
```
Agregá minijuegos dentro del escenario, accesibles desde objetos/locales: una RULETA de premios
(monedas/powerups), un juego de cartas tipo UNO contra 1–3 NPCs (colores/números, comodines), y un
memoria de vocabulario (parear es↔idioma). Cada minijuego otorga monedas y refuerza lo aprendido.
```

## 6. Definición de “terminado” (checklist de calidad)
- [ ] 60 fps en celulares de gama media; sin fugas de memoria (cache por nivel).
- [ ] Responsivo real (notch/safe-area), controles cómodos con una mano.
- [ ] Progreso y sesión persistentes por jugador; resume confiable.
- [ ] Accesibilidad: alto contraste, texto legible, opción de bajar gráficos.
- [ ] Sin dependencias externas ni assets binarios pesados (todo vectorial/sintetizado).
- [ ] Verificación visual real en dispositivo (capturas) en cada release.

## 7. Prompts de INGENIERÍA / CONSTRUCCIÓN (centro comercial + modo obra)

### 7.1 — Mall de varios pisos (estructura real)
```
Diseñá un centro comercial jugable de 4 pisos en canvas 2D top-down. Cada piso tiene su temática y
sus locales (estaciones): Planta Baja (salud/poderes/comida), Piso 2 Moda (vestuario/accesorios/
vehículos), Piso 3 Diversión (ruleta/memoria/UNO), Piso 4 Cine y Terraza. Una escalera/elevador con
botones ▲▼ cambia de piso y regenera las estaciones. Decorá con vidrieras de locales en la pared,
gente caminando, plantas, bancos, guirnaldas de luces y ventana con vista día/noche. El jugador
camina con el stick, toca una estación y se despliega un menú de opciones con precios en monedas.
Mostrá feedback visible de compra (LISTO!/te faltan monedas).
```

### 7.2 — Modo construcción del taco (con cuadrilla y OSHA)
```
Agregá un MODO CONSTRUCCIÓN: el taco puede comprar un terreno y contratar CONSTRUCTORES (NPCs con
casco y chaleco). El jugador elige un DISEÑO de edificio (casa, tienda, torre) y HERRAMIENTAS
(grúa, andamio, hormigonera). La obra avanza por etapas (cimientos → estructura → fachada → techo)
con una barra de progreso y costo en monedas/tiempo; los obreros animan el trabajo. Cumplí seguridad
OSHA: casco, chaleco reflectivo, antiparras, orejeras, conos y cinta de peligro; mostrá un "puntaje
de seguridad" que sube si el taco y la cuadrilla usan el equipo correcto. Al terminar, el edificio
queda en la ciudad y se puede entrar (otro local del mall). Todo vectorial, con sombras y volumen
4D/5D (extrusión, degradados, rim-light, AO).
```

### 7.3 — Herramientas de diseño de edificios (editor)
```
Construí un editor simple de edificios: el jugador elige cantidad de pisos, color, tipo de techo,
ventanas (encendidas/apagadas), toldo/cartel de tienda y detalles de azotea (AC, tanque, antena).
Previsualizá el edificio extruido en tiempo real (paredes con degradado, parapeto, rim-light, AO).
Guardá el diseño por jugador y permití colocarlo en un terreno de la ciudad. Reglas de seguridad
(OSHA): vallado de obra, señalización y EPP obligatorio para habilitar la construcción.
```

### 7.4 — Seguridad laboral (OSHA) como mecánica educativa
```
Convertí la seguridad en aprendizaje: antes de construir, un mini-quiz de EPP (¿qué te ponés para
trabajar en altura?) con casco/arnés/chaleco; acertar desbloquea el equipo y sube el "puntaje de
seguridad". Accesorios OSHA en el vestuario: CASCO DE OBRA, ANTIPARRAS, OREJERAS y traje
CONSTRUCTOR (chaleco reflectivo). Basado en buenas prácticas reales de seguridad en el trabajo.
```

---
*Este documento acompaña a `index.html` y describe el juego tal como está y a dónde va.*
