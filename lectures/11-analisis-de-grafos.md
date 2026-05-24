# Sesión 4: Análisis de Grafos

## 1. Introducción

El análisis de grafos estudia estructuras formadas por **nodos** (entidades) y **aristas** (relaciones). En redes sociales, cada usuario es un nodo y sus interacciones son aristas.

**Permite:**
- Identificar influenciadores y puentes entre comunidades.
- Detectar comunidades (clusters) con intereses o comportamientos similares.
- Analizar robustez y vulnerabilidades de la red ante fallos o ataques.

```python
import networkx as nx

G = nx.karate_club_graph()
print(nx.info(G))
```

---

## 2. Conceptos Básicos

| Concepto | Definición |
|----------|-----------|
| **Grado (degree)** | Número de aristas conectadas a un nodo. |
| **Camino** | Secuencia de nodos conectados por aristas. |
| **Diámetro** | Longitud del camino más largo entre cualquier par de nodos. |
| **Clustering coefficient** | Medida de cuánto tienden a agruparse los vecinos de un nodo. |
| **Hub** | Nodo con grado muy alto; característico de redes scale-free. |

### Representaciones
- **Lista de adyacencia:** eficiente para grafos dispersos.
- **Matriz de adyacencia:** eficiente para grafos densos.
- **Lista de aristas (edge list):** formato más común para carga desde archivos.

---

## 3. Métricas Globales y de Centralidad

### Distribución de grado
- **Redes aleatorias (homogéneas):** P(k) se concentra en torno a un valor medio.
- **Redes scale-free:** P(k) sigue una ley de potencia; pocos nodos con grado muy alto (**hubs**). (Barabási & Albert, 1999).

### Métricas de centralidad

| Métrica | Fórmula conceptual | Interpretación |
|---------|--------------------|----------------|
| **Grado** | Número de vecinos directos. | Conectividad inmediata. |
| **Intermediación (Betweenness)** | Fracción de caminos cortos que pasan por el nodo. | Puentes o cuellos de botella en la red. |
| **Cercanía (Closeness)** | Inverso de la distancia promedio a todos los demás. | Difusión rápida de información. |
| **Vector propio (Eigenvector)** | Importancia ponderada por la de los vecinos. | "Autoridad" en la red; base de PageRank. |

---

## 4. Detección de Comunidades

### Algoritmo de Girvan-Newman
Identifica comunidades eliminando iterativamente las aristas con mayor **centralidad de intermediación**, que actúan como puentes entre grupos.

**Pasos:**
1. Calcular la intermediación de todas las aristas.
2. Eliminar la arista con mayor intermediación.
3. Recalcular la intermediación para las aristas afectadas.
4. Repetir hasta obtener estructuras de comunidad significativas.

**Ventaja:** interpretable y bien fundamentado teóricamente.  
**Desventaja:** computacionalmente costoso para redes grandes — O(m² n).

### Método de Louvain
Optimiza la **modularidad** (valor entre −0.5 y 1) de forma jerárquica y heurística.

1. Optimiza modularidad localmente para todos los nodos → comunidades pequeñas.
2. Colapsa cada comunidad en un super-nodo.
3. Repite hasta convergencia.

**Ventaja:** escala a redes con millones de nodos.

> *Referencia: Blondel, V. et al. (2008). Fast unfolding of communities in large networks. Journal of Statistical Mechanics.*

---

## 5. Redes Dinámicas y Predicción de Enlaces

- **Redes dinámicas:** grafos cuya estructura cambia en el tiempo (aparecen/desaparecen nodos y aristas).
- **Predicción de enlaces:** estimar qué conexiones inexistentes tienen mayor probabilidad de formarse, basándose en vecindad común, índice Jaccard o Adamic-Adar.

---

## 6. Conjuntos de Datos Clásicos

### Karate Club (Zachary, 1977)
- **Origen:** estudio etnográfico de 34 miembros de un club de karate en EE. UU.
- **Nodos:** 34 socios. **Aristas:** 78 relaciones de amistad fuera del entrenamiento.
- **Valor didáctico:** presenta hubs y una división natural en dos facciones; ideal para ilustrar centralidad y modularidad.

### Les Misérables (Knuth, 1993)
- **Origen:** red de co-aparición de personajes de la novela de Victor Hugo.
- **Nodos:** 77 personajes. **Aristas ponderadas:** número de escenas compartidas.
- **Valor didáctico:** ilustra cómo los pesos modifican medidas (grado vs. strength); permite comparar algoritmos de comunidades (Girvan-Newman, Louvain, K-means sobre grafos).
