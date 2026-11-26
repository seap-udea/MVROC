# Clasificación visual — periodograms (multiband compare)

Guía para marcar **soluciones** en la galería de figuras
`*_multiband_photometry_compare.webp` (7775 asteroides) con la
[Gallery App](https://seap-udea.github.io/gallapp/).

Abre tu enlace de inicio (tabla siguiente) y trabaja en el rango asignado.

---

## Reparto del trabajo (desde la figura 1000)

Los índices **0–999** ya se revisaron. Desde **1000** hasta el final se reparte
así (abre el enlace de tu fila y avanza con → hasta cubrir tu rango):

| Persona | Rango (índice) | Figuras | Enlace de inicio |
|---------|----------------|--------:|------------------|
| Nico | 1000 – 2693 | 1694 | [Empezar](https://seap-udea.github.io/gallapp/?repo=seap-udea%2FMVROC&dir=pipeline%2Foutputs%2Fperiodograms%2Ffigures&session=&multi=true&n=1000&class=all&likes=all&filter=*.*&grid=true&preview=true&strip=66&persist=session) |
| Juanita | 2694 – 4387 | 1694 | [Empezar](https://seap-udea.github.io/gallapp/?repo=seap-udea%2FMVROC&dir=pipeline%2Foutputs%2Fperiodograms%2Ffigures&session=&multi=true&n=2694&class=all&likes=all&filter=*.*&grid=true&preview=true&strip=66&persist=session) |
| Vale | 4388 – 6081 | 1694 | [Empezar](https://seap-udea.github.io/gallapp/?repo=seap-udea%2FMVROC&dir=pipeline%2Foutputs%2Fperiodograms%2Ffigures&session=&multi=true&n=4388&class=all&likes=all&filter=*.*&grid=true&preview=true&strip=66&persist=session) |
| Angie | 6082 – 7774 | 1693 | [Empezar](https://seap-udea.github.io/gallapp/?repo=seap-udea%2FMVROC&dir=pipeline%2Foutputs%2Fperiodograms%2Ffigures&session=&multi=true&n=6082&class=all&likes=all&filter=*.*&grid=true&preview=true&strip=66&persist=session) |

Si dudas en un objeto, déjalo sin `1`–`5` y anótalo para revisión conjunta.
Al cerrar, **Export sidecars**.

---

## Qué mirar en cada figura

- El panel de arriba es el candidato principal; los de abajo son alternativas.
- Marca un panel cuando el **patrón de brillo se repite** a lo largo de la fase
  (dos máximos típicos de un elipsoide) y los puntos de las bandas siguen esa
  forma.
- **Si la curva armónica negra no ajusta del todo, pero ves el patrón
  repetirse, márcalo igual.** El modelo es una guía; el ojo manda.
- Si **ningún** panel sirve, no marques `1`–`5`.

---

## Cómo es la página

![Pantalla de la Gallery App (MVROC)](examples/MVROC-classification.png)

Lectura rápida del pantallazo:

1. **Arriba** — carpeta del repo, filtro y contador (`7775 images · … classified`).
2. **Navegación** — `«` `<` casilla `n / 7775` `>` `»`, o teclas **←** / **→**,
   para cambiar de asteroide.
3. **Filtros de clase** — *All*, *No class*, *Classified*, `select-1`…`select-5`,
   `jpl-sbdb (j)`, `green (g)`. *Classified* muestra todas las ya etiquetadas;
   los demás radios filtran por una sola clase.
4. **Figura central** — el compare multiband. Arriba el panel **1** (solución
   *selected* del algoritmo); abajo los paneles **2**, **3**, … en orden.
5. **Badge** (esquina de la figura) — clases ya puestas en esa imagen
   (p. ej. `1, 2, 3, j`).
6. **Abajo** — botones de la imagen (*View*, *Download*, …) y, importante,
   **Export sidecars** / **Import sidecars** y *Download classified*.

A la derecha del listado de clases suele aparecer el recordatorio:

> Use ← → to browse · Shift+ toggles classes · Shift+0 clears

---

## Teclas y navegación

| Acción | Cómo |
|--------|------|
| Asteroide anterior / siguiente | **←** / **→** (o botones `<` `>`) |
| Ir al primero / último | `«` / `»` |
| Marcar o quitar una clase | **Shift + tecla de la clase** (toggle) |
| Quitar todas las clases de la imagen | **Shift + 0** |
| Filtrar la galería por una clase | clic en el radio *select-1*, *green*, etc. |

### Clases de solución (tu trabajo principal)

| Shift + | Clase | Significado |
|--------:|-------|-------------|
| `1` | select-1 | Panel grande de arriba |
| `2` | select-2 | Primer panel pequeño (abajo, izq.) |
| `3` | select-3 | Siguiente panel |
| `4` | select-4 | Siguiente |
| `5` | select-5 | Siguiente |

Puedes marcar **varios** paneles si varios pliegan bien.

**Toggle:** si pulsas otra vez **Shift + la misma tecla**, **se quita** esa
clase de la imagen. No hace falta *Remove classification* para un solo tag.

### Clases de literatura (ya rellenadas en muchos casos)

| Shift + | Clase | Uso |
|--------:|-------|-----|
| `j` | jpl-sbdb | Periodo publicado en SBDB / JPL |
| `g` | green | Periodo en Greenstreet et al. |

`j` y `g` **no** significan “buen folding”. Solo dicen que ese asteroide tiene
un periodo en la literatura. En tu rango **no las borres** si ya están; tu
trabajo es decidir `1`–`5` mirando los paneles.

---

## Guardar el trabajo

- Si **siempre usas el mismo navegador** en el mismo equipo, gallapp **guarda
  la clasificación en la sesión** y al volver deberías ver tus marcas.
- Si vas a **cambiar de navegador, de máquina o limpiar datos del sitio**,
  antes de irte pulsa **Export sidecars**: descarga un **ZIP** con las
  selecciones.
- En el otro navegador (o tras reiniciar), abre la misma galería y pulsa
  **Import sidecars** con ese ZIP para recuperar las marcas.
- Cuando termines un bloque (o el día), exporta otra vez por si acaso.
  *Download classified (.zip)* también empaqueta lo clasificado para revisión.

---

## Conjunto de entrenamiento

Antes de clasificar tu rango, mira ejemplos **ya etiquetados** para calibrar el
ojo. En gallapp usa el filtro **Classified**, o abre:

[Todas las imágenes clasificadas](https://seap-udea.github.io/gallapp/?repo=seap-udea%2FMVROC&dir=pipeline%2Foutputs%2Fperiodograms%2Ffigures&session=&multi=true&n=0&class=x&likes=all&filter=*.*&grid=true&preview=true&strip=66&persist=session)
(`class=x`).

Ese conjunto mezcla dos cosas distintas:

1. **Soluciones visuales** — llevan `select-1`…`select-5` porque alguien juzgó
   que uno o más paneles pliegan bien (a veces junto con `j` o `g`).
2. **Solo literatura** — llevan `j` y/o `g` **sin** `1`–`5`. Son curvas con
   periodo publicado, incluidas para contraste; **muchas no están bien
   folded** con nuestros datos. No las tomes como modelo de “qué marcar”.

Al entrenar el ojo, prioriza las que tienen `1`–`5`. Filtra por `select-1` (u
otra select) si quieres ver solo folds aceptados. Usa `j` / `g` para ver cómo
se ve la literatura cuando el folding falla o es dudoso.

Hay **distintos tipos de curva** entre las que sí llevan `1`–`5`. En muchos de
esos casos **sí** conviene marcar un panel aunque el aspecto no sea “perfecto”.

### Submuestreado

Pocas observaciones o muestreo irregular.

![1977 UO5 — submuestreado](examples/1977_UO5_multiband_photometry_compare.webp)

### Fold limpio

Poca dispersión; los puntos siguen de cerca el modelo de dos picos.

![1981 US22 — fold limpio](examples/1981_US22_multiband_photometry_compare.webp)

![2025 MM81 — fold limpio](examples/2025_MM81_multiband_photometry_compare.webp)

### Disperso

Dispersión alta (con o sin errores grandes); la forma de rotación sigue
legible.

![1989 SL3 — errores altos y dispersión](examples/1989_SL3_multiband_photometry_compare.webp)

![1998 FN74 — errores bajos pero dispersión](examples/1998_FN74_multiband_photometry_compare.webp)

### Baja amplitud

Amplitud pequeña; la rotación aún se intuye.

![1993 OX7 — baja amplitud](examples/1993_OX7_multiband_photometry_compare.webp)

### Contaminado

Algunos puntos se apartan mucho del fold principal.

![1998 BG25 — contaminado](examples/1998_BG25_multiband_photometry_compare.webp)

### Fase incompleta

Solo se cubre un tramo de la rotación (huecos grandes en fase).

![1998 FH23 — fase incompleta](examples/1998_FH23_multiband_photometry_compare.webp)

![2025 MV38 — fase incompleta](examples/2025_MV38_multiband_photometry_compare.webp)

### Mejor folding no es el panel principal

El candidato de arriba no es el mejor; marca el panel de abajo que sí pliega
bien (p. ej. `select-2`…`select-5`).

![2025 MV31 — mejor folding no es el principal](examples/2025_MV31_multiband_photometry_compare.webp)

### En la literatura (`j` / `g`), pero el folding es fallido

Parte del conjunto de entrenamiento son objetos **solo** con `j` o `g` (sin
`1`–`5`): hay periodo en SBDB/Greenstreet, pero con nuestra fotometría **ningún**
panel pliega bien. Eso es normal. **No marques `1`–`5` solo porque veas `j` o
`g`.** La etiqueta de literatura no sustituye el folding.

![2025 MN45 — literatura, folding fallido](examples/2025_MN45_multiband_photometry_compare.webp)

![2025 MK41 — literatura, folding fallido](examples/2025_MK41_multiband_photometry_compare.webp)

### Periodos largos (clusters por días)

La fase se agrupa en “paquetes” por noche/día; aún así el patrón puede ser
válido.

![2016 RP29 — periodo largo / clusters](examples/2016_RP29_multiband_photometry_compare.webp)

### Ajuste armónico malo, pero se ve otra forma de curva

La curva negra no ajusta, pero hay una forma repetible distinta del armónico
clásico → puede marcarse si el patrón es claro.

![2025 MA19 — patrón claro aunque el armónico no sea perfecto](examples/2025_MA19_multiband_photometry_compare.webp)

### Cuándo **no** clasificar (`1`–`5`)

- El ajuste es muy poco armónico / la figura se ve casi **sinusoidal** sin el
  patrón de dos picos:

![2004 XW104 — no clasificar (poco armónico / sinusoidal)](examples/2004_XW104_multiband_photometry_compare.webp)

- La amplitud es **demasiado** baja para confiar en un periodo:

![2004 NZ8 — no clasificar (amplitud demasiado baja)](examples/2004_NZ8_multiband_photometry_compare.webp)
