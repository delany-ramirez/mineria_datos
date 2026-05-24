# Sesión 4: Ética en Minería de Datos e Introducción al Machine Learning

## 1. Ética y Sesgos en Minería de Datos

### Principios éticos básicos
- **Privacidad:** limitar la re-identificación y usar datos mínimos necesarios (GDPR, 2018).
- **Transparencia:** documentar fuentes, pre-procesamiento, algoritmos y métricas.
- **Justicia (fairness):** evitar que las decisiones automatizadas perjudiquen sistemáticamente a grupos protegidos.
- **No maleficencia:** sopesar beneficios vs. riesgos de daño.

> *Referencia: Barocas, S. & Selbst, A.D. (2016). Big Data's Disparate Impact. California Law Review.*

### Fuentes de sesgo

| Fuente | Descripción |
|--------|-------------|
| **Muestreo** | Sobre-representar ciertas clases induce discriminación en el modelo. |
| **Medición** | Proxies como "código postal" reemplazan variables sensibles y perpetúan desigualdades. |
| **Modelo** | Algoritmos que minimizan error global pueden ignorar el rendimiento en minorías. |
| **Retroalimentación** | Decisiones pasadas sesgadas alimentan nuevos datos (ciclo de refuerzo). |

### Estrategias de mitigación
- **Auditorías de datos:** revisar distribución de atributos sensibles antes de modelar.
- **Pre-procesamiento:** balancear clases, anonimizar, corregir outliers injustificados.
- **Métricas de equidad:** statistical parity, equal opportunity; reportarlas junto a accuracy.
- **Técnicas fairness-aware:** re-ponderación de ejemplos, Adversarial Debiasing, Fair GBM.
- **Gobernanza:** comités de ética, model cards y datasheets para documentar limitaciones.

> *Referencia: Mitchell, S. et al. (2019). Model Cards for Model Reporting. FAccT.*

---

## 2. Introducción al Machine Learning

### ¿Qué es?
Rama de la IA que permite a las computadoras aprender y mejorar automáticamente a través de la experiencia, sin ser programadas explícitamente.

**Componentes clave:** Datos · Algoritmos · Modelos.

### Relación IA – ML – Deep Learning
- **IA:** campo amplio que abarca cualquier técnica para imitar la inteligencia humana.
- **ML:** subconjunto de la IA; aprende patrones a partir de datos.
- **DL:** subconjunto del ML; usa redes neuronales con múltiples capas profundas.

---

## 3. Tipos de Aprendizaje

| Tipo | Descripción | Algoritmos típicos |
|------|-------------|-------------------|
| **Supervisado** | Datos con entradas y salidas conocidas; corrige el modelo con las salidas reales. | Regresión lineal/logística, Árbol de decisión, SVM, Redes neuronales. |
| **No supervisado** | Datos sin etiquetas; busca estructura oculta. | K-Means, Clustering jerárquico, PCA. |
| **Semi-supervisado** | Combina datos etiquetados (pocos) y no etiquetados (muchos). | Aplicaciones en NLP, reconocimiento de imágenes. |
| **Por refuerzo** | Agente aprende interactuando con un entorno maximizando recompensa acumulada. | Q-Learning, AlphaGo, robótica, trading. |

### Tipos de problemas supervisados
- **Regresión:** predicción de valores continuos (e.g., precio de una casa).
- **Clasificación:** asignación de etiquetas a categorías (e.g., detección de spam).

### Tipos de problemas no supervisados
- **Clustering:** agrupar datos similares (e.g., segmentación de clientes).
- **Asociación:** encontrar reglas en grandes porciones de datos (e.g., cesta de mercado).
- **Reducción de dimensionalidad:** simplificar datos manteniendo su estructura esencial (PCA).

---

## 4. Ciclo de Vida de un Proyecto de ML

1. **Definición del problema:** objetivos claros, métricas de éxito, restricciones (tiempo, recursos, datos).
2. **Recolección y preparación de datos:** limpieza, transformación, ingeniería de características.
3. **EDA:** distribuciones, patrones, relaciones entre variables.
4. **Construcción y entrenamiento:** selección del modelo, ajuste de hiperparámetros, validación cruzada.
5. **Evaluación:**
   - Clasificación: Precisión, Recall, F1-score, curva ROC.
   - Regresión: MSE (error cuadrático medio), MAE (error absoluto medio).
6. **Implementación y despliegue.**
7. **Monitoreo y mantenimiento:** detectar data drift y degradación del modelo en producción.
