# TACO CITY / CATACOMB — Diseño ELITE · Wireframe · Protocolo · Mockup (de inicio a fin)

> Documento vivo de UX y arquitectura del juego web (`index.html`, Canvas 2D + JS vanilla, PWA).
> Objetivo: experiencia **elite, clara y entendible desde el primer toque**, reusando todo lo que ya
> existe (no duplicar) y agregando lo genuinamente nuevo: **pantalla de inicio reconfigurada** +
> **salas y servidores premium**.

---

## 0. Filosofía elite (3 reglas)
1. **Claridad antes que features.** En cada pantalla el jugador entiende en <2 s qué puede hacer y cuál
   es la acción principal (1 botón primario grande + secundarios ordenados en grilla).
2. **Una sola fuente de verdad.** El juego YA tiene casi todo; lo elite es *ordenar, nombrar y pulir*,
   no recrear. (Regla dura: reusar lo existente.)
3. **PC + dispositivos por igual.** Todo es Canvas con hit-boxes por toque; los botones son grandes
   (≥40 px), legibles y con jerarquía de color/sombra.

---

## 1. Inventario: lo que YA existe (para NO duplicar)

| Pedido | Estado real en el código | Qué falta para "elite" |
|---|---|---|
| Continuar partida | ✅ `saveRun`/`resumeRun`, autosave c/4 s + al ocultar app | Exponerlo claro en la pantalla de inicio |
| Minijuegos | ✅ trivia, anagrama, math (`mathq`), secuencia, ruleta, memoria, UNO | Agruparlos en ACADEMIA + accesos claros |
| Tutor mates+inglés | ✅ hub `academia`, lecciones EN/ZH (A1→C1, HSK), asistente IA, voz | Entrada visible desde el inicio |
| Trajes / personalización | ✅ `wardrobe` (skins, caras, accesorios, vehículos) | — |
| Multijugador / salas | ✅ BETA PeerJS P2P (`net`, crear/unir por código) | **Lista de servidores + tier PREMIUM** (nuevo) |
| Servidores premium | ❌ no existe | **Construir** (este pase) |
| Pantalla de inicio elite | ⚠️ existe `title` con botones sueltos | **Reconfigurar** (este pase) |

**Conclusión:** el trabajo elite de este pase = (A) pantalla de inicio reconfigurada, (B) salas +
servidores premium, (C) documentación de inicio a fin (este archivo). El resto es pulido incremental.

---

## 2. Arquitectura (resumen)
- **1 archivo** `index.html` (~3.760 líneas): `<head>` + `<canvas id="c">` + `<script>` con todo el juego.
- **Render 100% Canvas** (no hay HTML/CSS para UI): cada pantalla = `drawXxx()` + `xxxRect()`/`xxxTapAt()`.
- **Máquina de estados:** `let state` con ~30 estados. Cambio = asignación `state = "..."` o `openXxx()`.
- **Loop:** `requestAnimationFrame` → `update(dt)` + `render()`. `dt` clamp ≤0.05.
- **Persistencia:** `localStorage`, por jugador con prefijo `pl_<nombre>_<clave>` (best, bank, run, lstats…).
- **Multijugador:** PeerJS WebRTC P2P, aislado (solo carga la lib al entrar a ONLINE).

### Estados (agrupados)
```
ARRANQUE → players (perfil) → title (INICIO)
INICIO   → play | salas(online) | academia | wardrobe | options | iso(3D) | players
JUEGO    → play → {quiz, interior, menu, shop, mirador, ia}
INTERIOR → {store, build, roulette, memory, uno, trivia, anagram, mathq, seq, cine}
FIN      → over → (title | players)
```

---

## 3. PROTOCOLO de navegación (de inicio a fin, explicado)

