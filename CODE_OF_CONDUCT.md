# 🤝 Código de Conducta y Contribución

Toda persona que interactúe con los repositorios del Neuro-IA LAB —sea miembro del laboratorio o colaborador externo— debe hacerlo con respeto, rigor técnico y siguiendo los estándares definidos en esta guía.

---

## 🎯 Objetivo y Contexto

> [!NOTE]
> Este documento no busca imponer restricciones innecesarias, sino establecer un marco común que permita que personas con distintos niveles de experiencia y distintos orígenes institucionales trabajen juntas de forma ordenada, respetuosa y productiva.

El Neuro-IA LAB es un espacio académico y de investigación. Sus repositorios son el reflejo público del trabajo del laboratorio y, como tal, deben mantenerse con el mismo nivel de rigor que se exige en cualquier producción científica. Este código aplica a todos los espacios de interacción vinculados a los repositorios de la organización: código, Issues, Pull Requests, comentarios de revisión y cualquier otro canal de comunicación asociado.

---

## 🌟 Reglas de Oro

> [!IMPORTANT]
> Las siguientes reglas aplican sin excepción a toda persona que interactúe con cualquier repositorio de la organización, independientemente de su rol, nivel de experiencia o filiación institucional.

* **Respeto ante todo:** Las interacciones deben ser respetuosas y constructivas. Las críticas se dirigen al código o a las ideas, nunca a las personas. No se toleran comentarios ofensivos, discriminatorios ni descalificaciones de ningún tipo.

* **Rigor y honestidad:** Reportar un error o proponer un cambio requiere contexto suficiente para que pueda ser entendido y reproducido. La información vaga o incompleta no aporta valor y demora la resolución.

* **Comunicación en español:** Toda interacción dentro de los repositorios de la organización —Issues, Pull Requests, comentarios y commits— debe realizarse en español, salvo que el contexto técnico lo haga imprescindible en otro idioma.

* **Cumplimiento de los estándares organizacionales:** Toda contribución debe respetar los estándares definidos por la organización: estructura de proyectos, Conventional Commits, reglas de Pull Request y convención de ramas. Contribuir sin leer estos estándares previamente no es una justificación válida para incumplirlos.

* **Apertura al aprendizaje:** Este es un entorno académico con colaboradores de distintos niveles. Se espera disposición para recibir retroalimentación y para ayudar a quienes tienen menos experiencia.

---

## 👥 Roles y Alcance

Este código distingue dos tipos de colaboradores, cada uno con un proceso de incorporación distinto:

| Rol | Quién es | Proceso |
|:---|:---|:---|
| 👤 **Miembro del laboratorio** | Estudiante, investigador o director perteneciente a la institución | Incorporación directa, coordinada con el director del laboratorio |
| 🌐 **Colaborador externo** | Persona ajena a la institución que desea aportar en algún repositorio | Debe contactar al director del laboratorio antes de realizar cualquier contribución |

> [!IMPORTANT]
> La incorporación de colaboradores externos es una decisión institucional que corresponde exclusivamente al director del laboratorio. No se aceptan contribuciones externas en repositorios de la organización sin autorización previa explícita.

---

## 🐛 Issues

### ¿Qué es un Issue?

Un Issue es el mecanismo formal para reportar un problema, proponer una mejora o plantear una pregunta técnica sobre un repositorio. Es el punto de partida de cualquier cambio: antes de abrir una rama o un Pull Request, debe existir un Issue que justifique ese trabajo.

Pensalo como el acta de una reunión: queda registrado qué se detectó, quién lo detectó, cuándo y qué se decidió hacer al respecto.

### ¿Cuándo abrir un Issue?

* Se detectó un error o comportamiento inesperado en el código.

* Se quiere proponer una mejora, nueva funcionalidad o refactor.

* Hay una pregunta técnica que afecta la dirección del proyecto y requiere discusión.

* Se va a iniciar trabajo nuevo que no estaba planificado previamente.

> [!NOTE]
> Los Issues no son el canal para consultas rápidas o dudas generales sobre programación. Para eso, usar los canales de comunicación directa del laboratorio.

