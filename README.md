# JAGUAR TECH — sitio con catálogo desde Excel

Sitio estático (sin PHP, sin base de datos) que lee tu catálogo
directamente de `productos.xlsx` en el navegador, y genera cotizaciones
con folio (ticket) para enviar por WhatsApp.

## Estructura

```
jaguar-tech/
├── index.html          ← el sitio completo (no lo edites salvo lo indicado abajo)
├── productos.xlsx       ← TU CATÁLOGO. Este es el que reemplazas seguido.
├── imagenes/             ← fotos de tus productos
│   └── LEEME.txt
└── README.md             ← este archivo
```

## Publicar en GitHub Pages

1. Crea un repositorio en GitHub (público o privado con Pages habilitado
   en el plan que tengas).
2. Sube estos 4 elementos (`index.html`, `productos.xlsx`, la carpeta
   `imagenes/`, `README.md`) a la raíz del repositorio.
3. Ve a **Settings → Pages**.
4. En "Source" elige la rama (normalmente `main`) y la carpeta `/root`.
5. Guarda. GitHub te da una URL tipo
   `https://tuusuario.github.io/jaguar-tech/`.

## Cómo actualizar el catálogo (lo harás seguido)

1. Abres `productos.xlsx` en Excel.
2. Agregas, borras o editas filas. **No cambies los nombres de las
   columnas de la fila 1** (el sitio busca esos nombres exactos).
3. Guardas el archivo (mismo nombre: `productos.xlsx`).
4. Lo subes a GitHub reemplazando el anterior (arrastrar y soltar en la
   página del repo, o hacer commit desde tu editor).
5. Refrescas la página — el catálogo ya está actualizado. No hay que
   tocar el `index.html`.

## Columnas del Excel

| Columna | Para qué sirve |
|---|---|
| ID | identificador interno, no se muestra al cliente |
| Clave TVC | referencia de tu proveedor |
| Nombre | título del producto (obligatorio) |
| Marca / Modelo | se muestran debajo del nombre |
| Tipo de producto | informativo, no se filtra por él |
| Etapa de producto | si dice "Nuevo" se muestra una etiqueta NUEVO |
| Clave SAT / Descripción SAT | informativo |
| **Categoría 1** | genera los botones de filtro automáticamente |
| Categoría 2 | se muestra como subcategoría junto al nombre |
| **Precio de Lista USD** | el que ve el cliente en el catálogo |
| Precio de Distribuidor USD | **no se muestra en el sitio** — queda solo en tu Excel como referencia interna de costo |
| **Foto del Producto** | nombre exacto del archivo dentro de `imagenes/` (ej. `DH-H3A.jpg`). Si lo dejas vacío, se muestra un ícono automático según la categoría |

Las categorías (botones "Cámaras", "Cómputo", "Redes"...) se generan
solas a partir de lo que escribas en "Categoría 1" — no hay que tocar
código para agregar una categoría nueva, solo úsala en el Excel.

## Imágenes

Coloca los archivos dentro de `imagenes/` con el mismo nombre que
pusiste en la columna "Foto del Producto". Si el archivo no existe o
el nombre no coincide, el producto simplemente muestra un ícono en
vez de romperse.

## Configuración del sitio (logo, nombre, WhatsApp)

Dentro del sitio hay un botón ⚙️ en el encabezado:

- Cambia nombre del negocio, eslogan, número de WhatsApp y logo
  (emoji/texto o imagen).
- Cambia el % de anticipo que se muestra en cada cotización (por
  defecto 70% anticipo / 30% saldo).
- **Importante:** como es una página estática, lo que guardas ahí solo
  se ve en tu propio navegador (sirve para probar). Para que el cambio
  se vea igual para todos tus visitantes, usa el botón **"Exportar
  código"** dentro del panel: te da un bloque de texto que debes pegar
  reemplazando el objeto `SITE_CONFIG` al inicio del `<script>` en
  `index.html`, y luego subir ese archivo actualizado a GitHub.

## Cotizador y tickets

- El cliente agrega productos al carrito (🛒), ajusta cantidades y
  pulsa "Solicitar cotización por WhatsApp".
- El sitio genera un folio único (ej. `JT-20260813-0007`), calcula el
  anticipo/saldo según el % configurado, y abre WhatsApp con todo el
  detalle ya escrito.
- Cada cotización (ticket) se guarda en el navegador del cliente, en
  "Mis cotizaciones" (link en el pie de página), por si necesita
  reenviarla después.
- Ese historial vive en cada navegador/dispositivo, no en un servidor
  central — no hay forma de verlo tú desde otro lado sin agregar un
  backend.

## Probar localmente antes de subir a GitHub

Si abres `index.html` con doble clic (protocolo `file://`), el
navegador normalmente bloquea la lectura automática de
`productos.xlsx` por seguridad. En ese caso el sitio te muestra un
botón para seleccionar el archivo manualmente y probar el catálogo ahí
mismo.

Para probarlo exactamente como se verá en producción, ábrelo con
Laragon (como ya trabajas normalmente) o cualquier servidor local —
ahí sí carga `productos.xlsx` automáticamente por `fetch`, igual que
en GitHub Pages.
