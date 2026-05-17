# Sesión 1: Análisis Exploratorio de Datos (EDA)

El EDA es un procedimiento sistemático y visual propuesto por Tukey (1977) para comprender la estructura de un conjunto de datos antes del modelado.

## 1. Objetivos del EDA
- Resumir distribuciones y relaciones.
- Verificar supuestos (linealidad, homocedasticidad).
- Identificar outliers y valores faltantes.
- Guiar la selección de transformaciones y modelos.

## 2. Tipos de Análisis
- **Univariante:** 
    - Estadística: Media, mediana, moda, asimetría, curtosis.
    - Visual: Histogramas, Boxplots, Q-Q plots.
- **Bivariante/Multivariante:**
    - Num–Num: Dispersión, correlación (Pearson, Spearman).
    - Cat–Num: Boxplots agrupados.
    - Cat–Cat: Tablas de contingencia, mapas de calor.

## 3. Multicolinealidad
Ocurre cuando dos o más variables independientes están altamente correlacionadas, lo que dificulta la estimación precisa de coeficientes.

**Detección:**
- Matriz de Correlación.
- **VIF (Variance Inflation Factor):** Valores altos indican fuerte multicolinealidad.

## 4. Herramientas Recomendadas
- `ydata-profiling`: Reportes automáticos.
- `sweetviz`, `skimpy`: Alternativas rápidas.
- `Plotly Express`, `Altair`: Dashboards interactivos.
