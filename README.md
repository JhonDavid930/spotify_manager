# Spotify Manager V9 (Admin Edition)

Aplicación SPA (HTML + CSS + JS) para gestionar playlists de Spotify en el cliente.

## Archivos
- `index.html`: Aplicación monolítica. Edita este único archivo para mantener o extender la app.

## Requisitos
- Navegador moderno (Chrome, Edge, Safari, Firefox).
- No se requiere servidor; puedes abrir `index.html` directamente o usar un servidor estático para mejor compatibilidad.

Opcional (para servir localmente):
```bash
python3 -m http.server 8000
# luego abre http://localhost:8000/index.html
```

## Funcionalidades principales
- Persistencia en `localStorage` bajo la clave `spotify_db_v9`.
- Carga inicial garantizada mediante `fullInitialData` si no hay datos previos.
- Búsqueda en tiempo real (texto: `name` + `desc`) y filtros por `type`, `genre`, `vibe`, `audience` (operador AND).
- Lazy loading: `visibleCount` inicia en 20 y botón "Mostrar más resultados" carga lote siguiente.
- Importar/Exportar CSV (maneja comillas en campos). La importación evita duplicados por `id` o `link`.
- Copiar enlace al portapapeles con fallback `document.execCommand('copy')`.

## Cómo usar
- Abrir `index.html` en el navegador.
- Botones en la barra superior:
  - Importar: seleccionar un `.csv` con cabecera y columnas en el orden exportado.
  - Exportar: descargar `spotify_manager_v9.csv` con la base actual.
  - Nueva: abrir modal para agregar playlist.
  - Reset: restaurar `fullInitialData` (se perderán cambios).
- Filtros: usan combinación AND, escribe en la caja de búsqueda para filtrar por `name`/`desc`.

## Formato CSV esperado (cabecera exportada)
ID,Nombre,Tipo,Genero,Vibe,BPM,Publico,Descripcion,Link

La app exporta y espera este mismo esquema; la importación respeta comillas dobles y campos con comas.

## Notas para desarrolladores
- La lógica está en `index.html` dentro de la etiqueta `<script>`.
- `fullInitialData` contiene la base maestra usada como backup inicial o al resetear.
- Para ajustar el lote de lazy-loading, cambia la variable `visibleCount` en el script.
- Para cambiar la clave de almacenamiento, modifica `'spotify_db_v9'` en `loadData()` y `saveData()`.

## Sugerencias
- Hacer copias de seguridad exportando CSV regularmente.
- Si añades muchas playlists, considera indexar o paginar del lado lógico antes de renderizar.

---
Generado automáticamente para el proyecto local. Si quieres, puedo:
- Abrir `index.html` en un navegador (instrucciones de servidor).
- Añadir tests mínimos o un script de build estático.
