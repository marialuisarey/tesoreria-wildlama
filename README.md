# Wild Lama — Herramienta de Tesorería e Inversión de Excedentes

Herramienta web interna de análisis para la gestión de excedentes de caja de **Wild Lama** mediante fondos mutuos de deuda. Prioriza **preservación de capital, liquidez operacional, rentabilidad ajustada por riesgo y trazabilidad para aprobación interna**.

> Herramienta interna. No constituye recomendación de inversión.

## Objetivo

- Preservar excedentes de caja y mantener liquidez operacional.
- Rentabilizar fondos mientras no se usan, separando la caja por tramos según horizonte.
- Comparar fondos mutuos de deuda con criterios objetivos y su nivel de riesgo.
- Generar un memo simple para aprobación interna.

## Funcionalidades

- **Dashboard** — cuadro de *Monto a invertir* (ingreso manual), KPIs del universo, tabla de **fondos recomendables con su nivel de riesgo** y composición crediticia, matriz Liquidez–Rentabilidad, distribución por tramo, calidad crediticia promedio y panel de alertas.
- **Explorador** — tabla completa de las 649 series con filtros globales, orden por columna, columnas adicionales y exportación a CSV (separador `;`, formato chileno).
- **Asignación por tramos** — Caja Operativa y Reserva Mediano Plazo, con reglas de elegibilidad propias, asignación por porcentaje y resumen consolidado.
- **Reglas de elegibilidad** — política de inversión auditable.
- **Memo para aprobación** — documento imprimible / PDF que se arma automáticamente desde la asignación.

## Fuente de datos

Los datos provienen de la **CMF Chile — Estudios de Rentabilidades, Costos y Cartera**, procesados vía **Apps Script Wild Lama**:

- Hoja **Fondos**: se consume en vivo desde el endpoint (649 series).
- Hoja **Macro** (UF, Dólar, Euro, UTM, IPC): el endpoint actual **no la expone**; la app muestra valores de respaldo etiquetados como *referenciales*. Ver nota más abajo.

## Estructura de archivos

```
index.html      Aplicación completa (HTML + CSS + JS en un solo archivo)
fonts/          Fuente de marca Minion Pro (.otf)
README.md       Este archivo
.gitignore      Archivos ignorados
```

## Uso local

```bash
python3 -m http.server 8000
```

Luego abrir:

```text
http://localhost:8000
```

## Despliegue en GitHub Pages

1. Sube el repositorio a GitHub.
2. Ve a **Settings → Pages**.
3. En **Build and deployment → Source** elige `Deploy from a branch`.
4. Selecciona la rama (`main`) y la carpeta `/ (root)`.
5. Guarda. La herramienta quedará disponible en `https://<usuario>.github.io/<repo>/`.

## Nota sobre la hoja Macro

El deployment `/exec` entregado responde siempre la hoja **Fondos**, ignorando parámetros de hoja. Para mostrar los indicadores macro en vivo se necesita un endpoint que sirva la hoja **Macro** con columnas `Indicador`, `Valor`, `Fecha dato`, `Actualizado`. Mientras tanto, las tarjetas macro usan valores de respaldo (marcados como *referencial*) y la app detecta automáticamente el endpoint macro si se habilita.

## Formato

Números en formato chileno: separador de miles `.` y decimal `,` (ej. `$1.250.000`, `4,81%`). Valores nulos se muestran como `—`.

---

Última actualización: julio de 2026 · Autor: Tesorería Wild Lama
