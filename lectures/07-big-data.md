# Sesión 2: Big Data, Bodegas y Lagos de Datos

## 1. Motivación

- Explosión de datos desde 2010: redes sociales, sensores IoT, logs web, genómica.
- Limitaciones de los RDBMS clásicos: escalado vertical costoso, latencias altas con terabytes.
- Demanda empresarial de analítica en tiempo real e histórica.

---

## 2. Definición Formal

> *"Conjunto de tecnologías y prácticas que permiten capturar, almacenar, procesar y analizar datos cuyo volumen, velocidad o variedad excede la capacidad de los sistemas convencionales."* — Gartner.

- **Esquema-on-read:** estructura inferida durante la consulta, no al cargar.
- **Paradigma scale-out:** clústeres de hardware commodity en lugar de un único servidor potente.

---

## 3. Las 5 V

| V | Descripción |
|---|-------------|
| **Volumen** | Terabytes/Petabytes generados continuamente. |
| **Velocidad** | Datos que llegan en tiempo real o casi real. |
| **Variedad** | Múltiples formatos: estructurado, semiestructurado, no estructurado. |
| **Veracidad** | Incertidumbre e inconsistencia en los datos de origen. |
| **Valor** | Extracción de conocimiento útil para la toma de decisiones. |

---

## 4. Arquitectura Lambda

| Capa | Función | Herramientas |
|------|---------|--------------|
| **Batch** | Procesa datos históricos con alta precisión; mayor latencia. | Hadoop, Spark batch. |
| **Velocidad** | Procesa flujos en tiempo real con baja latencia. | Kafka, Spark Streaming. |
| **Servicio** | Combina resultados de ambas capas para consultas unificadas. | HBase, Cassandra, APIs. |

---

## 5. Criterios de Elección

| Usar **RDBMS** si... | Usar **Big Data** si... |
|----------------------|------------------------|
| Integridad fuerte requerida. | Múltiples formatos de datos. |
| Volumen ≤ 1 TB. | Procesamiento streaming. |
| OLTP/OLAP ligero. | Crecimiento impredecible. |
| | IA y analítica a escala. |

**Modelo híbrido:** base transaccional + lago de datos para analítica.

---

## 6. Bodegas y Lagos de Datos

| | **Data Warehouse** | **Data Lake** |
|---|---|---|
| **Definición** | Almacén histórico optimizado para consultas analíticas y reportes. | Gran repositorio que conserva la información en su estado bruto. |
| **Esquema** | Schema-on-write (estructura al cargar). | Schema-on-read (estructura al consultar). |
| **Datos** | Estructurados, procesados. | Todos los formatos, sin procesar. |
| **Usuarios típicos** | Analistas de negocio. | Científicos de datos, ingenieros. |

---

## 7. Retos y Mejores Prácticas

- **Gobernanza:** catálogo de datos, linaje, cumplimiento GDPR.
- **Costos:** gestión eficiente de red y almacenamiento frío.
- **Observabilidad:** métricas, alertas y pruebas de calidad de datos.
- **Ética:** control de sesgos algorítmicos y privacidad de usuarios.

> *Referencia: Han, J., Kamber, M. & Pei, J. (2012). Data Mining: Concepts and Techniques (3ª ed.).*
