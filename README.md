# ComprayVentaSII · Dashboard de Compras y Ventas SII

Dashboard para el gerente basado en el **Registro de Compras y Ventas (RCV)** del SII de Chile. Se suben los CSV de ventas y compras y se analizan por día, mes, trimestre o año, por tipo de documento, comparando meses.

## Funciones

- **Subir archivos**: arrastrar o elegir varios CSV del RCV. Detecta solo si son de Ventas o Compras, quita documentos duplicados y acepta archivos en UTF-8 o Windows-1252.
- **Resumen**: ventas, compras, balance e IVA a pagar con variación vs el período anterior; gráfico ventas vs compras; composición por tipo de documento; top 5 clientes y proveedores.
- **Comparar meses**: Mes A vs Mes B por tipo de documento, con gráfico y tabla de variación %.
- **Documentos**: búsqueda por razón social, RUT o folio, filtro por flujo y orden por columnas.
- Pensado para **tablet** (vertical y horizontal): botones táctiles grandes, pestañas fijas arriba y se puede instalar en la pantalla de inicio.

## Reglas de cálculo

| Concepto | Cálculo |
|---|---|
| Ventas (salidas) | Monto total de los documentos del CSV de Ventas |
| Compras (entradas) | Monto total de los documentos del CSV de Compras |
| Notas de crédito (61) | Restan |
| IVA a pagar | IVA débito (ventas) − IVA crédito recuperable (compras) |

Tipos de documento: 33 factura electrónica, 34 factura exenta, 39 boleta electrónica, 46 factura de compra, 56 nota de débito, 61 nota de crédito.

## Datos

Los CSV se procesan **en el navegador**; no se envían a ningún servidor. Al recargar la página hay que volver a subirlos. En `ejemplos/` hay dos CSV de muestra con el formato del RCV (empresas y RUT ficticios).

## Correr en local

```bash
npx serve .
# o
python3 -m http.server 8000
```

Abrir http://localhost:3000 (serve) o http://localhost:8000.

## Deploy en Vercel

Es un sitio estático, sin build.

1. En vercel.com → **Add New… → Project** → importar este repositorio de GitHub.
2. Framework Preset: **Other**. Build Command: vacío. Output Directory: vacío (raíz).
3. **Deploy**. Cada `git push` a `main` vuelve a publicar.

Con la CLI: `npx vercel` (vista previa) y `npx vercel --prod` (producción).

## Instalar en la tablet

- **iPad (Safari)**: Compartir → *Agregar a pantalla de inicio*.
- **Android (Chrome)**: menú ⋮ → *Instalar app* o *Agregar a pantalla principal*.

## Tecnologías

HTML + JavaScript, Bootstrap 5.3, Chart.js 4, IBM Plex (Google Fonts).

## Próximos pasos

- Guardar los archivos subidos (base de datos o almacenamiento) para no subirlos cada vez.
- Login para el gerente.
- Minería de datos: detección de documentos atípicos, proyección de ventas, segmentación de clientes.
