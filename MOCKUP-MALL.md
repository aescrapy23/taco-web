# TACO CITY — Mockup del Mall y las Tiendas (inicio a fin)

Mockups en texto/ASCII del flujo completo: desde que arrancás hasta que entrás a una tienda y volvés.
Sirve como guía de diseño para programadores/artistas. Todo es canvas 2D top-down, vectorial.

---

## 1. Flujo general (navegación)

```
TÍTULO ──► JUGAR ──► CIUDAD (calle) ──► [tocás puerta de tienda] ──► CENTRO COMERCIAL (mall)
   ▲                                                                      │
   │                                                                      ├─► escalera ▲▼ : PISO 1..4
   │                                                                      ├─► tocás una ESTACIÓN ──► menú de opciones
   │                                                                      ├─► tocás una VIDRIERA ──► TIENDA (entrás y caminás)
   └──────────────────────── SALIDA ◄────────────────────────────────────┘         │
                                                                          [producto] ─► compra / abre vestuario / minijuego
                                                                          [SALIDA]   ─► vuelve al mall
```

Estados: `title · play · interior(mall) · store(tienda) · roulette · uno · memory · cine · wardrobe · ...`

---

## 2. Mall — vista de un piso (planta baja)

```
┌───────────────────────────────────────────────────────── CENTRO COMERCIAL · PLANTA BAJA ──┐
│ [▲][▼] PISO 1/4    ╔═══╗╔═══╗╔═══╗   ┌ESCALERA┐   ╔═══╗╔═══╗╔═══╗            [ SALIR ]      │  ← claraboya + balcón (baranda)
│  FARMACIA  GYM   SUPER  PANADERIA   │▲ up │▼ dn│  LIBRERIA  BANCO  ...                       │  ← vidrieras (locales con nombre,
│  [vidriera][vidriera][vidriera]     │escalones│  [vidriera][vidriera]   "ENTRAR"            │     toldo, maniquí, productos)
│ ································· piso embaldosado con perspectiva ····························│
│        🪴            👤 (gente)        ╔════════╗                     👤            $        │
│                                       ║ PODERES ║                                          │  ← estaciones (kioscos):
│    ╔═══════╗                          ╚════════╝                    ╔════════╗             │     SALUD · PODERES · COMIDA
│    ║ SALUD ║          $                                             ║ COMIDA ║   $         │     (tocás → menú de opciones)
│    ╚═══════╝                                  🌮(taco)                ╚════════╝            │
│   🪴   [banco]                       ▼ SALIDA ▼                       [banco]   🪴          │  ← SALIDA abajo-centro (a la calle)
└───────────────────────────────────────────────────────────────────────────────────────────┘
```

**Pisos:**
- **PISO 1 · Planta Baja** → Salud · Poderes · Comida (locales: Farmacia, Gym, Súper, Panadería, Kiosco, Librería, Banco)
- **PISO 2 · Moda** → Vestuario · Accesorios/Cascos · Vehículos (locales: Moda, Zapatos, Joyas, Óptica, Perfume…)
- **PISO 3 · Diversión** → Ruleta · Juegos (memoria) · Casino (UNO) (locales: Arcade, Juguetes, Cómics, Música, Tech…)
- **PISO 4 · Cine y Terraza** → Cine · Cafetería · Mirador (locales: Café, Helados, Pizza, Sushi, Tacos, Jugos…)

**Interacciones:** caminás con el stick · tocás una **estación** (popup de opciones) · tocás una **vidriera** (entrás a la tienda) · escalera mecánica central o botones ▲▼ para cambiar de piso · juntás monedas del piso · **SALIDA** vuelve a la calle.

---

## 3. Tienda — vista interior (al entrar a una vidriera)

```
┌──────────────────────────── NOMBRE DEL LOCAL (ej. JUGUETES) ──────────── 9 mon ──[AL MALL]──┐
│  ▭▭▭▭▭▭  estantería con productos de colores  ▭▭▭▭▭▭▭▭▭▭▭▭▭▭▭▭▭▭▭▭                         │  ← pared con 3 estantes
│  ▭▭▭▭▭▭                                        ▭▭▭▭▭▭▭▭▭▭▭▭▭▭▭▭▭▭▭▭                         │
│  ┌mostrador┐ 🌮(cajero)        piso con perspectiva                                          │
│ ···································································································│
│              ╔═══╗            ╔═══╗            ╔═══╗                        $                 │  ← productos en pedestales:
│              ║🎲 ║            ║🎲 ║            ║🎲 ║                                          │     pisás uno y se compra
│              RULETA            UNO            MEMORIA          $                              │     (o abre vestuario/minijuego)
│      $                                                                                       │
│                                  🌮(vos)                                                     │
│                              ▼ SALIDA ▼  (volver al mall)                                    │
└─────────────────────────────────────────────────────────────────────────────────────────────┘
```

**Tipos de tienda (según el nombre del cartel):**
- **MODA / Zapatos / Joyas / Óptica / Perfume / Bolsos / Deportes** → productos: ROPA, ACCESORIOS, VEHÍCULOS (abren el vestuario).
- **ARCADE / Juguetes / Cómics / Música / Tech / VR / Cine** → productos: RULETA, UNO, MEMORIA (minijuegos).
- **Resto (Farmacia/Súper/Café/Helados/Pizza/…)** → productos: BEBIDA (cura vida), ESCUDO, SNACK (rápido). Se compran con monedas.

**Flujo dentro de la tienda:** entrás → caminás → **pisás un producto** (compra con feedback “LISTO!”/“te faltan monedas”, o abre vestuario/minijuego) → juntás monedas → **SALIDA** te devuelve al mall (al mismo piso).

---

## 4. Anidamiento (3 niveles de interior)

```
CALLE (ciudad 3D) ─► MALL (4 pisos, roam) ─► TIENDA (roam) ─► [vestuario / minijuego / compra]
   exit ◄─────────────  SALIDA ◄────────────  SALIDA ◄──────────  VOLVER
```

---

## 5. Próximo (modo construcción — mockup objetivo)

```
TERRENO vacío  ─► [CONTRATAR cuadrilla 🦺]  ─► [ELEGIR diseño: casa/tienda/torre]
   │                                              │
   ├─ EPP/OSHA obligatorio (casco, chaleco, conos, cinta)                   
   ├─ ETAPAS: cimientos → estructura → fachada → techo  (barra de progreso, obreros animan)
   └─ FIN ─► el edificio queda en la ciudad y se puede ENTRAR (otro local del mall)
```

---
*Acompaña a `index.html`, `PROMPTS-DESARROLLO.md`. Refleja el juego en su versión actual + objetivo.*
