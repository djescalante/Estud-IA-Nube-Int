# Biblioteca La Esquina · catálogo web

**Tecnología:** HTML, CSS y JavaScript servidos por nginx · sin código de servidor · puerto **80**

## El negocio

La Biblioteca La Esquina es una biblioteca comunitaria que funciona en la casa de la cultura del
barrio. Tiene libros donados y los presta a los vecinos. Hoy la gente llama por teléfono para
preguntar si un libro está disponible.

Este sitio publica el catálogo con un buscador y muestra qué libros están prestados.

## Qué hay

| Archivo | Qué es |
| --- | --- |
| `sitio/index.html` | La página |
| `sitio/estilos.css` | Los colores y la forma |
| `sitio/catalogo.js` | El buscador: lee `libros.json` y filtra mientras escribes |
| `sitio/libros.json` | Los datos: título, autor y si está disponible |
| `Dockerfile` | Dos líneas: nginx y copiar la carpeta `sitio/` |

**La regla del negocio** vive en los datos: un libro con `"disponible": false` se muestra como «Prestado».

## Arrancarlo

```bash
docker build -t biblioteca:0.1.0 .
docker run -d -p 9000:80 --name biblioteca biblioteca:0.1.0
```

Abre <http://localhost:9000> en el navegador.

## Dos pruebas para empezar

1. Si abro `/`, debo ver «Biblioteca La Esquina».
2. Si abro `/libros.json`, debo ver «Cien años de soledad».

## Integración continua en tu fork (Clase 4)

Usa `clases/clase-04/villa-nube/ci/plantillas/ci-docker.yml` y guárdalo como
`.github/workflows/biblioteca-barrio.yml`. Cambia:

| CAMBIA | Valor |
| --- | --- |
| `working-directory` | `"proyectos/biblioteca-barrio"` |
| `PUERTO_APP` | `"80"` |
| Prueba 1 | `curl -s http://localhost:9000/` y el texto `Biblioteca La Esquina` |
| Prueba 2 | `curl -s http://localhost:9000/libros.json` y el texto `Cien años de soledad` |

**Un rojo para provocar:** en `sitio/libros.json` borra el libro «Cien años de soledad». ¿Qué prueba falla?

## Lo que le falta (para las próximas clases)

- Actualizar el catálogo exige editar un archivo y volver a construir la imagen.
- No está publicado en internet.
- No sabemos cuántas personas lo visitan.

Caso ficticio con fines educativos.

## Cómo se valida

Uso el proyecto de práctica Biblioteca La Esquina del curso.

Cada vez que se sube un cambio, GitHub Actions corre el workflow `.github/workflows/biblioteca-barrio.yml`:

1. Construye la imagen de nginx con el sitio y la enciende.
2. Prueba 1: «Si abro /, debo ver Biblioteca La Esquina».
3. Prueba 2: «Si abro /libros.json, debo ver Cien años de soledad».

Si algo falla, el check queda en rojo y el cambio no se considera listo.

Lo que todavía NO se valida: que el buscador filtre bien (curl no ejecuta JavaScript), que los prestados se marquen como «Prestado» y que el sitio esté publicado en internet.
