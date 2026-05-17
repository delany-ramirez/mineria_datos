# Sesión 1: Ingeniería de Características

Proceso de crear, transformar o seleccionar variables para mejorar el rendimiento de los modelos.

## 1. Importancia
- Incrementa el poder predictivo.
- Facilita la interpretabilidad.
- Reduce la dimensionalidad y tiempos de cómputo.

## 2. Codificación de Variables Categóricas
- **One-Hot Encoding:** Crea columnas binarias para cada categoría. Útil para modelos lineales y de distancia.
- **Target / Mean Encoding:** Reemplaza la categoría con el promedio del target para esa categoría.
- **Ordinal Encoding:** Asigna un número entero a cada categoría (si existe un orden natural).

## 3. Escalado y Transformación Numérica
- **StandardScaler (Z-score):** Centra en 0 y escala a varianza unitaria.
- **Min-Max Scaler:** Escala los datos al rango [0, 1].
- **Transformaciones de Potencia:** Log, Box-Cox, Yeo-Johnson para estabilizar varianza y normalizar distribuciones sesgadas.

## 4. Creación de Variables
- **Interacciones:** Producto o combinación de variables (e.g., ingreso × edad).
- **Ratios y Tasas:** E.g., ventas / población.
- **Binning:** Discretización de variables continuas en intervalos (bins).
