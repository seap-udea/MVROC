# Clasificación visual — periodograms (multiband compare)

Guía para marcar soluciones en
[`pipeline/outputs/periodograms/figures`](https://seap-udea.github.io/gallapp/?repo=seap-udea%2FMVROC&dir=pipeline%2Foutputs%2Fperiodograms%2Ffigures&session=&multi=true&n=0&class=all&likes=all&filter=*.*&grid=true&preview=true&strip=66&persist=session)
con [gallapp](https://seap-udea.github.io/gallapp/) (`multi=true`).

Hay **7775** figuras `*_multiband_photometry_compare.webp` (una por asteroide).
El índice `n` del enlace es la posición en la galería ordenada por nombre de
archivo (0 … 7774).

---

## Qué muestra cada figura

Cada WebP es un **multiband 2-peak compare**:

1. **Panel grande (arriba)** — periodo adoptado por el algoritmo (`selected`).
2. **Paneles pequeños (abajo)** — otros candidatos a dos picos (votados / alias),
   de izquierda a derecha y luego la fila siguiente.

En cada panel: fase en \(2P\), magnitud absoluta \(H\), modelo armónico de dos
picos, \(\chi^2_\nu\), power, amplitud \(A\) y \(A/s\). Un título en **rojo**
suele indicar alias de campaña u otro problema; no lo marques como solución
salvo que el fold sea claramente bueno.

---

## Clases

| Tecla | Clase | Uso |
|------:|-------|-----|
| `1` … `5` | `select-1` … `select-5` | Paneles que **sí** guardas como solución (puedes marcar varios) |
| `j` | `jpl-sbdb` | Coincide / ya contrastado con periodo SBDB (literatura JPL) |
| `g` | `green` | Coincide / ya contrastado con Greenstreet et al. |

**Regla principal:** `select-k` = el panel número **k** de la figura (1 = el de
arriba; 2, 3, … = los de abajo en orden de lectura).

- Marca **todos** los paneles que folden bien (curva coherente, dos máximos
  claros, datos que siguen el modelo).
- Si **ningún** panel sirve, no marques `1`–`5` (déjalo en *No class* para
  soluciones).
- **No borres** `j` / `g` si ya están; son etiquetas de literatura. Tu trabajo
  en el rango asignado es decidir `1`–`5`.

Persistencia: el enlace usa `persist=session` (la sesión del navegador).
Revisa que gallapp esté guardando en este directorio del repo.

---

## Cómo decidir (criterio breve)

Marca un panel cuando:

- Se vean **dos picos** en fase y el modelo negro los describa.
- Los puntos (todas las bandas, con zero-points) no estén dispersos al azar.
- \(A/s\) y power sean razonables frente a paneles peores de la misma figura.
- Un \(\chi^2_\nu\) alto no descarta solo: mira el fold. Un panel con título rojo
  (alias) casi nunca se marca.

No marques cuando:

- El fold es plano, de un solo pico, o el modelo no sigue los datos.
- Solo hay ruido / outliers sin forma de rotación.
- El periodo es un alias de campaña evidente y el fold no convence.

---

## Ejemplos de la clasificación previa

Enlaces con `n` = posición actual en la galería. Ábrelos en gallapp y mira qué
clases ya tienen (`1`–`5`, `j`, `g`).

### Solo panel 1 (`select-1`)

El de arriba folda bien; el/los de abajo no.

| Asteroide | `n` | Enlace |
|-----------|----:|--------|
| 1985 QP5 | 10 | [abrir](https://seap-udea.github.io/gallapp/?repo=seap-udea%2FMVROC&dir=pipeline%2Foutputs%2Fperiodograms%2Ffigures&session=&multi=true&n=10&class=all&likes=all&filter=*.*&grid=true&preview=true&strip=66&persist=session) |
| 1989 SL3 | 17 | [abrir](https://seap-udea.github.io/gallapp/?repo=seap-udea%2FMVROC&dir=pipeline%2Foutputs%2Fperiodograms%2Ffigures&session=&multi=true&n=17&class=all&likes=all&filter=*.*&grid=true&preview=true&strip=66&persist=session) |

### Paneles 1 y 2 (`select-1` + `select-2`)

Arriba y el primer candidato de abajo son soluciones distintas útiles
(p. ej. 1981 US22: \(P\approx 2.94\,\mathrm{h}\) y \(2.77\,\mathrm{h}\)).

| Asteroide | `n` | Enlace |
|-----------|----:|--------|
| 1981 US22 | 8 | [abrir](https://seap-udea.github.io/gallapp/?repo=seap-udea%2FMVROC&dir=pipeline%2Foutputs%2Fperiodograms%2Ffigures&session=&multi=true&n=8&class=all&likes=all&filter=*.*&grid=true&preview=true&strip=66&persist=session) |
| 1993 OX7 | 30 | [abrir](https://seap-udea.github.io/gallapp/?repo=seap-udea%2FMVROC&dir=pipeline%2Foutputs%2Fperiodograms%2Ffigures&session=&multi=true&n=30&class=all&likes=all&filter=*.*&grid=true&preview=true&strip=66&persist=session) |

### Tres paneles (`select-1` + `2` + `3`)

| Asteroide | `n` | Enlace |
|-----------|----:|--------|
| 2003 FY140 | 893 | [abrir](https://seap-udea.github.io/gallapp/?repo=seap-udea%2FMVROC&dir=pipeline%2Foutputs%2Fperiodograms%2Ffigures&session=&multi=true&n=893&class=all&likes=all&filter=*.*&grid=true&preview=true&strip=66&persist=session) |
| 2003 UJ112 | 958 | [abrir](https://seap-udea.github.io/gallapp/?repo=seap-udea%2FMVROC&dir=pipeline%2Foutputs%2Fperiodograms%2Ffigures&session=&multi=true&n=958&class=all&likes=all&filter=*.*&grid=true&preview=true&strip=66&persist=session) |

### Panel 4 (`select-4`)

Poco frecuente: un candidato más abajo en la figura (no el seleccionado).

| Asteroide | `n` | Enlace |
|-----------|----:|--------|
| 2003 TF1 | 948 | [abrir](https://seap-udea.github.io/gallapp/?repo=seap-udea%2FMVROC&dir=pipeline%2Foutputs%2Fperiodograms%2Ffigures&session=&multi=true&n=948&class=all&likes=all&filter=*.*&grid=true&preview=true&strip=66&persist=session) |

### Literatura ya marcada (`j` / `g`)

Solo referencia; en tu rango céntrate en `1`–`5`.

| Etiqueta | Ejemplo | `n` | Enlace |
|----------|---------|----:|--------|
| `jpl-sbdb` (`j`) | 1931 TF2 | 0 | [abrir](https://seap-udea.github.io/gallapp/?repo=seap-udea%2FMVROC&dir=pipeline%2Foutputs%2Fperiodograms%2Ffigures&session=&multi=true&n=0&class=all&likes=all&filter=*.*&grid=true&preview=true&strip=66&persist=session) |
| `green` (`g`) | 2022 CJ2 | 4439 | [abrir](https://seap-udea.github.io/gallapp/?repo=seap-udea%2FMVROC&dir=pipeline%2Foutputs%2Fperiodograms%2Ffigures&session=&multi=true&n=4439&class=all&likes=all&filter=*.*&grid=true&preview=true&strip=66&persist=session) |
| solución + green | 2015 KR298 (`1,2,7`) | 3268 | [abrir](https://seap-udea.github.io/gallapp/?repo=seap-udea%2FMVROC&dir=pipeline%2Foutputs%2Fperiodograms%2Ffigures&session=&multi=true&n=3268&class=all&likes=all&filter=*.*&grid=true&preview=true&strip=66&persist=session) |

Filtrar por clase en gallapp: cambia `class=all` por `class=1`, `class=6`
(`jpl-sbdb`), `class=7` (`green`), etc.

---

## Reparto del trabajo (`n` ≥ 1000)

Los índices **0–999** ya se usaron en la pasada previa. Desde **`n = 1000`**
hasta el final (**`n = 7774`**, 6775 figuras) se reparte entre cuatro personas
(casi 1694 cada una; Angie cierra con 1693).

Plantilla de enlace (cambia solo `n=`):

```text
https://seap-udea.github.io/gallapp/?repo=seap-udea%2FMVROC&dir=pipeline%2Foutputs%2Fperiodograms%2Ffigures&session=&multi=true&n=START&class=all&likes=all&filter=*.*&grid=true&preview=true&strip=66&persist=session
```

| Persona | Rango `n` | Figuras | Primero → último (archivo) | Enlace de inicio |
|---------|-----------|--------:|----------------------------|------------------|
| Nico | 1000 – 2693 | 1694 | `2004_DX24_…` → `2013_NK72_…` | [n=1000](https://seap-udea.github.io/gallapp/?repo=seap-udea%2FMVROC&dir=pipeline%2Foutputs%2Fperiodograms%2Ffigures&session=&multi=true&n=1000&class=all&likes=all&filter=*.*&grid=true&preview=true&strip=66&persist=session) |
| Juanita | 2694 – 4387 | 1694 | `2013_NN2_…` → `2021_RF13_…` | [n=2694](https://seap-udea.github.io/gallapp/?repo=seap-udea%2FMVROC&dir=pipeline%2Foutputs%2Fperiodograms%2Ffigures&session=&multi=true&n=2694&class=all&likes=all&filter=*.*&grid=true&preview=true&strip=66&persist=session) |
| Vale | 4388 – 6081 | 1694 | `2021_RG114_…` → `2025_MD86_…` | [n=4388](https://seap-udea.github.io/gallapp/?repo=seap-udea%2FMVROC&dir=pipeline%2Foutputs%2Fperiodograms%2Ffigures&session=&multi=true&n=4388&class=all&likes=all&filter=*.*&grid=true&preview=true&strip=66&persist=session) |
| Angie | 6082 – 7774 | 1693 | `2025_MD87_…` → `2026_GH4_…` | [n=6082](https://seap-udea.github.io/gallapp/?repo=seap-udea%2FMVROC&dir=pipeline%2Foutputs%2Fperiodograms%2Ffigures&session=&multi=true&n=6082&class=all&likes=all&filter=*.*&grid=true&preview=true&strip=66&persist=session) |

Al terminar un bloque, el `n` del navegador debe quedar en el **último** de tu
rango (o uno más). Si dudas en un objeto, déjalo sin `1`–`5` y anótalo para
revisión conjunta.
