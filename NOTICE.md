# Origen y licencia

## El codigo

Todo lo que hay en `src\` es codigo del clan **SilkSong** de crazyjackel, tomado del tag
`0.4.0` de https://github.com/crazyjackel/SilksongClan, que es exactamente la version con la
que se compilo el DLL original de este mod (comprobado comparando las 99 rutas JSON del
`Plugin.cs` del tag con las cadenas del `Silk_Song_Clan.Plugin.dll` instalado: coinciden una
a una).

Se distribuye bajo **licencia MIT**, y el fichero `LICENSE` de esta carpeta es el original,
con su aviso de copyright intacto:

> Copyright (c) 2025 Monster Train 2 Modding Group

**Ese aviso hay que conservarlo.** Es la unica obligacion que impone la MIT: el aviso de
copyright y el texto de la licencia tienen que viajar con el codigo y con cualquier obra
derivada. A cambio permite usarlo, modificarlo y redistribuirlo, en publico o en privado,
sin pedir permiso.

## Modificaciones propias sobre el codigo

Sobre el tag `0.4.0` hay un solo cambio, en `src\Plugin.cs`: la **lista de ficheros JSON**
que el plugin carga al arrancar. El resto del codigo esta intacto.

La lista ha ido cambiando con el contenido:

| cuando | rutas | que paso |
|---|---|---|
| tag `0.4.0` original | 99 | punto de partida |
| 13-sep, salas y equipo | 103 | +4: dos salas y dos equipos nuevos |
| 13-sep, poda del clan | 80 | -23: pulgas, unidades genericas y Pinata |
| 13-sep, troceo de los HollowWisp | 89 | -1 `hornet_cursed.json`, +10 `hollow_wisp_*.json` |

El bloque de tokens queda asi:

```csharp
//Tokens
"json/units/hollow_wisp_shared.json",
"json/units/hollow_wisp_pyreg.json",
"json/units/hollow_wisp_decay.json",
"json/units/hollow_wisp_melee.json",
"json/units/hollow_wisp_armor.json",
"json/units/hollow_wisp_frost.json",
"json/units/hollow_wisp_regen.json",
"json/units/hollow_wisp_refrm.json",
"json/units/hollow_wisp_gold.json",
"json/units/hollow_wisp_clean.json",
```

## El contenido

Los `json\` y `textures\` de la raiz son **trabajo propio derivado** del contenido original
del clan: unidades rediseñadas, la senda de Lace rehecha, los nueve HollowWisp (ahora en `json\units\hollow_wisp_*.json`), las dos
salas, el equipo y el balanceo. Se mantienen tambien bajo MIT, que es lo coherente con la
base de la que parten.

El arte generado para las cartas nuevas (Bellhart, The Slab, Threefold Pin, Magnetite
Brooch) es de creacion propia.

## Como anadir tu propio copyright

Si quieres constar, la forma habitual es anadir una segunda linea al `LICENSE` **sin tocar
la primera**:

```
Copyright (c) 2025 Monster Train 2 Modding Group
Copyright (c) 2026 David
```

No es obligatorio. Lo que no se puede es sustituir la linea original por la tuya.
