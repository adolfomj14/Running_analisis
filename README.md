# Impacto Supply y Lucro Cesante — Octubre 2026

Vista interactiva que contrasta el GMV semanal con el stock físico de los 5 productos Top Sellers. Muestra que las caídas de venta responden a quiebres de stock o pérdida de facing visual, y no a baja demanda.

## Contenido

| Archivo | Descripción |
|---|---|
| `index.html` | Página completa (HTML, CSS, JS y datos JSON incrustados) |
| `chart.umd.min.js` | Chart.js local (con respaldo por CDN si no carga) |

## Cómo usarlo

Abrir `index.html` en el navegador. No requiere instalación ni servidor.

## Funcionalidades

- **Resumen global:** número de productos críticos, lucro cesante total estimado y días en riesgo acumulados.
- **Selector de producto:** tarjetas (dropdown en móvil). Al cambiar de producto se actualizan diagnóstico, KPIs, gráfico y línea de tiempo.
- **Diagnóstico:** callout justo debajo del nombre del producto.
- **KPIs:**
  - Venta perdida estimada (lucro cesante), en rojo.
  - Días en riesgo (menos de 3 unidades).
  - Falla del sistema, como etiqueta.
- **Gráfico dual-axis:**
  - Línea azul: GMV semanal en COP (eje izquierdo).
  - Barras: unidades en piso (eje derecho).
  - Franja roja de fondo ("Zona de riesgo") y barras rojas cuando el stock es "Crítico", "Cero" o ≤ 2 unidades.
  - Insignias ⚠️ (quiebre/stock crítico) y 🚚 (pedido manual/push) sobre la línea, con tooltip de detalle.
- **Línea de tiempo semanal:** GMV, nivel de stock, variación % frente a la semana anterior y eventos; las semanas críticas se resaltan en rojo.

## Datos

El objeto `DATA.modulo_supply` está en el `<script>` de `index.html`. Para actualizar cifras basta editar ese JSON; todo se recalcula.

## Supuestos (datos no incluidos en el JSON)

- **Unidades de stock:** se toman de textos como "(6 unds)"; un rango "0-2" cuenta como 2. Si no hay cifra se asigna un valor representativo: Óptimo 7, Medio 4, Bajo 3, Riesgo 3, Crítico 2, Cero 0.
- **Lucro cesante con `null`** (ID 8817439 y 8861547): estimado como la suma de (GMV promedio de semanas sin alerta crítica − GMV de cada semana crítica). Resultado aprox. \$678.400 y \$737.000 COP. La interfaz lo marca como "Estimación calculada".
- **Días en riesgo:** semanas críticas × 7, salvo el ID 8817440, que usa el dato reportado de 23 días.

Si hay datos reales, reemplazarlos en el JSON (`lucro_cesante_estimado`, `dias_riesgo`).

## Historial

1. Módulo creado inicialmente dentro del proyecto EID.
2. Movido a esta carpeta independiente, ya que es una presentación aparte de EID.
3. Rediseño visual: hero, tarjetas resumen, selector en tarjetas, franja de riesgo, insignias de eventos y línea de tiempo.
