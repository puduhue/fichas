# Fichas de campo · Puduhue SpA

Sitio estático (GitHub Pages) con la tarjeta de presentación de cada predio lechero, pensado para abrirse
desde un QR en el teléfono, sin cuenta ni aplicación.

## Estructura

```
index.html          portada: lista de campos publicados (ES/EN)
404.html            página de error
robots.txt          bloquea indexación (las fichas son para el directorio, no para buscadores)
.nojekyll           desactiva Jekyll en GitHub Pages
<slug>/index.html   ficha autónoma del campo (un solo archivo, sin dependencias salvo Fira Sans)
<slug>/Tarjeta_QR_<Nombre>.png   tarjeta imprimible 2480×1240 con el QR a <base>/<slug>/
<slug>/qr.json      matriz del QR (n módulos, path SVG, url)
```

La URL de cada ficha es `<base>/<slug>/`. El QR impreso apunta ahí; **no cambiar el nombre del repositorio ni
las carpetas** una vez impresos los QR.

## Cómo se agrega un campo

Los fuentes viven en OneDrive › Portal Puduhue › Versiones portal › scripts (y en el espacio de trabajo de Claude):

1. Crear `campos/<slug>.json` con nombre, slug, corte, 4 KPI de la tarjeta y los archivos fuente de la ficha
   (head, body, script, data).
2. Construir la ficha del campo (head/body/script + `<slug>_data.js`), igual que la de Radales.
3. `python3 build_site.py https://<cuenta>.github.io/fichas` → regenera QR, tarjeta y `site/<slug>/index.html`
   para todos los campos.
4. Agregar la tarjeta del campo a `index.html` (portada) y subir la carpeta `site/` al repositorio.

## Actualización mensual

Reconstruir con los datos al último mes completo y volver a subir `site/<slug>/index.html`. La URL no cambia,
por lo que los QR impresos siguen vigentes.
