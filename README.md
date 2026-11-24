Assessment 3 - Acuerdo de trabajo del grupo

**NLP - Sentiment Analysis con Amazon Reviews y Hugging Face**

Integrantes: Carlos | Heidy | Renato | Oscar

| **PROPÓSITO DE ESTE DOCUMENTO**Alinear al grupo antes de comenzar el desarrollo: qué exige el Assessment 3, qué enfoque técnico proponemos, cómo se divide el trabajo y qué decisiones todavía deben confirmarse. No sustituye el Assessment Brief; funciona como acuerdo operativo del equipo. |
| --- |
# 1. Objetivo del proyecto
Construir un sistema de **Natural Language Processing (NLP)** capaz de clasificar reviews de Amazon como **positivas o negativas**. El sistema debe entrenarse con los datos etiquetados proporcionados, evaluarse con datos separados y ofrecer una forma sencilla de introducir una review nueva y obtener una predicción.

Entrega grupal: código del proyecto.

Entrega grupal: video/presentación de 10-15 minutos, con participación de todos.

Entrega individual: informe de contribución de 250 palabras (±10%) y porcentajes de contribución del equipo que sumen 100%.

El brief también exige considerar aspectos éticos y utilizar Git/version control para evidenciar colaboración.
# 2. Datos con los que trabajaremos
El dataset entregado contiene cuatro dominios de productos y un conjunto etiquetado equilibrado:

| **Domain** | **Positive** | **Negative** | **Total etiquetado** |
| --- | --- | --- | --- |
| Books | 1,000 | 1,000 | 2,000 |
| DVD | 1,000 | 1,000 | 2,000 |
| Electronics | 1,000 | 1,000 | 2,000 |
| Kitchen & Housewares | 1,000 | 1,000 | 2,000 |
| **TOTAL** | **4,000** | **4,000** | **8,000** |

**Alcance inicial:** trabajaremos con las 8,000 reviews etiquetadas. Los datos unlabeled no forman parte del entrenamiento principal en esta primera versión, salvo que el equipo decida posteriormente justificar un uso específico.

# 3. Enfoque técnico acordado/propuesto


| **ACORDADO**El proyecto será NLP Sentiment Analysis. Se utilizará Hugging Face como ecosistema recomendado por el profesor. El modelo se entrenará/adaptará con nuestro dataset y no se limitará a usar un pipeline preentrenado sin fine-tuning. |
| --- |


| **TODAVÍA POR DECIDIR**El modelo preentrenado exacto (por ejemplo, una arquitectura Transformer adecuada para sequence classification), el split definitivo Train/Validation/Test, la longitud máxima de secuencia y los hiperparámetros. Estas decisiones deben justificarse con el EDA, recursos disponibles y resultados de validación. |
| --- |
**Flujo de trabajo propuesto:**

1.  Carga de datos

2.  Inspección inicial + EDA

3.  Cleaning + duplicados + outliers

4.  Train / Validation / Test

5.  Hugging Face tokenizer

6.  Padding / truncation

7.  Modelo preentrenado + fine-tuning

8.  Evaluación + error analysis

9.  Inference

10.  Web app / interfaz sencilla

# 4. División principal del trabajo
Cada integrante tendrá una responsabilidad principal, pero todos deben entender el flujo completo y revisar el trabajo integrado del grupo.

| **Persona** | **Responsabilidad principal** | **Entregables / tareas clave** | **Pregunta que debe poder explicar** |
| --- | --- | --- | --- |
| **Carlos** | Data + EDA | Carga y organización de datos; dominios; balance; duplicados; longitudes; palabras/bigrams frecuentes; recomendaciones de cleaning/outliers. | ¿Qué datos tenemos, qué problemas presentan y qué decisiones se justifican con el EDA? |
| **Heidy** | Preprocessing + Hugging Face tokenizer | Split Train/Validation/Test; tokenizer; input_ids/attention_mask; padding/truncation; preparación de datasets para training. | ¿Cómo convertimos las reviews en entradas válidas para el modelo sin contaminar el test set? |
| **Renato** | Selección del modelo + fine-tuning | Seleccionar un modelo apropiado de Hugging Face; configurar training; epochs, batch size y learning rate; validar; guardar el mejor modelo. | ¿Por qué elegimos este modelo y qué significa fine-tuning en nuestro problema? |
| **Oscar** | Evaluation + error analysis + app | Accuracy, precision, recall, F1, confusion matrix; análisis de errores; función de predicción; interfaz web sencilla; integración de resultados. | ¿Cómo sabemos si el modelo generaliza y cómo convertimos la predicción en un sistema utilizable? |
# 5. Responsabilidades compartidas
GitHub/Git: cada integrante debe realizar commits propios y comprensibles. Evitar que una sola persona suba el trabajo de todos.