```
[1] BOOT (initPlayers)
      ├─ sin perfiles  ──────────────► [2] PLAYERS  (crear "+ NUEVO JUGADOR")
      ├─ datos viejos  ── migra ─────► [3] INICIO
      └─ con perfil    ──────────────► [3] INICIO

[2] PLAYERS  (selector de perfil; cada uno guarda su progreso)
      └─ elegir/crear perfil ────────► [3] INICIO

[3] INICIO (title)  ◄── reconfigurado ELITE
      ├─ ▶ CONTINUAR/JUGAR  ─────────► [4] PLAY
      ├─ 🌐 SALAS (multijugador)  ───► [5] SALAS
      ├─ 🎓 ACADEMIA  ───────────────► [6] ACADEMIA
      ├─ 👕 VESTUARIO ───────────────► wardrobe
      ├─ ⚙ OPCIONES  ───────────────► options
      ├─ 🌌 DIMENSIÓN 3D ────────────► game-iso.html (el banco viaja con vos)
      └─ 🔁 CAMBIAR JUGADOR ─────────► [2] PLAYERS

[4] PLAY (ciudad explorable, twin-stick)
      ├─ misión completa → portal ───► [7] QUIZ → nextLevel → PLAY
      ├─ puerta de edificio ─────────► INTERIOR → minijuegos
      ├─ edificio ACADEMIA ──────────► [6] ACADEMIA
      ├─ botón ≡ menú ───────────────► MENU (todas las opciones in-game)
      └─ vida 0 ─────────────────────► [8] OVER

[5] SALAS (online)  ◄── nuevo: lista de servidores + PREMIUM
      ├─ SERVIDOR gratis (1 toque) ──► PLAY con presencia online (ves a otros)
      ├─ SERVIDOR ⭐ PREMIUM ─────────► (si desbloqueado) PLAY · (si no) desbloquear con 🪙
      ├─ CREAR SALA PRIVADA (código) ► host
      ├─ UNIRSE POR CÓDIGO ──────────► join
      └─ VOLVER ─────────────────────► INICIO/MENU

[6] ACADEMIA (tutor neural)
      └─ elegir actividad ───────────► trivia | anagram | mathq | seq → vuelve a ACADEMIA/PLAY

[7] QUIZ (portal): idioma (50%) / mate (28%) / lógica (22%)
      ├─ correcto → (idioma) pronunciar con micrófono → nextLevel
      └─ incorrecto → reintento

[8] OVER → toca → reintento (PLAY) o cambiar perfil (PLAYERS)
```

---

## 4. WIREFRAMES (ASCII) de inicio a fin

### 4.1 PLAYERS (perfil)
```
            ╔══════════════════════════════╗
            ║          JUGADORES            ║
            ║  cada jugador guarda su prog.  ║
            ║ ┌──────────────────────────┐ ║
            ║ │ ● BICHO        récord 980 ✕│ ║
            ║ │   TACO2        récord 120 ✕│ ║
            ║ └──────────────────────────┘ ║
            ║ [   + NUEVO JUGADOR          ] ║
            ║ [   VOLVER                   ] ║
            ╚══════════════════════════════╝
```

### 4.2 INICIO (title) — RECONFIGURADO ELITE  ◄── mockup principal
```
┌────────────────────────────────────────────────────┐
│                      ╭───╮                            │
│                      │🌮 │   (taco mascota, glow)      │
│                      ╰───╯                            │
│                  C A T A C O M B                      │  título dorado, grande
│             el taco que aprende jugando               │  subtítulo
│   ┌────────────────────────────────────────────┐     │
│   │ 👤 BICHO · 🌎 Inglés A2 · 🧮 Mate Lv3 · 🪙 1240│     │  barra de perfil (cinta)
│   └────────────────────────────────────────────┘     │
│                                                        │
│        ╔══════════════════════════════════╗           │
│        ║   ▶   CONTINUAR · Mundo 5         ║           │  PRIMARIO (grande, glow verde)
│        ╚══════════════════════════════════╝           │  (si no hay run → "▶ JUGAR")
│        ┌──────────────────┐┌──────────────────┐       │
│        │ 🌐 SALAS          ││ 🎓 ACADEMIA       │       │  grilla 2×3, secundarios
│        └──────────────────┘└──────────────────┘       │
│        ┌──────────────────┐┌──────────────────┐       │
│        │ 👕 VESTUARIO      ││ ⚙  OPCIONES       │       │
│        └──────────────────┘└──────────────────┘       │
│        ┌──────────────────┐┌──────────────────┐       │
│        │ 🌌 DIMENSIÓN 3D   ││ 🔁 CAMBIAR JUGADOR│       │
│        └──────────────────┘└──────────────────┘       │
│   izq: mover (doble-toque esquiva) · der: apuntar      │  hint compacto
│                                            build vNN    │
└────────────────────────────────────────────────────┘
```
Jerarquía: **1 primario** (continuar/jugar) + **6 secundarios** en grilla. Color por función
(verde=jugar, cian=social/online, dorado=cosmético, violeta=3D). Cinta de perfil = identidad + progreso
visibles desde el inicio (motivación).

### 4.3 PLAY (HUD)
```
┌────────────────────────────────────────────────────┐
│ MUNDO 5 · NEÓN          🪙1240  ❤❤❤        ≡ 🔇 ⏸ 🔫 🌐│  top: estado + botones
│ MISIÓN: junta 6 gemas (3/6)                          │
│                                                        │
│                 · · ·  (ciudad)  · · ·                 │
│                        🌮                              │  jugador (centro, cámara sigue)
│              [minimapa]                  [    ENTRAR  ]│  botón contextual grande
│   (stick izq mover)                  (stick der apuntar)│
└────────────────────────────────────────────────────┘
```

