# Minimal

`minimal` es un blog estático muy sencillo para publicar notas de restaurantes escritas en Markdown. No usa framework, compilador, base de datos ni dependencias externas. La idea es que toda la página pueda moverse como una sola carpeta y funcionar en cualquier hosting estático.

El sistema se basa en tres piezas:

- Un `index.html` que lee un archivo JSON y construye el listado de restaurantes.
- Un `nota.html` que recibe el nombre del archivo Markdown por query string, por ejemplo `nota.html?file=naan.md`.
- Una carpeta `articulos/` que contiene el índice (`index.json`) y los textos (`*.md`).

La conversión de Markdown a HTML ocurre en el navegador con JavaScript mínimo incluido dentro de `nota.html`. El parser es deliberadamente pequeño: soporta títulos, párrafos, negritas, cursivas, enlaces externos, listas, citas, reglas horizontales, código inline y bloques de código. No pretende cubrir todo Markdown, sino lo necesario para este blog.

## Estructura

- `index.html`: índice de restaurantes.
- `nota.html`: lector genérico para cualquier archivo Markdown listado en el índice.
- `articulos/index.json`: lista de notas disponibles.
- `articulos/*.md`: textos en Markdown.

## Formato del índice

`articulos/index.json` define qué notas aparecen en el índice:

```json
{
  "articles": [
    {
      "file": "naan.md",
      "restaurant": "Naan"
    }
  ]
}
```

- `file`: nombre del archivo Markdown dentro de `articulos/`.
- `restaurant`: texto que aparece como enlace en el índice.

## Agregar una nota

1. Crear el archivo `.md` dentro de `articulos/`.
2. Agregar una entrada en `articulos/index.json`.
3. El índice crea el enlace automáticamente.

## Ejecución

Esta versión usa `fetch()` para cargar `articulos/index.json` y los archivos `.md`. Por eso debe servirse desde un servidor web o hosting estático. Abrir `index.html` con doble clic puede fallar en algunos navegadores por restricciones de seguridad sobre archivos locales.

Para revisarlo localmente desde esta carpeta:

```sh
python3 -m http.server 8000
```

Luego abrir:

```txt
http://localhost:8000/
```
