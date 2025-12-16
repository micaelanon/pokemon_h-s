# Cómo Generar el Parche UPS de la Traducción al Español

## Opción 1: Compilar y Crear Parche (Si el proyecto compila)

### Requisitos:
- ROM original de Pokemon Emerald (U) - `pokemon_emerald.gba`
- Flips (herramienta para crear parches UPS)

### Pasos:

1. **Compilar el ROM traducido:**
```bash
make -j$(nproc) MODERN=1
```

2. **Descargar Flips:**
   - Windows: https://github.com/Alcaro/Flips/releases/download/1.31/flips-windows.zip
   - Linux: https://github.com/Alcaro/Flips/releases/download/1.31/flips-linux.zip
   - Mac: https://github.com/Alcaro/Flips/releases/download/1.31/flips-macos.zip

3. **Crear el parche UPS:**
```bash
# En Windows (GUI):
# 1. Abre flips.exe
# 2. Selecciona "Create Patch"
# 3. Original file: pokemon_emerald_original.gba
# 4. Modified file: pokemonHnS.gba (compilado)
# 5. Patch: pokemonHnS_spanish.ups

# En Linux/Mac (CLI):
./flips --create --ups pokemon_emerald_original.gba pokemonHnS.gba pokemonHnS_spanish.ups
```

## Opción 2: Usar ROM Pre-compilado (Más fácil)

### Si no puedes compilar:

1. **Descarga el ROM base de pokemonHnS v1.2.1:**
   - Consíguelo del Discord oficial o de releases previas

2. **Descarga tu versión traducida desde GitHub Actions:**
   - Ve a: https://github.com/micaelanon/pokemon_h-s/actions
   - Descarga el artefacto `pokemonHnS-traducido-espanol.gba` (si logró compilar)

3. **Crea el parche UPS comparando ambos:**
```bash
./flips --create --ups pokemonHnS_v1.2.1_original.gba pokemonHnS_traducido.gba pokemonHnS_spanish_v1.2.1.ups
```

## Opción 3: Editar ROM Pre-compilado Manualmente

Si la compilación falla, puedes:

1. **Descargar pokemonHnS v1.2.1 compilado**
2. **Usar herramientas de ROM hacking:**
   - G3T (Gen 3 Tools) para editar textos
   - HxD (editor hexadecimal) para cambios específicos
   
3. **Importar tus traducciones manualmente:**
   - Abre los archivos `.h` de este repo
   - Copia los textos traducidos
   - Pégalos en el ROM usando G3T

4. **Genera el UPS comparando:**
```bash
./flips --create --ups pokemonHnS_v1.2.1_original.gba pokemonHnS_v1.2.1_spanish.gba pokemonHnS_spanish.ups
```

## Distribución del Parche

Una vez tengas el archivo `.ups`:

1. **Sube el parche a GitHub Releases:**
   - Ve a tu repositorio: https://github.com/micaelanon/pokemon_h-s
   - Click en "Releases" > "Create a new release"
   - Sube `pokemonHnS_spanish.ups`

2. **Instrucciones para usuarios:**

```markdown
# Parche de Traducción al Español - Pokemon Heart & Soul

## Requisitos:
- ROM original de Pokemon Emerald (U) - versión USA
- pokemonHnS v1.2.1 (aplicar primero el parche inglés)
- Rom Patcher JS: https://www.marcrobledo.com/RomPatcher.js/

## Pasos:
1. Descarga el parche original pokemonHnS_v1.2.1.ups
2. Aplica el parche inglés sobre Pokemon Emerald (U)
3. Descarga pokemonHnS_spanish.ups (este repositorio)
4. Aplica el parche español sobre el ROM del paso 2
5. ¡Juega en español!
```

## Archivos Traducidos en Este Repo

✅ **Completado al 95%+:**
- `include/constants/abilities.h` - Nombres y descripciones de habilidades
- `include/constants/moves.h` - Nombres de movimientos
- `src/data/text/move_descriptions.h` - Descripciones de movimientos (1843 líneas)
- `src/data/text/item_descriptions.h` - Descripciones de objetos (1804 líneas)
- `src/data/pokemon/follower_messages.h` - Mensajes de seguidores (500+ líneas)
- `src/data/text/nature_names.h` - Nombres de naturalezas
- `include/constants/ribbon_descriptions.h` - Descripciones de cintas

**Formato:** Sin tildes/acentos, ñ→n, "POKeMON" format

---

## Problemas Conocidos

- El proyecto tiene errores de compilación con el compilador moderno (gcc 15.1.0)
- Requiere correcciones en varios archivos `.c` para compatibilidad C99
- La opción 3 (edición manual) es la más confiable actualmente
