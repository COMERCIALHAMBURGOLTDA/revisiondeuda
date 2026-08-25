# Dashboard de Cartera - Estilo Power BI

## Archivos
- `index.html` — el dashboard, lee los datos en vivo desde Google Sheets

## Fuente de datos: Google Sheets en vivo

El dashboard ya no depende de un archivo local. Carga los datos directamente desde:

```
https://docs.google.com/spreadsheets/d/e/2PACX-1vTZv1MRU94SlBqHDGifdjPZ_UV4hAp1Xezn1eESu0xottRM6QLu5oTCLla-gXgYhvUiTSZ4Q9lmog6s/pub?gid=0&single=true&output=csv
```

Cada vez que abras o refresques el dashboard, trae los datos más recientes de esa hoja — no hace falta reemplazar ningún archivo manualmente.

### Cómo actualizar los datos ahora
1. Pega los datos nuevos (mismo formato de columnas) en la hoja de Google Sheets original.
2. Refresca el navegador donde tengas abierto el dashboard.
3. Listo — no hay que tocar ni copiar archivos.

### Si cambias de hoja de Sheets
Si algún día publicas una hoja distinta, edita la constante `SHEET_CSV_URL` al inicio del `<script>` en `index.html` con la nueva URL "Publicar en la web → CSV".

## Qué hace el dashboard (resumen)

- **Fondo claro** (blanco/gris), tarjetas con sombra sutil, tipografía Segoe UI, estilo Power BI.
- **Cross-filtering real**: clic en gráficos, matriz, ranking de vendedor, filtra todo el dashboard a la vez.
- Filtros locales independientes en algunas tablas (Deuda por cadena, Deuda por comuna) que solo afectan la tabla de detalle, sin tocar KPIs ni gráficos.
- Modal con árbol Comuna → Dirección → Facturas, accesible por cadena (solo visible con el chip SUPERMERCADO REGIONAL activo).
- Botón "Borrar filtros" para resetear todo de una vez.

## Cómo abrirlo en VS Code

Usa `fetch()`, así que **no funciona con doble clic** directo (los navegadores bloquean `fetch` sobre archivos `file://`). Necesitas un servidor local:

### Opción A — Live Server (recomendada)
1. Instala la extensión **"Live Server"** en VS Code.
2. Click derecho sobre `index.html` → **"Open with Live Server"**.

### Opción B — Servidor Python
```
python -m http.server 8000
```
Luego abre `http://localhost:8000`.

## Si el fetch a Google Sheets falla

Si ves un mensaje de "Error cargando datos" en la esquina superior derecha, revisa la consola del navegador (F12 → Console). Las causas más comunes:
- La hoja dejó de estar publicada como CSV (revisa Archivo → Compartir → Publicar en la web en Sheets).
- Problema de red/CORS puntual — recarga la página.
- La URL cambió — actualiza `SHEET_CSV_URL` en el script.


## Fuente complementaria: cheques y documentos por cobrar

El dashboard también carga en vivo la hoja publicada con `gid=1972109013`. Esta fuente alimenta un bloque de resumen ubicado inmediatamente debajo de la matriz de morosidad y antes de los KPI principales.

El resumen muestra monto total, cantidad de documentos, documentos vencidos, próximos vencimientos a 7 días y un desglose por condición de pago.

```
https://docs.google.com/spreadsheets/d/e/2PACX-1vTZv1MRU94SlBqHDGifdjPZ_UV4hAp1Xezn1eESu0xottRM6QLu5oTCLla-gXgYhvUiTSZ4Q9lmog6s/pub?gid=1972109013&single=true&output=csv
```
