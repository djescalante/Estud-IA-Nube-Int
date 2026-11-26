# Fallas para provocar en el CI

Cada falla es **un cambio pequeño** que haces en tu fork, directamente en GitHub
(abre el archivo → lápiz ✏️ → cambia → *Commit changes*). Después mira la pestaña
**Actions** y responde:

1. ¿Qué job quedó en rojo?
2. ¿Cuál es el **primer** mensaje útil del log?
3. ¿El problema es del **entorno** (falta algo para correr) o del **comportamiento**
   (la aplicación hace algo distinto de lo esperado)?

Al terminar, **deshaz el cambio** (vuelve a editar y deja el valor original) y comprueba
que todo vuelve a verde.

| # | Archivo | Cambio |
| --- | --- | --- |
| 01 | `app/app.py` | En la línea de `DIAS_VIGENCIA`, cambia `"90"` por `"900"` |
| 02 | `app/requirements.txt` | Borra la línea `Flask==3.1.3` |
| 03 | `Dockerfile` | En la última línea, cambia `0.0.0.0` por `127.0.0.1` |
| 04 | `.github/workflows/clase-04-villa-nube.yml` | Haz la falla 01 y además cambia `run: pytest -v` por <code>run: pytest -v &#124;&#124; true</code> |

La falla 04 es distinta: mira el color del resultado y lee el log completo.
¿Qué te dice eso de un check verde?

¿No puedes usar GitHub hoy? Los logs de estas fallas están guardados en `ci/logs/`.
