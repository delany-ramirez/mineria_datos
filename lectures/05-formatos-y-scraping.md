# Sesión 2: Formatos de Datos y Web Scraping

## 1. CRISP-DM: Comprensión de los Datos

La fase **Data Understanding** del ciclo CRISP-DM implica tres acciones principales:

- Localizar fuentes (archivos locales, bases de datos, APIs).
- Evaluar calidad (completitud, consistencia).
- Documentar metadatos (origen, fecha, licencia).

---

## 2. Formatos de Almacenamiento Local

Los datos estructurados se almacenan habitualmente en los siguientes formatos:

| Formato | Características |
|---------|----------------|
| `.csv`  | Texto plano delimitado por comas; universal y ligero. |
| `.xlsx` | Hoja de cálculo de Excel; admite múltiples hojas y fórmulas. |
| `.json` | Notación clave-valor anidable; común en APIs web. |
| `.xml`  | Etiquetas jerárquicas; usado en integraciones empresariales. |

### Buenas prácticas al importar

- Verificar encoding (`'utf-8'`, `'latin-1'`). Un encoding incorrecto produce caracteres ilegibles como `Ã©` en lugar de `é`.
- Declarar tipos con `dtype=` para ahorrar memoria.
- Usar `na_values=` para estandarizar valores faltantes.
- Validar filas/columnas inesperadas:

```python
df = pd.read_csv('ventas.csv', on_bad_lines='skip')
assert df.isnull().mean().max() < 0.1, "Exceso de NA"
```

---

## 3. Web Scraping Responsable en Python

**Web Scraping** es la extracción automática de contenido HTML o JSON publicado en la Web.

- **Casos de uso:** seguimiento de precios, estudios de opinión, datasets abiertos.
- **Diferencia con APIs:** la página no fue diseñada para consumo máquina.

### Librería `requests`

```python
import requests, time

url = 'https://books.toscrape.com/'
resp = requests.get(url, headers={'User-Agent': 'UTP-MD-2025'})
resp.raise_for_status()   # detiene ante error >399
html = resp.text
time.sleep(1)             # polite delay
```

### Datos Estructurados vs. No Estructurados

**Datos estructurados:** organizados en formato predefinido (tablas, filas y columnas). Facilitan la búsqueda, el análisis automatizado y el entrenamiento de modelos.

**Características:**
- Formato estándar por columna (numérico, texto, fecha).
- Consultables directamente con SQL.
- Escalables a grandes volúmenes.

**Recomendaciones para formatear una tabla:**
- Encabezados descriptivos únicos (sin espacios ni tildes si se usará software estadístico).
- Una fila = un registro.
- Formato consistente para datos similares (fechas, unidades).
- Manejar valores faltantes y duplicados adecuadamente.

**Datos no estructurados:** sin formato predefinido (textos libres, imágenes, vídeos, audios, publicaciones en redes sociales). Requieren técnicas avanzadas como NLP o visión por computadora.
