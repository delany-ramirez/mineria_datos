# Configuración de entorno virtual con `venv` para Python >= 3.9

Este documento explica cómo crear un entorno virtual desde cero e instalar las dependencias necesarias para trabajar con análisis de datos en Python.

---

## Requisitos previos

Verifica que tienes instalada una versión de Python **3.9 o superior**.

Ejecuta:

```bash
python --version
```

Debe mostrar algo como:

```bash
Python 3.9.x
```

---

## Librerías requeridas

Crea un archivo llamado **`requirements.txt`** con el siguiente contenido:

```txt
pandas>=2.0.0
numpy>=1.24.0
seaborn>=0.13.0
matplotlib>=3.7.0
```

Si necesitas versiones exactas para reproducibilidad:

```txt
pandas==2.2.3
numpy==1.26.4
seaborn==0.13.2
matplotlib==3.9.2
```

---

## Paso 1: Crear carpeta del proyecto

```bash
mkdir mi_proyecto
cd mi_proyecto
```

---

## Paso 2: Crear el archivo `requirements.txt`

### Linux / Mac

```bash
touch requirements.txt
```

### Windows

```cmd
type nul > requirements.txt
```

Luego pega el contenido de las dependencias.

---

## Paso 3: Crear el entorno virtual

```bash
python -m venv venv
```

Si necesitas especificar versión:

```bash
python3.9 -m venv venv
```

---

## Paso 4: Activar el entorno virtual

### Windows (CMD)

```cmd
venv\Scripts\activate
```

### Windows (PowerShell)

```powershell
.\venv\Scripts\Activate.ps1
```

Si aparece un error de permisos:

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

### Linux / Mac

```bash
source venv/bin/activate
```

---

## Paso 5: Actualizar pip

```bash
python -m pip install --upgrade pip
```

---

## Paso 6: Instalar dependencias

```bash
pip install -r requirements.txt
```

---

## Paso 7: Verificar instalación

Lista las librerías instaladas:

```bash
pip list
```

Prueba rápida:

```python
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt

print("Todo OK")
```

---

## Paso 8: Desactivar el entorno

Cuando termines:

```bash
deactivate
```

---

## Estructura recomendada del proyecto

### Proyecto básico

```txt
mi_proyecto/
├── venv/
├── requirements.txt
└── main.py
```

### Proyecto de análisis de datos

```txt
mi_proyecto/
├── venv/
├── requirements.txt
├── notebooks/
├── data/
├── src/
└── analisis.ipynb
```

---

## Uso diario

Cada vez que abras el proyecto:

### Activar entorno

**Windows**

```cmd
venv\Scripts\activate
```

**Linux / Mac**

```bash
source venv/bin/activate
```

### Ejecutar scripts

```bash
python main.py
```

### Salir del entorno

```bash
deactivate
```

---

## Librerías incluidas

- **pandas** → Manipulación de datos
- **numpy** → Computación numérica
- **seaborn** → Visualización estadística
- **matplotlib** → Gráficos y visualización