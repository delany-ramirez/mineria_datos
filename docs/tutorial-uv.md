# **Guía Completa para Instalar y Usar uv en Data Science**

## **Qué es UV**

uv es un administrador de paquetes de Python y un resolutor de dependencias (dependency resolver) extremadamente rápido, escrito en Rust. Fue creado por Astral, el mismo equipo detrás de Ruff (el linter de Python súper rápido).

En esencia, uv está diseñado para ser un reemplazo directo y mucho más rápido de herramientas estándar como pip, pip-tools y virtualenv. Su objetivo principal es acelerar drásticamente los flujos de trabajo de desarrollo en Python.

## **Por qué usar UV en data science**

El ecosistema de Data Science en Python es conocido por tener paquetes pesados con muchas dependencias complejas (como Pandas, NumPy, Scikit-learn, TensorFlow, PyTorch). Usar uv en este contexto ofrece ventajas críticas:

1. **Velocidad Extrema:** uv es increíblemente rápido resolviendo dependencias e instalando paquetes (a menudo de 10 a 100 veces más rápido que pip). Esto ahorra horas de espera al configurar nuevos entornos o actualizar proyectos, algo común en Data Science.  
2. **Resolución de Dependencias Confiable:** En Data Science, los conflictos de versiones son un dolor de cabeza constante. El resolutor de uv es muy estricto y eficiente, asegurando que los entornos sean reproducibles y estables.  
3. **Gestión de Entornos Integrada:** No necesitas usar herramientas separadas como virtualenv o venv. uv maneja la creación de entornos virtuales directamente y con mucha mayor velocidad.  
4. **Caché Global:** uv utiliza una caché global eficiente, lo que significa que si ya instalaste un paquete pesado (como PyTorch) en un proyecto, no tendrá que volver a descargarlo para un proyecto nuevo, ahorrando espacio en disco y tiempo de red.  
5. **Reemplazo Directo:** Su interfaz de línea de comandos está diseñada para ser muy similar a pip (uv pip install ...), por lo que la curva de aprendizaje es casi nula para quienes ya conocen las herramientas estándar.

## **Cómo instalar UV**

La instalación de uv es muy sencilla y se recomienda hacerla a nivel de sistema. Aquí te mostramos los métodos más comunes según tu sistema operativo:

### **En macOS y Linux**

La forma más recomendada es a través de su script de instalación o usando curl:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Si usas macOS y tienes **Homebrew**, puedes instalarlo así:

```bash
brew install uv
```

### **En Windows**

Puedes instalar uv usando PowerShell:

```powershell
powershell -c "irm https://astral.sh/uv/install.ps1 | iex"
```

Alternativamente, si usas **pipx** (una gran herramienta para instalar aplicaciones de Python globalmente):

```bash
pipx install uv
```

*Nota: Una vez instalado, asegúrate de reiniciar tu terminal para que reconozca el comando `uv`.*

## **Cómo activar el env UV**

uv facilita enormemente la creación de entornos virtuales (environments).

1. **Crear el entorno virtual:**  
   Para crear un nuevo entorno virtual en el directorio actual (por defecto se llamará .venv), ejecuta:  
   
   ```bash
   uv venv
   ```

2. **Activar el entorno virtual:**  
   La activación depende de tu sistema operativo (es igual a como activarías un entorno creado con el módulo venv estándar de Python):  
   * **En macOS y Linux:**  
     ```bash
     source .venv/bin/activate
     ```

   * **En Windows (Command Prompt):**  
     ```bat
     .venv\Scripts\activate.bat
     ```

   * **En Windows (PowerShell):**  
     ```powershell
     .venv\Scripts\Activate.ps1
     ```

Una vez activado, deberías ver (.venv) al principio de tu línea de comandos.

## **Cómo instalar paquetes UV**

Una vez que tienes tu entorno virtual activado, instalar paquetes con uv es muy similar a usar pip, pero debes anteponer uv pip.

* **Para instalar un solo paquete:**  
  ```bash
  uv pip install pandas
  ```

* **Para instalar múltiples paquetes:**  
  ```bash
  uv pip install numpy scikit-learn matplotlib
  ```

* **Para instalar desde un archivo requirements.txt:**  
  ```bash
  uv pip install -r requirements.txt
  ```

* **Para actualizar un paquete:**  
  ```bash
  uv pip install -U pandas
  ```

* **Para generar un archivo de requisitos (similar a pip freeze):**  
  ```bash
  uv pip freeze > requirements.txt
  ```

## **Recomendaciones**

* **Úsalo junto a `uvx`:** Al instalar `uv`, también se instala `uvx`. Esta es una herramienta fantástica (similar a `pipx`) para ejecutar herramientas de línea de comandos escritas en Python sin tener que instalarlas globalmente, en entornos aislados y temporales. Por ejemplo: `uvx ruff check .`.  
* **Aprovecha el modo "Sync":** Si usas archivos de requerimientos o proyectos más formales, investiga el comando `uv pip sync requirements.txt`. Este comando asegura que tu entorno tenga *exactamente* lo que dice el archivo, eliminando los paquetes que no estén listados.  
* **Integración con CI/CD:** Debido a su velocidad, `uv` es ideal para pipelines de Integración Continua (CI). Cambiar `pip install` por `uv pip install` en tus scripts de GitHub Actions o GitLab CI puede reducir significativamente los tiempos de construcción.  
* **Migración gradual:** No necesitas cambiar todos tus flujos de trabajo de inmediato. Puedes empezar usando uv solo para instalar paquetes en nuevos proyectos y ver cómo se siente antes de adoptarlo completamente.

## **FAQ**

**¿uv reemplaza a Conda en Data Science?**

No necesariamente. Conda es excelente instalando dependencias binarias complejas (no solo de Python, como librerías de C/C++ necesarias a veces para Data Science). Sin embargo, uv es mucho más rápido para paquetes puros de Python. Muchos Data Scientists usan una combinación: Conda para el entorno base y librerías críticas, y uv para instalar paquetes de Python rápidamente dentro de ese entorno.

**¿Funciona uv con Jupyter Notebooks?**

¡Sí\! Una vez que creas y activas un entorno con uv e instalas jupyter o ipykernel dentro de él, puedes registrar ese entorno para usarlo en tus notebooks de la misma manera que lo harías con un entorno venv estándar.

**¿Puedo usar uv sin activar el entorno virtual?**

Sí. `uv` es inteligente. Si estás dentro de un proyecto que tiene un directorio `.venv`, puedes ejecutar comandos de Python dentro de ese entorno sin activarlo explícitamente usando `uv run`. Por ejemplo: `uv run python mi_script.py`.

**¿Qué pasa si un paquete requiere compilación durante la instalación?**

uv puede compilar paquetes desde el código fuente si es necesario, pero prefiere instalar "wheels" (paquetes precompilados) por velocidad. Si falla la instalación de un paquete muy complejo, a veces puede requerir que tengas instaladas las herramientas de compilación del sistema (como build-essential en Linux).