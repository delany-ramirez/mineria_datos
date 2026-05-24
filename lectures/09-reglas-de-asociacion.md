# Sesión 4: Reglas de Asociación

## 1. ¿Qué son las Reglas de Asociación?

Las reglas de asociación expresan la probabilidad de que, si ocurre un conjunto de elementos (**antecedente**), también ocurra otro (**consecuente**). Son fundamentales en el **análisis de cesta de mercado**.

**Aplicaciones:**
- Análisis de cesta de compra en supermercados.
- Recomendación de productos en tiendas en línea.
- Análisis de redes (grupos de nodos con conexiones frecuentes).
- Diagnóstico médico (patrones de enfermedades y síntomas).

---

## 2. Métricas Clave

| Métrica | Definición formal | Interpretación |
|---------|-------------------|----------------|
| **Soporte** | `P(X ∪ Y)` | Fracción de transacciones que contienen tanto X como Y. |
| **Confianza** | `P(Y \| X) = Soporte(X ∪ Y) / Soporte(X)` | Probabilidad de Y dado que ocurrió X. |
| **Lift** | `Confianza(X → Y) / Soporte(Y)` | Fuerza de la asociación más allá del azar. Lift > 1 indica asociación positiva. |

---

## 3. Algoritmo Apriori

Propuesto por Agrawal & Srikant (1994). Se basa en la **propiedad Apriori**: todo subconjunto de un conjunto frecuente también es frecuente. Si un k-ítemset no supera el soporte mínimo, ninguno de sus superconjuntos lo superará.

### Notación formal

Sea `𝒟` un conjunto de N transacciones, `𝑰` el conjunto de todos los ítems, y un k-ítemset `X ⊆ 𝑰` con `|X| = k`.

```
Soporte(X) = |{t ∈ 𝒟 : X ⊆ t}| / N
```

### Pasos del algoritmo

1. **Nivel 1 (k = 1):** contar el soporte de cada ítem individual; conservar los que superan el umbral `σ`.
2. **Generar candidatos k-ítem:** combinar pares de conjuntos frecuentes de tamaño k−1 que difieren en un solo ítem; descartar cualquier candidato cuyo subconjunto de tamaño k−1 no sea frecuente.
3. **Conteo de soporte:** recorrer la base de datos una vez por nivel y actualizar contadores; retener solo los candidatos que siguen cumpliendo `σ`.
4. **Iterar** `k ← k + 1` hasta que no queden candidatos frecuentes.
5. **Generar reglas:** para cada conjunto frecuente probar todas las divisiones `X → Y`; aceptar las que cumplan la confianza mínima `γ` y, opcionalmente, lift > 1.

### Ejemplo de tabla transaccional

| Transacción | Ítems |
|-------------|-------|
| T1 | Pan, Leche |
| T2 | Pan, Pañales, Cerveza |
| T3 | Leche, Pañales, Cerveza, Cola |
| T4 | Pan, Leche, Pañales, Cerveza |

Con soporte mínimo = 0.5: `{Pan, Leche}` → `{Cerveza}` podría ser una regla válida si su confianza supera el umbral.
