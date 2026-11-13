# Clasificación de la Forma Reportada en Avistamientos de OVNIS en Estados Unidos mediante Aprendizaje Automático

# MODELOS EVALUADOS CON EL DATASET LIMPIO

**Alumno:** Ariel Tuñon

**Repositorio:** [Aprendizaje_automatico_parcial_2026](https://github.com/arieltunon74/Aprendizaje_automatico_parcial_2026)

---

# MODELOS EVALUADOS CON EL DATASET LIMPIO

**Regresión Logística Multiclase o Multinomial**: para predecir la forma del OVNI (shape), 
permitiendo evaluar la probabilidad de pertenencia a cada clase e interpretar mediante sus 
coeficientes el impacto de las variables temporales, geográficas, de duración de cada categoría. 


**Árbol de Decisión**: Se selecciona este modelo supervisado debido a su capacidad para ofrecer.
reglas de decisión claras y transparentes en la clasificación de las formas de los OVNIs (shape).


**K-Nearest Neighbors (KNN)**:  Se puede implementar el modelo de K-Nearest Neighbors (KNN) 
como clasificador basado en distancias para predecir la forma del OVNI (shape), asignando cada 
categoría según la clase mayoritaria de sus instancias más cercanas en el espacio vectorial de 
características 

## 📋 Descripción del Proyecto

Este proyecto tiene como objetivo predecir y clasificar la forma reportada de objetos voladores no identificados (`shape_grouped`) en avistamientos ocurridos en Estados Unidos, utilizando técnicas de **Aprendizaje Automático Supervisado** (clasificación multiclase).

A partir de un dataset previamente limpiado y estructurado, se diseñó un flujo de trabajo en Python que previene el *Data Leakage* (fuga de datos), evalúa distintos algoritmos de clasificación y selecciona el modelo con mejor desempeño para la tarea.

---

## Conjunto de Datos (Dataset)

* **Fuente:** `data/processed/dataset_procesado.csv` (delimitado por `;`).
* **Dimensiones:** 79,695 registros y 25 columnas originales.
* **Variable Objetivo ($y$):** `shape_grouped` (7 clases objetivo: *Circle, Disk, Fireball, Light, Other, Sphere, Triangle*).

### Variables de Entrada Seleccionadas ($X$)


Para evitar la fuga de datos (*data leakage*), se excluyeron variables derivadas directamente del objetivo o descripciones textuales reveladoras, conservando únicamente atributos contextuales, espaciales y temporales:

* **Numéricas (5):** `duration_seconds`, `year`, `month`, `day_of_week`, `hour`.
* **Ordinales (2):** 
  * `Duracion_clasificacion` (*Muy corto, Corto, Medio, Largo*).
  * `decade` (*1960s, 1970s, 1980s, 1990s, 2000s, 2010s*).
* **Nominales (6):** `state_grouped`, `us_region`, `north_season`, `time_of_day`, `day_category`, `is_weekend`.

En el proyecto de clasificación de formas de OVNIs, las variables excluidas para evitar la fuga de datos (data leakage) y el sobreajuste incluyen principalmente las siguientes:

La variable original `shape`: Fue descartada por tratarse de la fuente directa de la cual se derivó la variable objetivo (`shape_grouped`), lo que constituiría una fuga directa de la etiqueta a predecir.

Fechas de publicación posteriores (`posted_date`, `posted_year`, `posted_month`, `posted_dayofweek`): Excluidas porque la fecha en que se reporta o publica un avistamiento en la base de datos ocurre después de este, representando información futura que no estaría disponible en un escenario de predicción real.

Versiones redundantes de duración (duration en formato de texto o variantes previas): Se descartaron para evitar duplicidad, conservando únicamente la variable numérica estandarizada (`duration_seconds`).

Variables de alta cardinalidad específica (`city`): Se omitieron campos como la ciudad exacta para evitar un sobreajuste (overfitting) severo, priorizando en su lugar atributos espaciales y contextuales más amplios como `state_grouped` y `us_region`.

Esta selección rigurosa garantiza que el modelo aprenda a partir de patrones temporales, espaciales y cuantitativos reales (`duration_seconds`, años, estaciones, etc.) y no de indicios directos de la respuesta o información del futuro.

---

## ⚙️ Metodología y Preprocesamiento

El procesamiento de datos se implementó mediante `Pipeline` y `ColumnTransformer` de `scikit-learn` para garantizar la reproducibilidad y evitar la contaminación entre los conjuntos de entrenamiento y prueba:

1. **División Estratificada:** Separación en **80% Entrenamiento** (63,756 registros) y **20% Prueba** (15,939 registros) manteniendo la proporción original de las clases (`stratify=y`, `random_state=42`).

2. **Transformación por tipo de dato** (ajustada exclusivamente sobre `X_train`):
   * **Numéricas:** Imputación por mediana (`SimpleImputer`) + Estandarización (`StandardScaler`).
   * **Ordinales:** Imputación por moda + Codificación ordinal respetando la jerarquía (`OrdinalEncoder`).
   * **Nominales:** Imputación por moda + Codificación *One-Hot* (`OneHotEncoder`).
   * *Resultado tras el preprocesamiento:* Matriz de **38 características**.

---

## Modelos Evaluados y Selección

Debido al fuerte desbalance natural de las clases en los reportes (donde predominan las categorías *Other* y *Light*), se evaluaron distintos enfoques de clasificación comparando su *Accuracy*, *F1-Score* y Matrices de Confusión:

1. **Regresión Logística Multinomial (Modelo Base Lineal):**
   * *Accuracy:* **32.25%**
   * *Observación:* Al ser un modelo lineal, no logra capturar relaciones complejas y concentra casi todas sus predicciones en las clases mayoritarias (*Other* y *Light*), obteniendo `0.00` de *recall* en el resto.


2. **Árbol de Decisión (`max_depth=8`):**
   * *Accuracy:* **32.83%**
   * *Observación:* Mejora ligeramente la precisión y comienza a discriminar patrones no lineales en clases minoritarias (*Fireball*, *Disk*, *Circle*, *Triangle*), aunque con capacidad limitada por tratarse de un único árbol podado.


3. **🏆 Random Forest (Modelo Seleccionado):**
   * **Justificación de la elección:** Se seleccionó **Random Forest** como modelo final del proyecto. Al ser un método de ensamble (*bagging*) compuesto por múltiples árboles de decisión entrenados sobre subconjuntos aleatorios de datos y características, reduce drásticamente la varianza frente a un árbol individual, maneja de forma óptima las interacciones no lineales entre variables geográficas y temporales, y ofrece mayor estabilidad y capacidad de generalización sobre un dataset de casi 80,000 registros.


---

## Cómo Ejecutar el Proyecto

1. Clona este repositorio en tu máquina local:
   ```bash
   git clone [https://github.com/arieltunon74/Aprendizaje_automatico_parcial_2026.git](https://github.com/arieltunon74/Aprendizaje_automatico_parcial_2026.git)
   cd Aprendizaje_automatico_parcial_2026