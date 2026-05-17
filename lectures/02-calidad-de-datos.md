# Sesión 1: Calidad de Datos

La calidad de los datos se refiere al grado en que un conjunto de datos es adecuado para su uso en un contexto específico. Un dato “de calidad” permite tomar decisiones confiables y reproducir experimentos.

## 1. Dimensiones de la Calidad (Wang & Strong, 1996)
- **Exactitud:** Cercanía entre el valor registrado y la realidad.
- **Completitud:** Ausencia de valores faltantes críticos.
- **Consistencia:** Ausencia de contradicciones internas o entre fuentes.
- **Actualidad:** Vigencia temporal frente al fenómeno analizado.
- **Unicidad:** Cada entidad aparece una sola vez (sin duplicados).
- **Validez:** Conformidad con dominios, tipos y reglas de negocio.

## 2. Datos Faltantes (Missing Data)
Son valores ausentes expresados como `NaN`, `NULL`, espacios vacíos, etc. Provocan pérdida de información y sesgos.

### Mecanismos de falta (Little & Rubin, 2019):
- **MCAR:** Missing Completely at Random (Falta completamente al azar).
- **MAR:** Missing at Random (Falta al azar, depende de otras variables observadas).
- **MNAR:** Missing Not at Random (La falta depende del valor mismo del dato ausente).

### Tratamiento:
- **Eliminación:** *Listwise* (descarta filas) o *Pairwise*.
- **Imputación Simple:** Media, mediana, moda.
- **Imputación Avanzada:** Regresión múltiple, k-NN, MICE (Multiple Imputation by Chained Equations).

## 3. Valores Atípicos (Outliers)
Observación que se desvía sustancialmente del patrón general.

### Causas:
- Errores de captura o fallas de dispositivos.
- Fenómenos extremos reales (fraudes, eventos climáticos).

### Detección y Tratamiento:
- **Detección:** Métodos univariantes (Z-score, IQR) o multivariantes.
- **Tratamiento:** Verificación, corrección, transformación (log, Box-Cox) o eliminación (si es un error probado).
