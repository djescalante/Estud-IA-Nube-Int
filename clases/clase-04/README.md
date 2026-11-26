# Clase 4 · Guía del estudiante y ejercicios

Integración continua y validación de cambios · Nube Intermedio · Semana 2. No necesitas experiencia previa con GitHub Actions: vamos paso a paso y casi todo se hace en el navegador.

**Los ejercicios de la Clase 4** (cada clase numera sus ejercicios del 1 al 9: el «Ejercicio 7» de la Clase 3 no es el mismo de la Clase 4)

| # | Ejercicio | Modo | Tiempo |
| --- | --- | --- | --- |
| **1** | [¿Qué debería revisar la máquina?](#ejercicio-1--qué-debería-revisar-la-máquina) | En parejas · apertura | 5 min |
| **2** | [Sigue conmigo: tu primera ejecución](#ejercicio-2--sigue-conmigo-tu-primera-ejecución) | Individual, al mismo tiempo que el profesor | 10 min |
| **3** | [Rompe y arregla](#ejercicio-3--rompe-y-arregla) | En equipo · práctica guiada, parte A | 15 min |
| **4** | [Completa el workflow](#ejercicio-4--completa-el-workflow) | En equipo · práctica guiada, parte B | 15 min |
| **5** | [¿Entorno o comportamiento?](#ejercicio-5--entorno-o-comportamiento) | Votación en el chat | 4 min |
| **6** | [Predice antes de ver](#ejercicio-6--predice-antes-de-ver) | Individual · durante la explicación | 6 min |
| **7** | [Tu proyecto con CI](#ejercicio-7--tu-proyecto-con-ci) | Individual o con tu equipo de proyecto | 45 min |
| **8** | [¿Qué te protege?](#ejercicio-8--qué-te-protege) | En parejas | 25 min |
| **9** | [Exit ticket y preparación para la Clase 5](#ejercicio-9--exit-ticket-y-preparación-para-la-clase-5) | Individual | 5 min |

## Antes de empezar

En la Clase 3 un compañero encendió tu proyecto siguiendo tu README. Hoy ese trabajo lo hace una máquina: cada vez que cambias el código, GitHub construye tu proyecto, lo enciende y corre tus pruebas. Si algo se rompe, te avisa con un check rojo y un log que dice dónde.

**Te llevas:** un workflow de GitHub Actions en tu repositorio, una ejecución en verde y otra en rojo provocada a propósito, y una sección «Cómo se valida» en tu README.

**Cómo vamos a trabajar.** Igual que en la Clase 3: primero lo hace el profesor, luego lo haces con él y después en tu proyecto. Hoy casi todo se hace en el navegador, en GitHub. Si algo falla, copia en el chat el nombre del paso en rojo y la primera línea de error.

**Alistamiento (antes de la clase)**

- [ ] Puedes entrar a tu cuenta de GitHub.
- [ ] Tu `Dockerfile` y tu `README.md` de la Clase 3 están en tu repositorio de GitHub.
- [ ] Tienes a mano tus dos pruebas «Si hago ___, debo ver ___» de la Clase 3.
- [ ] Viste Platzi M1 · CI/CD, o al menos su primera parte.

**¿No tienes un proyecto propio o no lo subiste a GitHub?** No pasa nada: el repositorio del curso trae proyectos de práctica en la carpeta `proyectos/`. Eliges uno en el ejercicio 7 y lo usas como si fuera tuyo.

**Las 8 palabras de hoy**

| Palabra | Qué significa | En Villa Nube |
| --- | --- | --- |
| Integración continua (CI) | Que una máquina pruebe el proyecto cada vez que alguien lo cambia | Cada cambio en `clases/clase-04/villa-nube` se prueba solo |
| Workflow | Archivo con la receta de lo que la máquina debe hacer | `.github/workflows/clase-04-villa-nube.yml` |
| Disparador | Lo que hace arrancar el workflow | `on: push` (cuando subes un cambio) |
| Job | Un grupo de pasos que corre en una misma máquina | «Pruebas del código» e «Imagen y prueba de humo» |
| Paso (step) | Una sola acción dentro de un job | `pytest -v` |
| Runner | La máquina limpia que GitHub presta para cada ejecución | `ubuntu-latest` |
| Log | Lo que escribió cada paso mientras corría | El texto que ves al abrir un paso |
| Check | El resultado final: verde (pasó) o rojo (falló) | ✅ o ❌ junto a cada commit |

**El laboratorio.** Es la misma Villa Nube de la Clase 3, en la carpeta `clases/clase-04/villa-nube` del repositorio del curso, github.com/dlemusg/Estud-IA-Nube-Int. El workflow que la prueba está en `.github/workflows/clase-04-villa-nube.yml`, en la raíz del repositorio. Es un caso inventado: no uses datos personales reales ni claves de tu trabajo.

## Ejercicio 1 · ¿Qué debería revisar la máquina?

*En parejas · apertura · 5 minutos.*

**Paso 1.** Mira tus dos pruebas de la Clase 3. Elige la que más te importaría que se comprobara sola **cada vez** que cambias el código.

La prueba que quiero automatizar: ______________________

**Paso 2.** Completa: «Si alguien rompe ______________________, esta prueba lo detecta porque ______________________».

Ejemplo con Villa Nube: «Si alguien cambia la regla de los 90 días, la prueba "un documento vencido se rechaza" lo detecta porque la solicitud ya no recibe el error 422».

**¿Está bien elegida?** Si la prueba puede quedar en rojo cuando el comportamiento cambia, sí. «Que el pipeline salga verde» no es una prueba: es un resultado.

## Ejercicio 2 · Sigue conmigo: tu primera ejecución

*Individual, al mismo tiempo que el profesor · 10 minutos.* Todo en el navegador. Marca la casilla cuando veas el resultado.

**Paso 1 · Haz tu copia del repositorio (fork).** Entra a github.com/dlemusg/Estud-IA-Nube-Int y pulsa **Fork** → **Create fork**.

- [ ] Estoy en `github.com/MI-USUARIO/Estud-IA-Nube-Int`.

**Paso 2 · Habilita Actions.** En tu fork, abre la pestaña **Actions** y pulsa el botón verde **I understand my workflows, go ahead and enable them**.

- [ ] Veo a la izquierda la lista de workflows, con **Clase 4 · Villa Nube CI**.

**Paso 3 · Corre el workflow a mano.** Elige **Clase 4 · Villa Nube CI** → **Run workflow** → **Run workflow**.

- [ ] Aparece una ejecución con un círculo amarillo que gira y, en uno o dos minutos, un ✅ verde.

**Paso 4 · Lee el log.** Haz clic en la ejecución, luego en el job **Pruebas del código** y abre el paso **Correr las pruebas**.

- [ ] Leo `5 passed`.
- [ ] En el job **Imagen y prueba de humo**, el paso **Prueba de humo** dice `5 pasaron, 0 fallaron`.

Qué pasó: GitHub prestó una máquina Linux limpia, descargó el código, instaló Python, corrió las pruebas y, como pasaron, construyó la imagen, la encendió y repitió las pruebas de la Clase 3 contra el contenedor. Es tu arranque a ciegas, hecho por una máquina.

Si algo no salió, escribe en el chat en qué paso te quedaste y qué ves en pantalla.

## Ejercicio 3 · Rompe y arregla

*En equipo · práctica guiada, parte A · 15 minutos.* Una persona comparte pantalla y las demás repiten en su fork. Vas a dejar evidencia de **un caso correcto y uno fallido**.

**Paso 1 · Lee el workflow** (en tu fork, abre `.github/workflows/clase-04-villa-nube.yml`). Esta es su versión corta, traducida:

| Línea | En palabras |
| --- | --- |
| `on: push` con `paths` | Corre cuando subo un cambio dentro de la carpeta de Villa Nube |
| `workflow_dispatch` | Agrega el botón «Run workflow» |
| `permissions: contents: read` | El workflow solo puede leer el repositorio |
| `runs-on: ubuntu-latest` | Cada job corre en una máquina Linux limpia |
| `uses: actions/checkout@v6` | Descarga el código del repositorio |
| `uses: actions/setup-python@v6` | Instala Python |
| `run: pytest -v` | Corre las pruebas del código |
| `needs: pruebas` | El job de la imagen solo corre si las pruebas pasaron |
| `if: failure()` | Este paso solo corre si algo falló antes |

**Paso 2 · Rompe la regla del negocio.** En tu fork abre `clases/clase-04/villa-nube/app/app.py`, pulsa el lápiz ✏️ y en la línea de `DIAS_VIGENCIA` cambia `"90"` por `"900"`. Pulsa **Commit changes** → **Commit changes**.

- [ ] En **Actions** aparece una ejecución nueva que termina en ❌ rojo.

**Paso 3 · Encuentra el primer error útil.** Abre la ejecución roja → job **Pruebas del código** → paso **Correr las pruebas**. Busca la línea que empieza con `FAILED` y la que empieza con `E`.

| Pregunta | Respuesta |
| --- | --- |
| ¿Qué job quedó en rojo? | |
| ¿Qué prueba falló? | |
| ¿Qué esperaba la prueba y qué recibió? | |
| ¿Qué pasó con el job «Imagen y prueba de humo»? | |

**Paso 4 · Arréglalo.** Vuelve a editar `app/app.py` y deja `"90"`. Haz commit.

- [ ] La ejecución nueva termina en ✅ verde.
- [ ] Copio en mis notas el enlace de la ejecución roja y el de la verde: son mi evidencia.

**Checkpoint (minuto 12).** Escriban en el chat general «Sala N: rojo y verde» o el paso donde se quedaron.

## Ejercicio 4 · Completa el workflow

*En equipo · práctica guiada, parte B · 15 minutos.* Abre `clases/clase-04/villa-nube/ci/plantilla-ci.yml` y completa cada `___` con una palabra del banco. Cada palabra se usa una vez.

**Banco de palabras:** `push` · `ubuntu-latest` · `actions/checkout@v6` · `"3.12"` · `pytest -v` · `docker build` · `pruebas`

```yaml
name: Mi primer CI

# 1. ¿Cuándo corre? Cada vez que subo un cambio
on:
  ___:
    paths:
      - "clases/clase-04/villa-nube/**"

permissions:
  contents: read

defaults:
  run:
    working-directory: clases/clase-04/villa-nube

jobs:
  pruebas:
    # 2. ¿En qué máquina corre? Una Linux que presta GitHub
    runs-on: ___
    steps:
      # 3. Primero hay que descargar el código
      - uses: ___

      # 4. ¿Qué versión de Python instalamos?
      - uses: actions/setup-python@v6
        with:
          python-version: ___

      - run: pip install -r app/requirements.txt -r requirements-dev.txt

      # 5. ¿Qué comando corre las pruebas?
      - run: ___

  imagen:
    # 6. Este job espera a que otro termine en verde. ¿Cuál?
    needs: ___
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v6

      # 7. ¿Qué comando construye la imagen?
      - run: ___ -t villa-nube/tramites:${{ github.sha }} .
```

**Para probarlo:** en tu fork, **Add file** → **Create new file**, escribe el nombre `.github/workflows/mi-ci.yml`, pega tu versión completa y haz commit. Luego cambia cualquier archivo de la carpeta de Villa Nube (por ejemplo, agrega una línea al README) para dispararlo.

- [ ] **Mi primer CI** aparece en Actions y termina en verde.

**Cuidado con la sangría.** En YAML los espacios definen qué va dentro de qué. Si GitHub muestra «Invalid workflow file», revisa que cada línea tenga los mismos espacios que en la plantilla.

**Dos preguntas para el equipo**

1. ¿Por qué el job `imagen` tiene `needs: pruebas`? *Pista: piensa en qué pasaría si las pruebas fallan y aun así se construye la imagen.*
2. ¿Por qué la etiqueta de la imagen es `${{ github.sha }}` y no `latest`?

## Ejercicio 5 · ¿Entorno o comportamiento?

*Votación en el chat · 4 minutos.* Para cada log, escribe **E** si el problema es del **entorno** (falta algo para poder correr) o **C** si es del **comportamiento** (la aplicación corre, pero hace algo distinto de lo esperado). Los logs completos están en `ci/logs/`.

| # | Lo que dice el log | E o C |
| --- | --- | --- |
| 1 | `FAILED test_documento_vencido_se_rechaza - assert 201 == 422` | |
| 2 | `pytest: command not found` | |
| 3 | `ModuleNotFoundError: No module named 'flask'` | |
| 4 | `/salud → 000` y en los logs del contenedor: `Listening at: http://127.0.0.1:8080` | |

**Cómo leer un log rojo, en tres pasos**

1. Busca el **primer** paso con ❌: los de después suelen fallar por culpa de ese.
2. Dentro del paso, busca las líneas con `Error`, `FAILED` o `E `.
3. Pregúntate: ¿faltaba algo para correr (entorno) o corrió y respondió distinto (comportamiento)?

## Ejercicio 6 · Predice antes de ver

*Individual · durante la explicación · 6 minutos.* Escribe tu predicción antes de que el profesor muestre el resultado. Equivocarse es parte del ejercicio.

**Verde y rojo**

| Pregunta | Mi predicción | Lo que pasó |
| --- | --- | --- |
| Si el job «Pruebas del código» falla, ¿corre el job «Imagen y prueba de humo»? | | |
| Cambio `run: pytest -v` por <code>run: pytest -v &#124;&#124; true</code> y rompo la regla. ¿De qué color queda? | | |
| Cambio solo el README de la raíz del repositorio. ¿Corre el workflow de Villa Nube? | | |
| El workflow quedó en verde. ¿Villa Nube ya está publicada en internet? | | |

Regla corta: **un check verde solo garantiza lo que realmente se probó.** Si un paso no corre o su error se ignora, el verde no dice nada de eso.

**¿Dónde vive cada dato?**

| Dato | ¿Dónde va? |
| --- | --- |
| La clave de la base de datos de producción | |
| El número de días de vigencia del documento | |
| La clave de tu base de datos local para practicar | |

Opciones: **secreto de GitHub** (Settings → Secrets and variables → Actions → *Secrets*), **variable de GitHub** (la misma pantalla → *Variables*) o **archivo `.env` en tu equipo** (nunca se sube a Git).

Regla corta: **lo sensible va en un secreto; lo que no es sensible pero cambia, en una variable; lo de tu equipo, en tu `.env`.** Un secreto nunca se imprime en el log; si por error aparece, GitHub lo tapa con `***`, pero igual hay que cambiarlo.

## Ejercicio 7 · Tu proyecto con CI

*Individual o con tu equipo de proyecto · 45 minutos.* Ahora lo haces en tu proyecto: el tuyo de la Clase 3 o uno de los proyectos de práctica del curso.

**Paso 0 · Elige tu proyecto.** Si ya tienes el tuyo en GitHub con un Dockerfile, úsalo. Si no, elige uno de estos. Están en la carpeta `proyectos/` de tu fork y cada uno tiene un README con el negocio, dos pruebas para empezar y los valores para la plantilla.

| Proyecto | Tecnología | El negocio | Carpeta |
| --- | --- | --- | --- |
| Mercado Raíces | Python · Flask | Una cooperativa campesina recibe pedidos de tiendas de barrio | `proyectos/mercado-raices` |
| BiciBarrio | Node.js · Express | Una junta de acción comunal presta bicicletas en tres estaciones | `proyectos/bici-barrio` |
| Biblioteca La Esquina | Sitio estático (HTML, CSS, JavaScript) | Una biblioteca comunitaria publica su catálogo | `proyectos/biblioteca-barrio` |

Usar un proyecto de práctica es válido: lo que se evalúa es lo que haces con él. Escríbelo en tu evidencia.

**Paso 1 · Elige tu plantilla.** Están en `clases/clase-04/villa-nube/ci/plantillas/` del repositorio del curso.

| Tu proyecto… | Usa |
| --- | --- |
| Tiene Dockerfile, pero todavía no tiene pruebas automáticas (cualquier lenguaje, también sitios estáticos). Biblioteca La Esquina | `ci-docker.yml` |
| Es Python y tiene pruebas con pytest. Mercado Raíces | `ci-python.yml` |
| Es Node.js y tiene `npm test`. BiciBarrio | `ci-node.yml` |
| Es tuyo y todavía no tiene Dockerfile | Elige hoy un proyecto de práctica y deja tu Dockerfile como pendiente |

**Paso 2 · Créala desde el navegador.** **Add file** → **Create new file** → pega la plantilla. El nombre del archivo: en tu repositorio, `.github/workflows/ci.yml`; en tu fork, con un proyecto de práctica, `.github/workflows/<nombre-del-proyecto>.yml` (por ejemplo `.github/workflows/mercado-raices.yml`).

**Paso 3 · Cambia lo que dice CAMBIA.**

- La carpeta donde está el Dockerfile (`working-directory`): `"."` en tu repositorio, o la carpeta del proyecto de práctica, por ejemplo `"proyectos/mercado-raices"`.
- El puerto de la aplicación dentro del contenedor (`PUERTO_APP`).
- Tu prueba 1 de la Clase 3: la ruta que se abre y un texto que debe aparecer en la respuesta.
- Tu prueba 2, o borra ese paso si todavía no la tienes.

**Paso 4 · Haz commit y mira Actions.**

- [ ] Mi workflow termina en ✅ verde.

Si queda en rojo, lee el log con los tres pasos del ejercicio 5 antes de pedir ayuda.

**Paso 5 · Provoca un rojo a propósito y arréglalo.** Cambia una sola cosa que tu prueba debería detectar (un texto de la respuesta, una ruta), haz commit, mira el rojo y deshaz el cambio.

- [ ] Tengo el enlace de una ejecución roja y de una verde de mi proyecto.

**Paso 6 · Agrega a tu README la sección «Cómo se valida».**

```markdown
## Cómo se valida

Cada vez que se sube un cambio, GitHub Actions corre el workflow `.github/workflows/ci.yml`:

1. [Qué hace el primer paso importante: construye la imagen, corre las pruebas…]
2. [Tu prueba 1: «Si hago ___, debo ver ___»]
3. [Tu prueba 2, si la tienes]

Si algo falla, el check queda en rojo y el cambio no se considera listo.

Lo que todavía NO se valida: [por ejemplo: la base de datos, el despliegue, la seguridad]
```

**Si usas un proyecto de práctica,** su README trae los valores de cada CAMBIA, dos pruebas para empezar y un rojo para provocar en el paso 5. Escribe la sección «Cómo se valida» en el README de la carpeta del proyecto.

**Minuto 35.** Asegúrate de tener la ejecución roja y la verde: en 10 minutos otra persona va a revisar tu workflow.

## Ejercicio 8 · ¿Qué te protege?

*En parejas · 25 minutos.* Si tu workflow está bien, otra persona puede entender qué protege sin que se lo expliques.

1. A comparte el enlace de su repositorio y de su última ejecución verde, y **no explica nada**.
2. B abre el workflow y el log, y responde la tabla de abajo.
3. A hace en vivo un cambio que su prueba debería detectar. Los dos miran si queda en rojo.
4. A los 10 minutos intercambian.

**Lo anota B**

| Pregunta | Respuesta |
| --- | --- |
| ¿Qué prueba protege este cambio? | |
| Si la prueba falla, ¿qué pasa? (¿se detiene algo?, ¿quién se entera?) | |
| ¿Qué NO está probando este workflow? | |
| ¿El cambio en vivo quedó en rojo? | |

**Ajuste (5 minutos).** Cada autor corrige su workflow o su sección «Cómo se valida» con lo que encontró su compañero.

## Ejercicio 9 · Exit ticket y preparación para la Clase 5

*Individual · 5 minutos.* Responde en el formulario o por chat privado al profesor.

1. En una frase: ¿qué hace tu workflow cada vez que subes un cambio?
2. ¿Qué parte de tu proyecto todavía se revisa o se configura a mano?
3. ¿Qué fue lo más difícil hoy?

**Antes de la Clase 5**

- [ ] Tu `.github/workflows/ci.yml` y tu sección «Cómo se valida» están en GitHub.
- [ ] Guardaste el enlace de una ejecución roja y de una verde.
- [ ] Platzi: avanza en el módulo de la semana. Mientras lo ves, piensa: «¿qué parte de mi infraestructura configuro hoy a mano, con clics, y cómo la describiría en un archivo?».

En la Clase 5 la infraestructura también se describe en archivos, para que se pueda revisar y repetir igual que el código.

## Comandos, problemas frecuentes y retos

**Dónde está cada cosa en GitHub**

| Para qué | Dónde |
| --- | --- |
| Ver las ejecuciones | Pestaña **Actions** de tu repositorio |
| Correr un workflow a mano | Actions → el workflow → **Run workflow** |
| Volver a correr una ejecución | Abre la ejecución → **Re-run jobs** |
| Editar un archivo | Abre el archivo → lápiz ✏️ → **Commit changes** |
| Crear un archivo nuevo | **Add file** → **Create new file** |
| Guardar un secreto | Settings → Secrets and variables → Actions → **New repository secret** |

**Si algo falla**

| Lo que pasa | Qué revisar |
| --- | --- |
| En Actions no aparece nada en mi fork | Falta habilitar Actions: pestaña Actions → botón verde |
| No aparece el botón «Run workflow» | El workflow debe tener `workflow_dispatch` y estar en la rama `main` |
| `Invalid workflow file` | La sangría del YAML: usa espacios, nunca tabuladores, y copia los espacios de la plantilla |
| El workflow no arranca al hacer commit | El archivo debe estar en `.github/workflows/` y terminar en `.yml`; revisa `paths` |
| `pytest: command not found` o `No module named` | Falta el paso que instala las librerías, o falta la librería en `requirements.txt` |
| La prueba de humo da `000` | La app no responde: revisa el puerto (`PUERTO_APP`) y que escuche en `0.0.0.0` |
| La prueba de humo falla en `grep` | La app responde, pero no con el texto que pusiste: abre el log y mira qué respondió |
| El job se queda en amarillo mucho tiempo | Espera; si pasan más de 10 minutos, cancélalo y vuelve a correrlo |
| Verde, pero sé que algo está roto | Busca <code>&#124;&#124; true</code> o `continue-on-error`, o un paso que no corre |

**Retos opcionales, si terminas antes**

- Agrega análisis estático a Villa Nube: un paso con `pip install ruff` y otro con `ruff check --select F app tests`.
- Haz que el workflow guarde el resultado de la prueba de humo como artefacto con `actions/upload-artifact`.
- Protege la rama `main` de tu fork para que un cambio solo se pueda unir si el check está en verde (Settings → Rules → Rulesets).
- Resuelve las fallas preparadas en `fallas-ci/` y anota, para cada una, si es de entorno o de comportamiento.
- Ayuda a otra persona de tu sala: explicar es la mejor forma de aprender.

> Material de apoyo generado con asistencia de IA y revisado por el profesor del curso.