### 4.4 SALAS (online) — RECONFIGURADO + PREMIUM
```
            ╔════════════════════════════════╗
            ║   MULTIJUGADOR · SALAS           ║
            ║   Estado: en SALA NEÓN · 3 online║
            ║ ┌────────────────────────────┐ ║
            ║ │ 🟢 CAVERNA        2/8  unir │ ║   servidores gratis (1 toque)
            ║ │ 🟢 BOSQUE         0/8  unir │ ║
            ║ │ ⭐ NEÓN  PREMIUM  5/24 unir │ ║   premium (badge dorado)
            ║ │ ⭐ ABISMO PREMIUM 0/24 🔒   │ ║   bloqueado → desbloquear 🪙
            ║ └────────────────────────────┘ ║
            ║ [ CREAR SALA PRIVADA (código) ] ║
            ║ [ UNIRSE POR CÓDIGO           ] ║
            ║ [ DESCONECTAR ]   [ VOLVER    ] ║
            ╚════════════════════════════════╝
```

### 4.5 ACADEMIA (tutor) · QUIZ · OVER
```
 ACADEMIA                         QUIZ (portal)              GAME OVER
 ╔══════════════╗                ╔════════════════╗         ╔══════════════╗
 ║ Hola BICHO 👋 ║                ║  ¿"PERRO" = ?   ║         ║  GAME OVER    ║
 ║ tutor: vamos! ║                ║ [ DOG ]         ║         ║ PUNTAJE 980   ║
 ║ ┌──────────┐ ║                ║ [ CAT ]         ║         ║ APRENDIDAS 42 ║
 ║ │RETO MENTAL│ ║                ║ [ FISH ]        ║         ║ RÉCORD 1200   ║
 ║ │PALABRAS   │ ║                ╚════════════════╝         ║ toca: reintento║
 ║ │ARMA PALABRA│ ║                (correcto→pronunciar 🎤)    ╚══════════════╝
 ║ └──────────┘ ║
 ╚══════════════╝
```

---

## 5. SALAS y SERVIDORES PREMIUM (diseño)

**Modelo honesto (sin backend de pago):** cada "servidor" es un `roomId` fijo sobre el PeerJS P2P ya
existente. No se cobra dinero real; **PREMIUM se desbloquea con las monedas del propio juego** (`bank`),
así se integra con la economía (no es una promesa de pago externa).

- **SERVIDORES gratis** (CAVERNA, BOSQUE…): unirse con **1 toque** (sin escribir código). Si no hay host,
  te volvés host; si existe, te unís. Cupo visible (n/8).
- **SERVIDORES ⭐ PREMIUM** (NEÓN, ABISMO…): cupo mayor (24), nombre dorado, badge ⭐. Requieren el flag
  `premium`. Al tocar uno bloqueado → "Desbloquear PREMIUM por 🪙500" (descuenta del banco; si falta,
  aviso). `premium` se guarda por jugador en `localStorage` (`pl_<n>_premium`).
- **SALA PRIVADA** (código): crear/unir por código compartido (lo actual, se conserva).
- Reusa `net*` (netStart/netClose/netCount) y los sonidos existentes (sPower/sRight/sWrong).

**Por qué premium importa para "elite":** da una meta aspiracional (gastar monedas en algo social),
diferencia salas, y deja el cableado listo si en el futuro se quiere un pago real o un código VIP.

---

## 6. Opciones necesarias (menú de OPCIONES)
Reusa el estado `options` existente y asegura: **idioma (EN/ZH)**, **gráficos (bajo/medio/alto)**,
**sonido (mute)**, **asistente IA (on/off)**, **voz/pronunciación**, **reducir movimiento** (accesibilidad),
**borrar datos del jugador**. (Pulido incremental sobre lo que ya hay.)

---

## 7. UX / jerarquía / accesibilidad
- **Jerarquía:** 1 acción primaria por pantalla (grande, glow). Secundarias en grilla pareja.
- **Color con significado:** verde=jugar/continuar, cian=social/online, dorado=cosmético/monedas,
  violeta=3D, rojo=salir/peligro.
- **Toque cómodo:** botones ≥40 px, separación ≥8 px, safe-area (notch) respetada.
- **Texto:** `fitFont()` evita desbordes; tamaños 11–24 px según jerarquía.
- **Accesibilidad:** alto contraste, opción de reducir movimiento/gráficos, voz para idioma.

---

## 8. Roadmap por fases
- **F1 (este pase):** documentación (este archivo) + **pantalla de inicio elite** + **salas/servidores premium**. ✅ objetivo del pase.
- **F2:** pulir OPCIONES (accesibilidad), entradas claras a ACADEMIA/minijuegos desde el inicio.
- **F3:** interiores caminables (free-roam) y más trajes temáticos.
- **F4:** persistencia online (perfiles compartidos), códigos VIP reales si se desea.

*Cada fase = incremento que compila/corre, verificado con captura headless del canvas real, commit + push.*