Testing e integración: cada parte debe entregarse funcional y luego revisarse en conjunto antes del merge final.

Ética y limitaciones: todos deben aportar hallazgos relacionados con su sección (sesgos del dataset, ambigüedad, truncation, pre-trained model bias, misclassification, etc.).

Presentación: todos participan y deben poder explicar el proyecto completo, aunque cada uno lidere su sección.

Documentación: decisiones técnicas importantes deben registrar una razón (no “porque el código lo hacía”).
# 6. Organización sugerida en GitHub
**Ramas de trabajo sugeridas:**

carlos-data-eda

heidy-hf-preprocessing

renato-model-training

oscar-evaluation-app

Flujo recomendado: branch -> commits descriptivos -> revisión/pull request -> merge a main.
# 7. Estructura inicial de la presentación


| **Persona** | **Sección principal de presentación** |
| --- | --- |
| **Carlos** | Problema, dataset, domains, EDA y decisiones de limpieza. |
| **Heidy** | Preprocessing, split, tokenizer, padding/truncation y preparación de entradas. |
| **Renato** | Modelo elegido, arquitectura general, fine-tuning, training y decisiones de hiperparámetros. |
| **Oscar** | Resultados, confusion matrix, error analysis, demo/inference, limitaciones y conclusión. |

**Nota:** ethical considerations deben aparecer integradas en la presentación, no como un comentario superficial al final.

# 8. Próximos pasos inmediatos
1.  Confirmar este reparto o proponer cambios antes de comenzar ramas grandes de código.

2.  Crear/organizar el repositorio de GitHub y asegurar que los cuatro tengan acceso.

3.  Carlos inicia EDA y produce un resumen compartido de hallazgos y recomendaciones.

4.  Con el EDA, el grupo decide split, reglas de outliers, max sequence length y criterios de preprocessing.

5.  Heidy prepara el pipeline de tokenizer/datasets; Renato selecciona y prueba el modelo; Oscar prepara el esquema de evaluación e interfaz.

6.  Reunión corta de integración: revisar métricas de validación, errores y decidir si hace falta una segunda iteración de training.
# 9. Límites de alcance para evitar trabajo innecesario
No construir una base de datos, login, frontend complejo o infraestructura cloud salvo que aparezca una necesidad real.

No entrenar muchos modelos por “probar de todo”. Comparar sólo opciones justificadas si hace falta.

No usar las reviews unlabeled por defecto: primero completar correctamente el pipeline supervisado exigido.

No optimizar únicamente accuracy: también revisar precision, recall, F1, confusion matrix y errores reales.

No tocar el test set para elegir hiperparámetros; las decisiones de ajuste deben basarse en training/validation.

# 10. Confirmación del equipo
Cada integrante puede responder en Teams “De acuerdo” o proponer cambios concretos. Una vez confirmada la versión final, este documento funciona como referencia común para repartir tareas y explicar contribuciones.

| **Integrante** | **Confirmación** | **Cambios / comentarios** |
| --- | --- | --- |
| **Carlos** | De acuerdo / Pendiente |  |
| **Heidy** | De acuerdo / Pendiente |  |
| **Renato** | De acuerdo / Pendiente |  |
| **Oscar** | De acuerdo / Pendiente |  |

**Base del documento:** ISY503 Assessment 3 Brief y dataset proporcionado para el proyecto. La recomendación de utilizar Hugging Face proviene de la orientación indicada por el profesor al grupo.