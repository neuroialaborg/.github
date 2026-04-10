# 🤝 Guía de Contribución

Esta guía establece el cómo colaborar en los repositorios del laboratorio, protegiendo la integridad académica de las investigaciones en curso mientras fomentamos el desarrollo Open Source.

---

## 🎯 Objetivo y Contexto

Los repositorios de este laboratorio (la organización) tiene una doble naturaleza: por un lado, son herramientas Open Source diseñadas para la comunidad; por otro, son artefactos científicos que sustentan tesis, investigaciones y publicaciones académicas. 

Esta guía busca equilibrar ambos mundos. Queremos que cualquier persona, desde un estudiante recién ingresado hasta un investigador externo, pueda proponer mejoras sin temor a romper el trabajo de grado de un compañero

---

## 🌟 Reglas de Oro

* **Respeta el Estado del Proyecto (Issue First):** Nunca comiences a escribir código para una nueva funcionalidad (feature) sin antes haber abierto un Issue para discutirlo. Si el proyecto es una tesis activa, tu tiempo podría desperdiciarse si el cambio altera los resultados de la investigación.
* **Cero Sorpresas:** Las contribuciones deben alinearse con el roadmap del laboratorio. No refactorices arquitecturas completas ni introduzcas nuevas dependencias pesadas sin validación previa del equipo de investigación.
* **Aplica el Estándar de PRs:** Toda contribución debe cumplir con la "Regla de las Tres Patas" (Código, Tests y Documentación). Revisa nuestra [Guía de Pull Requests](./PR_RULES.md) antes de solicitar una revisión.

---

## 🛠️ Implementación y Ejemplos

### ✅ Prácticas correctas

Para asegurar que tu contribución sea útil y rápidamente aceptada, sigue este flujo de trabajo:

1. **Verifica el contexto en el `README.md`:** Busca la sección de "Estado del Proyecto" para saber en qué fase se encuentra el repositorio:
   * 🛡️ **Investigación Activa / Tesis:** El código está siendo utilizado para un *paper* o evaluación. **Solo abre PRs para reportar bugs críticos o corregir documentación.** No propongas nuevas funcionalidades.
   * 🌐 **Open Source (Estable):** El proyecto está abierto a todo tipo de mejoras, optimizaciones y nuevas características.

2. **Abre un Issue Descriptivo:**
   Si tienes una idea, comunícala claramente antes de programar:
   > **[Feature] Reemplazar pandas por polars para optimizar rendimiento**
   > **Contexto:** Noté que el procesamiento de las señales EEG toma 45 min.
   > **Propuesta:** Si el proyecto está en fase Open Source, me ofrezco a reescribir este módulo usando `polars`. ¿Están de acuerdo con añadir esta dependencia?

3. **Crea Ramas Semánticas:**
   Nombra tus ramas indicando tu intención y el Issue que resuelves: `fix/issue-12-filtro-ruido` o `feat/exportar-pdf`.

---

### ❌ Prácticas desaconsejadas

Evita estos comportamientos, ya que suelen resultar en PRs rechazados y frustración para ambas partes:

> [!WARNING]
> **"PR Ninja" (Desarrollo sin comunicación)**
> Aparecer de la nada con un Pull Request de 1500 líneas de código que cambia toda la estructura del proyecto, sin haber abierto un Issue para preguntar si el autor de la tesis estaba de acuerdo con esa reestructuración.



> [!WARNING]
> **Ignorar el contexto científico**
> Cambiar una fórmula matemática o un algoritmo base simplemente porque "el código queda más corto o corre más rápido", sin entender que la investigación original necesitaba exactamente ese método para ser comparable con otra literatura.

---

## 🚀 ¿Cómo empezar? (Primeros pasos)

Si eres un estudiante nuevo en el laboratorio o un externo buscando cómo aportar:
1. Ve a la pestaña de **Issues** del repositorio.
2. Filtra por las etiquetas `good first issue` o `documentation`. Son tareas aisladas, seguras y perfectas para familiarizarse con la arquitectura del proyecto sin riesgo.
3. Comenta en el Issue: *"Me gustaría tomar esta tarea"*, espera a ser asignado, ¡y comienza a programar!


