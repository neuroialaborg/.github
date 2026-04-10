#  <img src="../icons/folder_tree.png" width="48" height="48" style="vertical-align:middle;"> Estructura de Proyectos

Se adopta la estructura de proyectos con el patrón `src layout`, estándar ampliamente utilizado en la comunidad Python y proyectos Open Source de referencia.

---

## 🎯 Objetivo y Contexto

> [!NOTE]
> Este estándar no busca restringir la creatividad del equipo, sino proporcionar una base unificada. Garantizar que todos los repositorios de la organización compartan una estructura de carpetas similar permite que los proyectos sean predecibles y mucho más legibles.

La adopción de esta guía resuelve problemas concretos generados por la falta de consistencia:

| ❌ Problema (Sin estándar) | ✅ Solución (Con estándar) |
| :---: | :---: |
| "¿Dónde va este archivo nuevo?" | Cada tipo de artefacto tiene un lugar único y predecible. |
| Imports rotos al correr tests. | El `src layout` aísla el paquete del entorno de desarrollo. |
| Configuración duplicada en múltiples archivos. | `pyproject.toml` centraliza todo en un único punto de verdad. |
| Onboarding lento de nuevos miembros. | La estructura conocida elimina la curva de exploración inicial. |

---

## 🌟 Reglas

> [!IMPORTANT]
> Las siguientes directrices representan decisiones de diseño clave. Se establecen con el objetivo de mantener los repositorios ordenados, predecibles y estructurados.

* 📂 **Uso del `src` layout:** El código fuente del paquete vive exclusivamente dentro de `src/<nombre_paquete>/`. Esta separación evita conflictos internos de Python al momento de correr las pruebas.
* ⚙️ **`pyproject.toml` como único punto de verdad:** Toda la configuración del proyecto se declara de forma centralizada en el `pyproject.toml`. Se debe evitar la creación de archivos de configuración paralelos como `setup.cfg`, `setup.py` o `.flake8` para no fragmentar el proyecto.
* 🧪 **Tests fuera del paquete:** El directorio `tests/` vive a nivel raíz, nunca dentro de `src/`. Los tests no son parte del programa en sí; incluirlos dentro aumenta el peso del proyecto y genera conflictos de importación.
* 🧩 **Sin lógica en `__init__.py`:** Los archivos `__init__.py` le indican a Python que una carpeta es un paquete importable. Su único rol es facilitar las importaciones, no contener lógica de negocio.
* 📦 **Separación estricta de entornos:** El `pyproject.toml` tiene dos "cajones" de dependencias: uno para lo que el programa necesita para **funcionar**  ([tool.poetry.dependencies]), y otro para lo que el equipo necesita para **desarrollarlo** ([tool.poetry.group.dev.dependencies]), como linters y herramientas de testing. Nunca mezclar ambos. Ver ejemplo en [Configuración de pyproject.toml](#️-configuración-de-pyprojecttoml)

---

## 🛠️ Implementación

### Árbol de directorios canónico

Esta es la estructura mínima viable para un proyecto Python de la organización. Todo proyecto nuevo debe respetar este esqueleto como punto de partida.

```
mi-proyecto/
├── src/
│   └── mi_paquete/           # Código fuente (nombre en minúsculas y sin guiones)
│       ├── __init__.py       # Solo facilita importaciones (sin lógica)
│       └── core.py           # Lógica principal del proyecto
├── tests/                    # Pruebas automatizadas (siempre fuera de src/)
│   ├── __init__.py
│   └── test_core.py          # Espeja la estructura de src/mi_paquete/
├── .gitignore                # Archivos y carpetas ignorados por Git
├── pyproject.toml            # ★ Punto de verdad: metadatos, dependencias y herramientas
└── README.md                 # Documentación principal del repositorio
```

---

### ✅ Prácticas correctas

**Estructura de `__init__.py`:**

```python
# src/mi_paquete/__init__.py
# ✅ Solo facilita importaciones. No contiene lógica.
from mi_paquete.core import MiClasePrincipal

__all__ = ["MiClasePrincipal"]
```

**Test que espeja la estructura de `src/`:**

```python
# tests/test_core.py
# ✅ La ruta del test refleja la ruta del módulo que testea.
from mi_paquete.core import MiClasePrincipal

def test_ejemplo():
    instancia = MiClasePrincipal()
    resultado = instancia.ejecutar()
    assert resultado is not None
```

---

### ❌ Prácticas desaconsejadas

**1. Paquete en la raíz (flat layout):**

```
# ❌ El paquete vive en la raíz, fuera de src/.
mi-proyecto/
├── mi_paquete/       ← ERROR: debe estar dentro de src/
│   └── __init__.py
└── pyproject.toml
```

**2. Lógica de negocio en `__init__.py`:**

```python
# ❌ __init__.py con lógica genera conflictos de importación.
# src/mi_paquete/__init__.py
import pandas as pd

def procesar_datos(df):
    return df.dropna()  # ← Esta función pertenece a core.py, no aquí.
```

**3. Archivos de configuración paralelos:**

```
# ❌ Configuración fragmentada en múltiples archivos.
mi-proyecto/
├── setup.cfg       # ← Redundante con pyproject.toml
├── .flake8         # ← Va dentro de pyproject.toml
├── mypy.ini        # ← Va dentro de pyproject.toml
└── pyproject.toml
```

> [!CAUTION]
> Tener `setup.py` junto con `pyproject.toml` puede causar comportamientos impredecibles. Si se encuentra un proyecto con esta coexistencia, debe migrarse completamente a `pyproject.toml` antes de continuar el desarrollo.

---

## ⚙️ Configuración de `pyproject.toml`

> [!NOTE]
> Esta sección es de referencia para quienes configuran o modifican el proyecto. Si sos colaborador externo o recién te sumás al equipo, no necesitás entender cada detalle — basta con respetar la estructura de carpetas del árbol de arriba y no crear archivos de configuración nuevos.

La organización gestiona las dependencias con **Poetry**. El siguiente es el template base aprobado:

```toml
[tool.poetry]
name = "mi-paquete"
version = "0.1.0"
description = "Descripción concisa del propósito del paquete."
authors = [
    {name = "tu_nombre", email = "equipo@organizacion.com"}
]
readme = "README.md"
requires-python = ">=3.10"

# ── Dependencias de producción ───────────────────────────
# Lo que el programa necesita para funcionar.
dependencies = [
    "libreria1",
    "libreria2",
]

# ── Dependencias de desarrollo ───────────────────────────
# Herramientas que usa el equipo para desarrollar el proyecto.
# No se instalan cuando alguien usa el paquete en producción.
[tool.poetry.group.dev.dependencies]
ruff = "^0.4"           # Linter y formateador de código
pytest = "^8.0"         # Correr pruebas
pytest-cov = "^5.0"     # Medir cobertura de pruebas
mypy = "^1.10"          # Verificar tipos

[project.urls]
source = "enlace_github"

[tool.setuptools]
packages = {find = {}}
```

> [!TIP]
> ¿Nunca usaste Poetry? Consultá con el líder técnico del equipo antes de modificar este archivo. Un cambio incorrecto en las dependencias puede romper el entorno de todos los colaboradores.

---

## 📎 Atribuciones

Íconos por <a href="https://icons8.com">Icons8</a>