### 🌟 Reglas para Issues

* **Un Issue, un tema:** Cada Issue debe abordar un único problema o propuesta. Mezclar varios temas dificulta el seguimiento y la resolución.

* **Título descriptivo:** El título debe resumir el problema o propuesta en una línea. Evitar títulos genéricos como "Error" o "Mejora".

* **Usar las plantillas disponibles:** Si el repositorio cuenta con plantillas de Issue, deben utilizarse obligatoriamente. Están diseñadas para recopilar la información mínima necesaria para entender y reproducir el problema.

* **Asignar etiquetas:** Usar las etiquetas (*labels*) disponibles en el repositorio para categorizar el Issue (`bug`, `enhancement`, `question`, etc.).

* **Vincular al trabajo:** Si el Issue da origen a un Pull Request, debe vincularse usando las palabras clave de cierre automático en el PR. (Ver [Pull Requests](./PR_RULES.md))

---

## 🛠️ Implementación y Ejemplos

### ✅ Prácticas correctas

**Issue de reporte de bug:**

```markdown
## 🐛 Descripción del problema
Al llamar a `get_data(channels=[0, 1], t_start=1.0, t_end=2.0)` con un
valor de `t_end` mayor al largo de la señal, el método lanza un
`IndexError` en lugar de recortar al último sample disponible.

## 🔁 Pasos para reproducir
1. Instanciar `RawSignal` con un archivo de 10 segundos.
2. Llamar a `get_data(t_end=15.0)`.
3. Observar el traceback.

## 🧪 Comportamiento esperado
El método debería retornar los datos hasta el último sample disponible
y emitir un `Warning` indicando que `t_end` fue recortado.

## 💻 Entorno
- Python 3.11
- Rama: `feat/clase-raw-signal`
```

**Issue de propuesta de mejora:**

```markdown
## 💡 Propuesta
Agregar un parámetro `return_times` (bool, default `False`) al método
`get_data()` para que opcionalmente retorne el vector de tiempos
correspondiente al segmento extraído.

## 🎯 Motivación
Actualmente, quien necesita el vector de tiempos debe calcularlo
manualmente fuera de la clase. Incluirlo en el método elimina código
repetido en todos los scripts de análisis.
```

---

### ❌ Prácticas desaconsejadas

```markdown
# ❌ Título genérico sin contexto.
Título: "Bug en el código"

# ❌ Sin información para reproducir el problema.
Descripción: "La función no funciona bien con algunos datos."

# ❌ Múltiples temas en un solo Issue.
Descripción: "El método get_data() falla con índices negativos y además
habría que agregarle el parámetro return_times y también cambiar el
nombre de la clase RawSignal por Signal."

# ❌ Tono inapropiado en la descripción.
Descripción: "Alguien rompió get_data(), esto está muy mal hecho."
```

> [!CAUTION]
> Un Issue con información insuficiente será cerrado y se solicitará que se reabra con el contexto necesario. Esto no es un rechazo a la contribución, sino una garantía de que el trabajo posterior sea útil y trazable.

---

## ⚠️ Comportamientos inaceptables

Los siguientes comportamientos constituyen una violación de este código y pueden resultar en la revocación del acceso a los repositorios de la organización:

* Lenguaje o imágenes ofensivas, discriminatorias o de acoso en cualquier espacio de interacción.

* Comentarios que descalifiquen el trabajo o la capacidad de otra persona.

* Publicación de información privada de otros colaboradores sin su consentimiento.

* Contribuciones deliberadamente incorrectas o que introduzcan código malicioso.

---

## 📬 Reporte de Incidencias

Si experimentás o presenciás un comportamiento que viola este código, reportalo directamente al director del laboratorio por los canales institucionales. Toda comunicación será tratada con confidencialidad.

---

## 📎 Atribuciones

Este código de conducta está basado en el [Contributor Covenant](https://www.contributor-covenant.org/), versión 2.1, adaptado al contexto del Neuro-IA LAB.
