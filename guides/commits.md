# 📸 Commits
Adoptamos Conventional Commits para automatizar el versionado, facilitar la revisión de código y generar un historial (changelog) claro y trazable.

---

## 🎯 Objetivo y Contexto

> [!NOTE]
Este estándar se adopta para generar un historial de repositorio explícito y predecible. Al estructurar nuestros mensajes, eliminamos la ambigüedad, facilitamos el *onboarding* de nuevos miembros y permitimos que cualquier contribuyente entienda exactamente qué cambió y por qué, sin necesidad de leer todo el código modificado.

---

## 🌟 Reglas

* **Atomicidad:** Cada commit debe corresponder a una única tarea lógica realizada. Si se arregla un bug y se agrega una funcionalidad, son dos commits distintos.
* **Nada de commits vacíos:** Evitar mensajes como "fix", "ahora sí" o "wip". Si se comete un error en el commit anterior, utilizar `git commit --amend` para sobreescribirlo en lugar de ensuciar el historial.
* **Formato estricto de texto:** Los commits no deben terminar en punto final ni usar puntos suspensivos. La descripción debe escribirse en **modo imperativo** (ej. "agrega", "corrige", no "agregado" o "añadiendo").
* **Regla 50/72 (Límites por línea):** La primera línea (título corto) no debe superar los **50 caracteres**. Si se utiliza el cuerpo (*body*), **ninguna línea individual** debe superar los **72 caracteres** (se debe presionar 'Enter' para hacer un salto de línea manual). El cuerpo puede tener las líneas que sean necesarias, siempre que ninguna exceda ese ancho. Esto asegura su correcta lectura en terminales.

---

## 🛠️ Implementación
La estructura de commit a utilizar, dada la adopción de Conventional Commits es:

```bash
<type>(scope): <description>

[optional body]

[optional footer(s)]
```

### 1. Type
Debe ir siempre en minúsculas. Indica la intención del cambio:
 
| Tipo | Intención | Ejemplo de uso |
| :---: | :---: | :---: |
| ✨ **`feat`** | Añade una nueva funcionalidad. | `feat(api): agrega endpoint de login` |
| 🐛 **`fix`** | Soluciona un error o bug. | `fix(eeg): corrige desbordamiento de memoria` |
| ♻️ **`refactor`** | Modifica el código sin añadir funcionalidades ni corregir errores. | `refactor: simplifica bucle de validación` |
| 🧪 **`test`** | Añade o corrige pruebas automáticas. | `test(auth): añade casos para token expirado` |
| 📝 **`docs`** | Cambios exclusivos en la documentación. | `docs: actualiza guía de instalación` |
| 🔧 **`chore`** | Tareas de mantenimiento o configuración (no afecta producción). | `chore: actualiza dependencias de pip` |


### 2. Scope, Description y Body
<div class="card blue">

**📦 Scope (Alcance — Opcional):** Va entre paréntesis `()`. Indica el módulo, componente o carpeta afectada (ej. `(api)`, `(ui)`, `(eeg)`).

</div>

<div class="admonition tip">
  <div class="admonition-icon">💡</div>
  <div class="admonition-body">
    <strong>Tip</strong>
    Si el cambio afecta a todo el proyecto de manera global, se debe omitir el scope.
  </div>
</div>

<div class="card blue">

**✍️ Description (Descripción):** Breve resumen de lo implementado. Conciso y siempre en imperativo (como si se estuviera dando una orden al código).

**📖 Body (Cuerpo — Opcional):** Separado de la descripción por una línea en blanco. Aquí se explica el *porqué* del cambio y no solo el *cómo*. Es el lugar ideal para justificar decisiones técnicas o comparar el comportamiento anterior con el nuevo.

</div>

### 3. Footer
El pie del commit se coloca al final del mensaje. Sirve exclusivamente para añadir metadatos y cumple dos propósitos principales:

**A. Cierre automático de Issues (Tickets):**
GitHub analiza el texto de los commits. Al utilizar ciertas palabras clave seguidas del número de un Issue (ej. `#89`), la plataforma genera un enlace directo y **cierra el ticket automáticamente** una vez que el código se fusiona con la rama principal. 

<div class="card green">

**Palabras clave soportadas por GitHub:**

| Keyword | Uso recomendado |
|:---:|:---:|
| `Closes #ID` | Funcionalidades nuevas o tareas generales |
| `Fixes #ID` | Cuando el Issue reporta un error o bug |
| `Resolves #ID` | Alternativa de uso general |

</div>

