# Sesión 4: Detección de Anomalías

## 1. ¿Qué es una Anomalía?

Observación que se desvía significativamente del patrón general de los datos; también llamada **outlier**. Su detección permite descubrir fraude, fallas técnicas, errores de sensor o comportamientos inusuales.

> *Referencia: Chandola, V., Banerjee, A. & Kumar, V. (2009). Anomaly detection: A survey. ACM Computing Surveys.*

---

## 2. Tipos de Anomalías

| Tipo | Descripción | Ejemplo |
|------|-------------|---------|
| **Puntual** | Un único registro inusual. | Transacción bancaria atípica. |
| **Contextual** | Inusual solo en un contexto específico. | Temperatura "alta" solo en invierno. |
| **Colectiva** | Grupo inusual aunque cada punto individualmente sea normal. | Ráfaga de paquetes en una red. |

---

## 3. Principales Enfoques

| Enfoque | Métodos representativos | Uso típico |
|---------|-------------------------|-----------|
| **Estadístico** | Z-score, IQR, pruebas de hipótesis. | Datos univariantes con distribución conocida. |
| **Basado en distancia** | k-NN, LOF (Local Outlier Factor). | Datos multivariantes de densidad uniforme. |
| **Basado en densidad** | DBSCAN, Isolation Forest. | Datos de alta dimensión o distribución compleja. |
| **Basado en modelos** | Autoencoders, One-Class SVM. | Anomalías complejas, datos no etiquetados. |

> *Referencia: Aggarwal, C.C. (2017). Outlier Analysis (2ª ed.). Springer.*

---

## 4. Detección con Isolation Forest (ejemplo)

```python
from sklearn.ensemble import IsolationForest
import pandas as pd

modelo = IsolationForest(contamination=0.05, random_state=42)
df['anomalia'] = modelo.fit_predict(df[['feature1', 'feature2']])
# -1 = anomalía, 1 = normal
anomalias = df[df['anomalia'] == -1]
```

---

## 5. Consideraciones Prácticas

- Definir el **umbral de contaminación** según el dominio (fraude ~1–5 %, errores de sensor ~0.1 %).
- Combinar detección automática con **validación de expertos** antes de descartar registros.
- Distinguir entre anomalías que son **errores** (eliminar) y **eventos reales extremos** (conservar y analizar).
- En series de tiempo, considerar el **contexto temporal** para evitar falsos positivos.
