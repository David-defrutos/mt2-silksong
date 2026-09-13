# Compilar el DLL de este mod

> El plugin lleva en `src\Plugin.cs` la **lista de ficheros JSON que carga**. Un JSON nuevo
> no existe para el juego hasta que aparece en esa lista y se recompila.
> Editar un JSON que ya esta en la lista no requiere compilar nada.

## 1. Anadir un JSON nuevo

Abre `src\Plugin.cs`, busca el bloque `c.AddMergedJsonFile(` y mete la ruta en el grupo que
toque. Las rutas son relativas a esta carpeta:

```csharp
//Rooms
"json/rooms/room_bellhart.json",
"json/rooms/room_the_slab.json",
```

## 2. Compilar

### 2.1. En local

Necesitas el **SDK de .NET 9**. El `src\nuget.config` apunta a dos fuentes, y una de ellas
(`nuget.pkg.github.com`) pide credenciales de GitHub aunque el paquete sea publico. Con un
token personal con permiso `read:packages`:

```powershell
cd "C:\Users\david\AppData\Roaming\Thunderstore Mod Manager\DataFolder\MonsterTrain2\profiles\Default\BepInEx\plugins\David-Silksong_Custom"
dotnet nuget update source monster-train-packages -u TU_USUARIO -p TU_TOKEN --store-password-in-clear-text
dotnet restore .\src
dotnet build .\src -c Release --output D:\Juegos\MT2_mod\_dll-build\out
```

### 2.2. En GitHub Actions

Actions resuelve esas credenciales solo, con el `GITHUB_TOKEN` del propio runner, y en repos
publicos es gratis e ilimitado. Haria falta un workflow propio; pidelo cuando lo necesites.

## 3. Instalar el DLL

**La salida del build no puede quedarse dentro de `plugins\`.** BepInEx escanea esa carpeta
en profundidad buscando DLLs, y una copia en `src\bin\` haria que cargase el plugin dos
veces. Por eso el `--output` apunta fuera y luego se copia solo el DLL:

```powershell
$mod = "C:\Users\david\AppData\Roaming\Thunderstore Mod Manager\DataFolder\MonsterTrain2\profiles\Default\BepInEx\plugins\David-Silksong_Custom"

# copia de seguridad del que funciona, antes de nada
Copy-Item "$mod\Silk_Song_Clan.Plugin.dll" "D:\Juegos\MT2_mod\backups\dll-0.4.0-original.dll"

Copy-Item "D:\Juegos\MT2_mod\_dll-build\out\Silk_Song_Clan.Plugin.dll" $mod -Force
```

## 4. Comprobar

Arranca el juego y mira el log:

```powershell
Select-String -Path "$env:USERPROFILE\AppData\LocalLow\Shiny Shoe\MonsterTrain2\Player.log" `
              -Pattern "Bellhart|TheSlab|ThreefoldPin|MagnetiteBrooch"
```

Tienen que salir lineas de `CardDataRegister` y `CardDataFinalizer` para las cuatro cartas.
Si no sale ninguna, el DLL viejo sigue puesto.

## 5. Por si el DLL nuevo rompe algo

```powershell
Copy-Item "D:\Juegos\MT2_mod\backups\dll-0.4.0-original.dll" "$mod\Silk_Song_Clan.Plugin.dll" -Force
```

Vuelves al estado de antes. Los cuatro JSON nuevos se quedan en disco sin cargarse, que es
donde estaban hasta hoy: no molestan.