**B. Alertas de Ruptura (Breaking Changes):**
>[!CAUTION]
Si el commit introduce un cambio que rompe la compatibilidad con versiones anteriores (por ejemplo, la modificación del nombre de una función), se debe indicar explícitamente. Esto se realiza escribiendo `BREAKING CHANGE:` seguido de un espacio y la explicación detallada de la modificación.

---

## Ejemplo de Implementación

### ✅ Buenas prácticas
Para commits completos con cuerpo y pie, se recomienda omitir el flag `-m` para que Git abra el editor de texto configurado (Vim, Nano, VSCode, etc.):

**1. Commits completos (Recomendado para funcionalidades y errores complejos):**
Para commits que requieren cuerpo explicativo y pie, se recomienda omitir el flag `-m` para que Git abra el editor de texto configurado (VSCode):
```bash
git commit
```

```plaintext
feat(eeg): agrega filtro paso banda 1-40Hz

Implementa un filtro Butterworth de 4to orden para eliminar
el ruido de línea base y los artefactos musculares. Esto
mejora la relación señal-ruido antes de pasar a la etapa 
de extracción de características.

Se optó por este filtro IIR en lugar del FIR anterior para 
reducir la latencia en tiempo real durante las capturas.

Closes #89
```

**2. Commits rápidos (Una sola línea):**
Para cambios menores o evidentes que no requieren una explicación extendida en el cuerpo (como actualización de dependencias, correcciones tipográficas o refactors simples), es completamente válido utilizar el flag `-m`. Se debe respetar el formato y el límite de 50 caracteres:

```bash
git commit -m "chore(docs): actualiza enlaces rotos en el README"
```

### ❌ Prácticas desaconsejadas

**1. En commits rápidos (Una sola línea):**
Se deben evitar mensajes sin formato explícito, que rompen la regla de atomicidad (varias tareas mezcladas) o que son demasiado vagos para aportar contexto al historial.

```bash
# ERROR: Mensaje genérico, sin tipo, sin scope y sin formato imperativo.
git commit -m "actualización de scripts y corrección de errores"

# ERROR: No es atómico (mezcla una funcionalidad y un refactor en el mismo commit).
git commit -m "feat(ui): agrega gráfica y refactoriza módulo de carga"

# ERROR: Uso de verbos en pasado o gerundio en lugar de imperativo.
git commit -m "fix(eeg): corrigiendo el filtro que fallaba con valores nulos"
```
**2. En commits completos (Con cuerpo y pie):**
Se desaconseja omitir las líneas en blanco reglamentarias, exceder el límite de 72 caracteres por línea en el cuerpo, o utilizar el cuerpo para explicar el "cómo" (el código en sí) en lugar del "porqué" (la motivación).

```bash
# ERROR: Faltan las líneas en blanco separadoras entre cabecera, cuerpo y pie. 
# El cuerpo detalla el código paso a paso en lugar de la motivación arquitectónica, 
# y la línea del cuerpo excede por mucho el límite de 72 caracteres de ancho.
feat(auth): agrega validación de tokens
Se añade una condición if para comprobar que el token no sea nulo y luego se usa split() para separar el Bearer y validar la firma con la función verify_signature().
Closes #42
```
---

## ♻️ Cómo "Pisar" un Commit
Es muy común olvidar agregar un archivo o notar un typo (error tipográfico) justo después de hacer commit. En lugar de crear un nuevo commit que diga `fix: ahora sí` o `chore: olvidé un archivo`, utilizamos el comando ***amend*** para fusionar esos cambios con el último commit.

### 1. Olvidé agregar un archivo (o corregí un error menor)

Si el mensaje de tu último commit sigue siendo válido, simplemente añade los cambios y usa la bandera `--no-edit`
```plaintext
    git add archivo_olvidado.py
    git commit --amend --no-edit
```

### 2. Me equivoqué en el mensaje del commit

Si los archivos están bien pero el mensaje no cumple el estándar (ej. olvidaste el scope), puedes reescribirlo así:
```plaintext
    git commit --amend -m "fix(auth): corrige validación de token"
```

> [!IMPORTANT]
**Regla de Oro para reescribir la historia** <br>
Solo debes hacer *amend* en commits que aún no has subido (push), o en tu propia rama personal de Pull Request. Si ya habías hecho push a tu rama de PR, deberás forzar la subida usando git push --force-with-lease (esta bandera es más segura que --force porque evita sobreescribir el trabajo de otros). 

> [!WARNING]
***¡Jamás reescribas el historial de la rama main/master (rama principal)!***