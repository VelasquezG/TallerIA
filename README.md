# Taller IA

Proyecto de análisis y modelado predictivo para identificar clientes con probabilidad de incurrir en mora de 30 días (`Mora30`) o de 60 días (`Mora60`) en sus créditos.

El proyecto pertenece al curso de Inteligencia Artificial e Ingeniería de Software del Tecnológico de Antioquia y utiliza una base de crédito de 10.000 clientes y 27 columnas.


## Configuración del entorno

### 1. Seleccionar Python con pyenv

Comprueba las versiones disponibles e instala Python 3.14 si todavía no está instalado:

```powershell
pyenv versions
pyenv install 3.14
pyenv local 3.14
python --version
```

Si `pyenv install 3.14` no está disponible en tu instalación de pyenv-win, consulta la versión exacta disponible con `pyenv install -l`, instala una versión `3.14.x` y actualiza `.python-version` con ese valor.

### 2. Crear y activar el entorno virtual

Desde la carpeta raíz del proyecto:

```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
```

Cuando el entorno esté activo, el prompt mostrará `(venv)`.

### 3. Instalar dependencias

Actualiza `pip` e instala las dependencias del proyecto:

```powershell
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```