# 🇪🇸 Crear Parche de Traducción al Español - Pokemon Heart & Soul

## 📋 Requisitos:
1. ✅ Pokemon Emerald (U) ROM original (BPEE.gba)
2. ✅ pokemonHnS_v1.2.1.ups (del repositorio oficial)
3. ✅ Flips (herramienta para crear parches UPS)
4. ✅ Tu código fuente con traducciones (este proyecto)

---

## 🚀 Método 1: Generar Parche UPS (RECOMENDADO)

### Paso A: Crear ROM base en inglés
```powershell
# 1. Descarga pokemonHnS_v1.2.1.ups desde:
# https://github.com/PokemonHnS-Development/pokemonHnS/releases/tag/Release-v1.2.1

# 2. Aplica el parche inglés a Pokemon Emerald (U):
# Usa Rom Patcher JS: https://www.marcrobledo.com/RomPatcher.js/
# - ROM file: Pokemon - Emerald Version (U).gba
# - Patch file: pokemonHnS_v1.2.1.ups
# - Resultado: pokemonHnS_v1.2.1_english.gba
```

### Paso B: Compilar tu versión traducida
```powershell
cd C:\Users\micael\Desktop\pokemonHnS-main

# Opción 1: Compilar en Windows (si funciona)
C:\devkitPro\msys2\usr\bin\make.exe clean
C:\devkitPro\msys2\usr\bin\make.exe -j4 MODERN=1

# Opción 2: Compilar en WSL2 (más confiable)
wsl
sudo apt update
sudo apt install build-essential binutils-arm-none-eabi git libpng-dev
make clean
make -j$(nproc) MODERN=1
exit

# Resultado: pokemonHnS.gba (con traducción española)
```

### Paso C: Crear parche UPS español
```powershell
# 1. Descarga Flips para Windows:
# https://github.com/Alcaro/Flips/releases/download/1.31/flips-windows.zip

# 2. Extrae flips.exe

# 3. Crear el parche UPS:
# OPCIÓN A - Interfaz gráfica:
# - Abre flips.exe
# - Selecciona "Create Patch"
# - Original file: pokemonHnS_v1.2.1_english.gba
# - Modified file: pokemonHnS.gba (tu ROM traducida)
# - Patch: pokemonHnS_v1.2.1_spanish.ups
# - Click "Create"

# OPCIÓN B - Línea de comandos:
.\flips.exe --create --ups pokemonHnS_v1.2.1_english.gba pokemonHnS.gba pokemonHnS_v1.2.1_spanish.ups
```

---

## 🛠️ Método 2: Usar GitHub Actions (Automático)

### Tu workflow ya está configurado para:
1. ✅ Compilar el ROM con tus traducciones
2. ✅ Generar el parche UPS automáticamente
3. ✅ Subir ambos archivos como artefactos

### Para ejecutarlo:
```powershell
# Commit y push los cambios recientes:
git add .
git commit -m "Preparar generacion de parche UPS espanol"
git push
```

### Descargar resultado:
1. Ve a: https://github.com/micaelanon/pokemon_h-s/actions
2. Espera a que termine el workflow (5-10 minutos)
3. Descarga el artefacto "pokemonHnS-traducido-espanol"
4. Extrae el archivo .ups

**⚠️ NOTA:** El workflow necesita el ROM base para crear el parche. Deberás:
- Añadir pokemonHnS_v1.2.1_english.gba al workflow (GitHub Secrets)
- O crear el parche localmente después de compilar

---

## 📦 Método 3: Edición Manual con G3T (Si compilación falla)

Si NO puedes compilar, edita el ROM inglés directamente:

### Herramientas necesarias:
- **G3T (Gen 3 Tools)** - Editor de textos para ROMs GBA
- **Advance Text** - Editor alternativo
- ROM pokemonHnS_v1.2.1_english.gba

### Proceso:
1. Abre pokemonHnS_v1.2.1_english.gba con G3T
2. Busca las secciones de texto (abilities, moves, items, etc.)
3. Copia tus traducciones desde los archivos `.h` de este repo:
   - `include/constants/abilities.h` → Habilidades
   - `src/data/text/move_descriptions.h` → Movimientos
   - `src/data/text/item_descriptions.h` → Objetos
   - `src/data/pokemon/follower_messages.h` → Mensajes seguidores
4. Guarda el ROM editado
5. Crea el parche UPS comparando con el original:
```powershell
.\flips.exe --create --ups pokemonHnS_v1.2.1_english.gba pokemonHnS_v1.2.1_spanish_manual.gba pokemonHnS_v1.2.1_spanish.ups
```

---

## 🎮 Distribución Final

### Archivos a compartir:
1. ✅ `pokemonHnS_v1.2.1_spanish.ups` - Parche de traducción
2. ✅ `README_SPANISH.md` - Instrucciones para usuarios

### Instrucciones para usuarios:
```markdown
# Pokemon Heart & Soul v1.2.1 - Traducción al Español

## Requisitos:
- Pokemon Emerald (U) ROM original
- pokemonHnS_v1.2.1.ups (parche inglés oficial)
- pokemonHnS_v1.2.1_spanish.ups (este parche)
- Rom Patcher JS: https://www.marcrobledo.com/RomPatcher.js/

## Pasos:
1. Aplica el parche inglés sobre Pokemon Emerald (U)
2. Aplica el parche español sobre el resultado del paso 1
3. ¡Disfruta en español!

## Emuladores compatibles:
- PC/Mac: mGBA
- Android: pizzaboy, Lemuroid, Retroarch (core mGBA)
- iOS: Delta, Retroarch (core mGBA)
- R36S: Retroarch (core mGBA)
```

---

## 📊 Estado de la Traducción

### ✅ Completado (95%+):
- Habilidades: 85 nombres + 85 descripciones
- Movimientos: 372 nombres + 370+ descripciones (1843 líneas)
- Objetos: 500+ descripciones (1804 líneas)
- Mensajes seguidores: 300+ mensajes (500+ líneas)
- Clases entrenador: 80+ clases
- Naturalezas: 25 nombres
- Cintas: 70+ descripciones

### ⏳ Pendiente (opcional):
- Diálogos de PNJs (37 archivos .inc)
- Mensajes del Pokénav (match_call_messages.h)

### 📝 Formato aplicado:
- Sin tildes/acentos (á→a, é→e, etc.)
- ñ → n
- "POKeMON" en mayúsculas especiales
- Nombres de especies Pokemon sin traducir

---

## 🐛 Solución de Problemas

### Error: "No se puede compilar"
**Solución:** Usa WSL2 o edita manualmente con G3T (Método 3)

### Error: "Parche UPS inválido"
**Solución:** Verifica que usas el mismo ROM base (Pokemon Emerald U)

### Error: "GitHub Actions falla"
**Solución:** Compila localmente y crea el parche manual

---

## 📞 Soporte

- **Repositorio original:** https://github.com/PokemonHnS-Development/pokemonHnS
- **Tu traducción:** https://github.com/micaelanon/pokemon_h-s
- **Discord oficial:** https://discord.gg/KmuvXJrS9M
