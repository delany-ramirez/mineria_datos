# Sesión 2: Bases de Datos Relacionales y SQL

## 1. Bases de Datos Relacionales

- **Base de datos:** conjunto organizado de datos interrelacionados para apoyar la toma de decisiones.
- **SGBD:** software que facilita la creación, almacenamiento, protección y consulta de datos.
- **Modelo relacional:** información distribuida en tablas conectadas. Propuesto por Edgar F. Codd (1970).

### Elementos clave

| Elemento | Descripción |
|----------|-------------|
| **Tabla** | Estructura en filas y columnas que alberga registros. |
| **Registro / campo** | Cada fila = una instancia; cada columna = un atributo. |
| **Dominio** | Conjunto válido de valores para un atributo. |
| **Llave primaria (PK)** | Identifica de forma única cada registro. |
| **Llave foránea (FK)** | Referencia a la PK de otra tabla; preserva la integridad referencial. |

La **cardinalidad** define cuántos registros de una tabla pueden vincularse con los de otra (1:1, 1:N, N:M) y guía la creación de claves.

---

## 2. SQL: Structured Query Language

Lenguaje declarativo estandarizado (ISO/IEC 9075) para definir, consultar y manipular datos.

| Categoría | Comandos |
|-----------|---------|
| **DDL** (Data Definition) | `CREATE`, `ALTER`, `DROP` |
| **DML** (Data Manipulation) | `SELECT`, `INSERT`, `UPDATE`, `DELETE` |
| **DCL/TCL** (Control) | `GRANT`, `COMMIT`, `ROLLBACK` |

Dialectos populares: MySQL, PostgreSQL, SQLite, SQL Server — comparten el núcleo estándar pero difieren en extensiones.

### Conexión en Python

```python
import sqlite3, pandas as pd

con = sqlite3.connect('ventas.sqlite')
df = pd.read_sql('SELECT * FROM clientes', con)
```

Drivers comunes: `sqlite3`, `psycopg2` (PostgreSQL), `pymysql` (MySQL/MariaDB). **SQLAlchemy** ofrece una capa ORM/connector unificada. Usar variables de entorno (`.env` + `dotenv`) para credenciales.

---

## 3. Cláusulas Esenciales

### SELECT — elegir columnas
```sql
SELECT nombre, ROUND(venta, 2) AS total
FROM clientes;
```
Buena práctica: evitar `SELECT *`; usar alias significativos.

### WHERE — filtrar filas
Aplica predicados antes de agrupar. Operadores: `=`, `<>`, `<`, `>`, `BETWEEN`, `LIKE`, `IN`, `IS NULL`.
```sql
WHERE ciudad = 'Pereira' AND total_compra > 1000;
```

### GROUP BY — agregación
Debe acompañarse de funciones agregadas: `SUM`, `AVG`, `COUNT`, `MIN`, `MAX`.
```sql
SELECT categoria, AVG(precio) AS pmedio
FROM productos
GROUP BY categoria;
```

### HAVING — filtrar grupos
Actúa después de `GROUP BY`; admite funciones agregadas.
```sql
HAVING COUNT(*) > 50;
```

### LIMIT / OFFSET — paginación
```sql
LIMIT 10 OFFSET 20;  -- devuelve filas 21–30
```

### JOIN — combinar tablas

| Tipo | Resultado |
|------|-----------|
| `INNER JOIN` | Solo filas con coincidencia en ambas tablas. |
| `LEFT JOIN` | Todas las filas de la tabla izquierda, coincidencias o NULL a la derecha. |
| `RIGHT JOIN` | Inverso al LEFT JOIN. |
| `FULL OUTER JOIN` | Todas las filas de ambas tablas. |

```sql
SELECT c.nombre, SUM(v.monto) AS ventas
FROM clientes c
JOIN ventas v ON c.id = v.cliente_id
GROUP BY c.id;
```
Buena práctica: usar alias claros (`c.nombre`, `v.monto`) para evitar ambigüedad.
