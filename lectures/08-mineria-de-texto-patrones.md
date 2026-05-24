# Sesión 3: Minería de Texto y Detección de Patrones

## 1. Expresiones Regulares (Regex)

Las **expresiones regulares** son un instrumento formal para buscar, extraer y validar patrones textuales sobre grandes volúmenes de datos.

**Usos típicos:**
- Limpieza de logs y texto libre.
- Normalización de cadenas.
- Extracción de entidades (fechas, e-mails, teléfonos).
- Filtrado de ruido en pipelines ETL.

**Ventajas:** concisión, reproducibilidad, alto rendimiento.

**Módulos:**
- Python: `re`
- R: `grep`, `regexpr`, `stringr`

---

## 2. Metacaracteres y Anclas

### Metacaracteres principales

| Símbolo | Significado |
|---------|-------------|
| `.`     | Cualquier carácter excepto salto de línea. |
| `^`     | Inicio de cadena (o inicio de línea con `re.MULTILINE`). |
| `$`     | Fin de cadena (o fin de línea con `re.MULTILINE`). |
| `\|`    | Alternancia (OR). |
| `()`    | Grupo de captura. |
| `[]`    | Clase de caracteres. |
| `{n,m}` | Cuantificador de rango. |

### Anclas comunes

| Ancla | Descripción |
|-------|-------------|
| `\b`  | Límite de palabra (word boundary). |
| `\B`  | No-límite de palabra. |
| `^`   | Inicio de cadena. |
| `$`   | Fin de cadena. |

---

## 3. Clases de Caracteres (`[...]`)

Conjunto entre corchetes que coincide con **un solo carácter** perteneciente a la lista.

```python
[aeiou]     # cualquier vocal minúscula
[A-Z0-9]    # mayúsculas o dígitos
[^0-9]      # cualquier carácter que NO sea dígito (negación con ^)
```

**Reglas:**
- `^` al inicio → negación.
- `-` define rangos; colócalo al final si es literal: `[A-Z-]`.
- `]` y `\` deben escaparse: `[\]]`.

### Clases abreviadas

| Clase | Equivalente | Descripción |
|-------|-------------|-------------|
| `\d`  | `[0-9]`     | Dígito. |
| `\D`  | `[^0-9]`    | No dígito. |
| `\w`  | `[a-zA-Z0-9_]` | Carácter de palabra. |
| `\W`  | `[^\w]`     | No carácter de palabra. |
| `\s`  | `[ \t\n\r]` | Espacio en blanco. |
| `\S`  | `[^\s]`     | No espacio. |

---

## 4. Escape de Caracteres Especiales

Los símbolos `. ^ $ * + ? { } [ ] ( ) | \` tienen significado meta. Para usarlos como **literales**, se antepone `\`.

```python
import re

texto = "Precio final: 9.99$ (oferta)."

# Coincide con el literal 9.99$
pat = r"\d\.\d{2}\$"
re.findall(pat, texto)
# ['9.99$']
```

> Usar **raw strings** (`r"..."`) evita conflictos con las secuencias de escape de Python.

### Secuencias de escape comunes

| Secuencia | Descripción |
|-----------|-------------|
| `\n`      | Salto de línea. |
| `\t`      | Tabulador. |
| `\\`      | Barra inversa literal. |
| `\.`      | Punto literal. |

---

## 5. Cuantificadores

| Cuantificador | Significado |
|---------------|-------------|
| `*`           | 0 o más repeticiones (greedy). |
| `+`           | 1 o más repeticiones (greedy). |
| `?`           | 0 o 1 repetición (opcional). |
| `{n}`         | Exactamente n repeticiones. |
| `{n,m}`       | Entre n y m repeticiones. |
| `*?`, `+?`    | Versión lazy (mínima). |

```python
# Fechas AAAA-MM-DD
pat = r"\b\d{4}-\d{2}-\d{2}\b"
re.findall(pat, texto)
```

---

## 6. Grupos, Alternancia y Referencias

Los **grupos de captura** `()` permiten extraer sub-patrones; los **grupos nombrados** `(?P<nombre>...)` mejoran la legibilidad.

```python
p = re.compile(r"(?P<user>\w+)@(?P<dom>\w+\.\w+)")
m = p.search("contacto: ana92@utp.edu.co")
m.groupdict()
# {'user': 'ana92', 'dom': 'utp.edu.co'}
```

**Alternancia:** `(gato|perro)` coincide con `gato` o `perro`.

---

## 7. Banderas en Python

| Bandera | Efecto |
|---------|--------|
| `re.IGNORECASE` (`re.I`) | Ignora mayúsculas/minúsculas. |
| `re.MULTILINE` (`re.M`)  | `^` y `$` coinciden en cada línea. |
| `re.DOTALL` (`re.S`)     | `.` también coincide con `\n`. |
| `re.VERBOSE` (`re.X`)    | Permite espacios y comentarios dentro del patrón. |

### Flujo de trabajo recomendado

1. Bosquejar el patrón en [regex101.com](https://regex101.com).
2. Probar con un subconjunto del corpus.
3. Refactorizar con grupos nombrados y comentarios `re.VERBOSE`.
4. Integrar en el pipeline ETL o notebook.

---

## 8. Buenas Prácticas

- Mantener patrones pequeños y testeables; dividir la lógica compleja en múltiples expresiones.
- Documentar con `re.VERBOSE` para facilitar el mantenimiento.
- Compilar patrones una sola vez con `re.compile` para mejorar el rendimiento.
- Validar contra casos borde antes de aplicar a producción.

```python
# Compilación única para reutilización
EMAIL_PAT = re.compile(r"[\w.+-]+@[\w-]+\.[a-z]{2,}", re.IGNORECASE)

correos = EMAIL_PAT.findall(texto_completo)
```

> *Referencia: Friedl, J. (2006). Mastering Regular Expressions (3ª ed.). O'Reilly.*
