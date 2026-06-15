# TACO CITY — Mockup Nano Banana del JUEGO COMPLETO (inicio a fin)

> Para qué: generar con **Nano Banana** un mockup visual de **cómo se ve el juego, pantalla por
> pantalla, de inicio a fin**. Cada bloque = un prompt para una pantalla. Generá en **9:16 (celular)**
> y **16:9 (escritorio)**. El código (canvas) debe quedar **idéntico** al mockup (diseño + estructura
> + vista), como en el flujo de CleanPro-ERP.
>
> **Estilo global (respetar en TODAS):** juego 3D estilizado amigable tipo Crash/Roblox, materiales con
> volumen, luz cinematográfica (key + rim light), sombras suaves, paleta alegre (amarillo #f5cd46,
> cyan #7fd6ff, verde #60d050, magenta #e0479a, dorado #ffd84a, violeta #b480ff). Protagonista SIEMPRE:
> un **TACO humanoide** (tortilla amarilla doblada con relleno lechuga/tomate/queso, ojos grandes,
> bracitos, piecitos). HUD oscuro glassy con acentos neón. Sin marcas registradas.

---

## 0. Flujo (orden de pantallas)
```
TÍTULO → ELEGIR JUGADOR → CIUDAD(combate, día/noche/lluvia) → PORTAL(quiz idioma + pronunciación)
   → MALL(4 pisos) → TIENDA(interior) → MODO OBRA(construcción) → DIMENSIÓN 3D(iso)
   → VESTUARIO(diseñá tu taco) → GAME OVER → (vuelve a TÍTULO)
```

## 1. TÍTULO
```
Title screen mockup of mobile game "TACO CITY". Big chunky 3D logo. Hero taco character in a heroic pose
with a frog bucket hat. Behind: colorful city skyline at golden hour with a glowing purple portal.
Buttons: "TOCA PARA JUGAR", "CONTINUAR · Mundo 3", "VESTUARIO", "OPCIONES", "DIMENSIÓN 3D". Cinematic,
bloom, vignette, joyful palette. 9:16 and 16:9.
```

## 2. ELEGIR JUGADOR (perfiles)
```
Player-select screen of a cute game: dark glassy panel titled "JUGADORES", a vertical list of player
cards (name + best score + delete X), a big "+ NUEVO JUGADOR" button, neon cyan accents, friendly. The
taco mascot peeking. 9:16.
```

## 3. CIUDAD + COMBATE (top-down, día)
```
Top-down stylized city for an action game: chunky extruded buildings with shaded faces and glowing
windows, asphalt streets with lane lines and crosswalks, sidewalks, flower planters, trees, street
lamps, parked cars, walking pedestrians. The taco hero in the center shooting salsa projectiles at
angry chili-pepper enemies. HUD: centered score, red health bar, weapon chip, minimap, mission banner
"MISIÓN: Derrota 4 enemigos 3/4", twin-stick controls, a friendly AI assistant bubble top-left. Sunny,
juicy, particles. 16:9.
```

## 4. CIUDAD de NOCHE + LLUVIA
```
Same stylized top-down taco city but at NIGHT with rain: dark blue tint, glowing warm windows and street
lamps, rain streaks, puddles, the taco emitting a soft light around itself, temperature "15° LLUVIA"
in HUD, moon in the sky. Moody but readable, cinematic. 16:9.
```

## 5. PORTAL — QUIZ de idioma + pronunciación
```
A glowing purple swirling portal quiz panel overlay: dark glassy card titled "PORTAL · INGLÉS", a Spanish
word to translate, 3 big multiple-choice answer buttons, a mastery dots row, a progress bar of mastered
words. Second state: a "PRONUNCIALO BIEN" screen with a big microphone button and the target word, kid-
friendly, educational. Neon violet/cyan. 9:16.
```

## 6. MALL (centro comercial, vista de un piso)
```
Interior of a bright stylized shopping mall, one floor: glass skylight atrium, upper-floor balcony
railing, a row of storefronts with striped awnings and readable signs (FARMACIA, GYM, MODA, ARCADE,
CAFÉ), mannequins in lit windows, a big animated escalator in the center, kiosks (SALUD, PODERES,
COMIDA, OBRA) as labeled stands, plants, benches, walking shoppers, the taco walking. Floor sign
"CENTRO COMERCIAL · PLANTA BAJA", coins on the floor, festive ceiling lights. 16:9.
```

## 7. TIENDA (interior de un local)
```
Inside a single mall shop (e.g. JUGUETES): shelves of colorful products, a counter with a taco cashier,
product pedestals on the floor with price tags in coins, the player taco walking inside, an EXIT door.
Warm shop lighting, readable, cute. 9:16.
```

## 8. MODO OBRA (construcción con OSHA)
```
Construction mode screen: a building rising in stages (foundation→structure→facade→roof) on a fenced
plot, a yellow crane with a hook, 3 worker tacos wearing hard hats and reflective vests, safety cones
and hazard tape, a progress bar "PROGRESO 2/4", an OSHA safety checklist (CASCO, CHALECO, CONOS, CINTA)
with a safety % meter, a big "CONSTRUIR ETAPA" button. Bright, instructive. 16:9.
```

## 9. DIMENSIÓN 3D (isométrica)
```
Isometric 2.5D version of the taco city: diamond-grid streets, chunky extruded buildings with 3 shaded
faces and glowing windows, the designed taco hero shooting at chili enemies in waves, power-up capsules
(shield, triple, speed), gems, a "MALL" building with a neon sign, day-to-night lighting. HUD shows wave
counter, health, weapon, shared coin bank "Banco", and a "← VOLVER" button. Cohesive with the top-down
game. 16:9.
```

## 10. VESTUARIO — "DISEÑÁ TU TACO"
```
Character customization screen "DISEÑÁ TU TACO": a big live preview of the taco on a lit stage, tabs
EQUIPOS / CARAS / ACCESORIOS / VEHÍCULOS, a scrollable grid of options (Mundial jerseys, face expressions,
hats/glasses/hard hat, roller skates/scooter/bike), price tags in coins, "EN USO" labels. Show variants:
frog hat, superhero cape, ninja, robot, construction outfit. Clean UI, joyful. 9:16.
```

## 11. GAME OVER
```
Game over screen of a cute game: dark overlay, big "GAME OVER", final score, words learned counter,
record, a "TOCA PARA REINTENTAR" prompt, the taco looking dizzy with stars. Encouraging, not scary. 9:16.
```

---

## Cómo lo usamos
1. Generás cada prompt en Nano Banana (9:16 + 16:9) → guardás en `scripts/nanobanana/output/juego/`.
2. Me los pasás (o los subís) y yo **ajusto el render del canvas** para que quede igual al mockup
   (sin cargar las imágenes como assets, para mantener el juego sin dependencias) — o las usamos como
   referencia/storyboard. Así tenemos un mockup oficial del juego de inicio a fin.
</content>
