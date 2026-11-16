
# Clasificación de la forma reportada en avistamientos de OVNIS en Estados Unidos mediante aprendizaje automático.

## Objetivo General

**Aplicar técnicas de Aprendizaje Automático supervisado, mediante un modelo de clasificación multiclase, para intentar identificar la categoría correspondiente a la forma reportada en los registros de avistamientos.**

Se busca identificar patrones y evaluar la capacidad de los modelos de aprendizaje automático para predecir la forma reportada del objeto (shape) según las características disponibles.

**Clasificación**: el modelo asigna una categoría
**Predicción**: el modelo estima cuál es la categoría más probable según los patrones aprendidos
**La variable objetivo (target)**: shape_grouped → forma reportada del objeto según los testigos - agrupada.

Cabe aclarar que no anticipará cuándo o dónde ocurrirá un avistamiento; No identifica visualmente el objeto ni verifica qué era realmente.

---

## Objetivos Específicos

- Explorar y comprender el dataset de avistamientos identificando sus variables y tipos de datos. 
- Realizar una limpieza y transformación de los datos, tratando valores duplicados, ausentes y preparando las variables categóricas y numéricas.
- Analizar las características de los avistamientos, considerando variables como fecha, hora, ubicación, duración y forma reportada.
- Determinar las variables que pueden utilizarse como características (features) para realizar la clasificación.
- Construir diferentes modelos de clasificación y comparar su comportamiento mediante métricas apropiadas. 
- Evaluar la capacidad predictiva de los modelos de aprendizaje supervisado utilizando datos de entrenamiento y prueba.
- Analizar la importancia de las variables predictoras e identificar cuáles aportan en mayor medida a las predicciones realizadas por los modelos.

---

## Alcance del proyecto

El proyecto se centra en el análisis de datos de avistamientos de objetos voladores no identificados (UFO), utilizando el dataset NUFORC como fuente de información, con el propósito de evaluar la capacidad de distintos algoritmos de Aprendizaje Automático supervisado para clasificar la forma reportada de los objetos.

**Importante**: 

El modelo estaría aprendiendo a partir de reportes humanos registrados en NUFORC, no estaría identificando científicamente qué objetos son realmente OVNIS/ UFO/ UAP.

El modelo NO busca determinar la existencia de vida extraterrestre ni comprobar la naturaleza de los objetos observados.

---

## Tipo de problema


**Clasificación supervisada multiclase**


## Problema planteado para resolver con un modelo de aprendizaje automático supervisado

**¿Es posible clasificar los reportes de avistamientos de objetos voladores no identificados (UFO - OVNI - UAP) según la forma descrita por los testigos, utilizando sus características temporales, geográficas y de duración?**

---

## Acerca de las variables predictoras

Se trataran o unificarán según el caso, las variables como `occurred_date_time` que contengan día, mes, año , horas, minutos y que contengan ubicación geeográfica como `state` para generar otros tipos de variables para la implementación de los modelos, es decir que a partir de ellas se podrán generar nuevas características derivadas que permitan representar mejor la información y evaluar su utilidad para la implementación de los modelos de Aprendizaje Automático.

Se utilizarán como variables predictoras todas las variables disponibles en el conjunto de datos, excepto las variables `summary` y `details_url` que ambos contienen campos de texto con las descripciones de los testigos que vieron los OVNIS. EL PROCESAMIENTO DE DICHOS TEXTOS NO SERÁ TENIDO EN CUENTA, dentro del alcance de este proyecto, pues hay que implementar otros modelos de aprendizaje que no vimos en clase.

`posted_date` se conservará inicialmente para evaluar su posible utilidad en el desarrollo del modelo, es decir que su inclusión como variable predictora dependerá de los resultados del análisis exploratorio y de su relevancia para el objetivo de clasificación.
Las fechas están representadas como texto y podrían convertirse a un tipo temporal.

---

## Estado final del dataset después del preprocesamiento

Resultado del proceso de limpieza, transformación y preparación de los datos, con el objetivo de obtener un conjunto de datos consistente y adecuado para el desarrollo de modelos de Aprendizaje Automático.

Después del preprocesamiento, el dataset principal cuenta con 79,695 filas (instancias) y 25 columnas (16 columnas adicionales generadas principalmente mediante la transformación de variables numéricas en categóricas y la creación de nuevas características derivadas.)

Filtrando y haciendo foco de las observaciones en Estados Unidos, el dataset considera 79,695 filas

Asimismo, se realizó un análisis de las variables disponibles para determinar su utilidad como predictoras. Se decidió excluir summary y details_url, por tener valores en texto que no serán considerados en este proyecto.

Se contempló el tratamiento de variables temporales y geográficas. A partir de `occurred_date_time`, se podrán obtener características como año, mes, día, hora, día de la semana y estación del año. 

Por otra parte, se evaluó la distribución de las categorías de la variable objetivo `shape` y `shape_grouped`, con el propósito de identificar las categorías adecuadas para el problema de clasificación multiclase y definir su tratamiento según su frecuencia y representatividad.

---

# Metodología

El proyecto fue desarrollado siguiendo las etapas clásicas de un flujo de trabajo de Ciencia de Datos:

1. Obtención de datos.
2. Limpieza y preparación.
3. Integración de dataset.
4. Construcción de variables derivadas unificando datos.
5. Análisis exploratorio de datos.
6. Imputaciones (SimpleImputer), Escalados (StandardScaler)
7. Codificaciones (OrdinalEncoder y OneHotEncoder)
8. División de 80% para entrenamiento y 20% para prueba
9. Modelado de Random Forest - Entrenamiento del algoritmo de ensamblaje optimizado para clasificación multiclase.
10. Muestra de resultados.

---

# Modelo Utilizado

**Random Forest (con balance de clases)**

---

## Modelos de aprendizaje automático supervisados que se probaron pero no se implementaron: 

**Regresión Logística Multiclase o Multinomial**: para predecir la forma del OVNI (shape), 
permitiendo evaluar la probabilidad de pertenencia a cada clase.

**Árbol de Decisión**: Se selecciona este modelo supervisado debido a su capacidad para ofrecer 
reglas de decisión claras y transparentes en la clasificación de las formas de los OVNIs (shape).

**K-Nearest Neighbors (KNN)**:  Se probó el modelo de K-Nearest Neighbors (KNN) 
como clasificador basado en distancias para predecir la forma del OVNI (shape)

---

## Codificación de Variables Categóricas (Dataset procesado NUFORC)

**En base al dataset original:** NUFORC UFO Sightings - Data scraped from the National UFO reporting center – By Thaddeus Segura - (DbCL) v1.0

Una técnica que se intentará en los modelos es **One Hot Encoding (OHE)** consiste en convertir variables categóricas en vectores binarios ($0$ y $1$). Su uso óptimo requiere que las variables tengan **baja a moderada cardinalidad** (pocos valores únicos) para evitar el aumento excesivo de dimensiones (*curse of dimensionality*).

## Variables a realizar One Hot Encoding en el Notebook

Las siguientes variables del dataset presentan niveles de cardinalidad controlados y estructura categórica discreta ideal para ser codificadas mediante OHE:

| Variable | Tipo de Información | Razones de Inclusión | 
| ----- | ----- | ----- | 
| `state_grouped` | Geográfica agrupada | Agrupaciones territoriales de baja cardinalidad que aportan contexto espacial limpio. | 
| `us_region` | Geográfica por regiones | Divisiones macro-regionales (Norte, Sur, Este, Oeste, etc.) con muy pocos niveles. | 
| `north_season` | Temporal / Estacional | Representa las 4 estaciones del año en el hemisferio norte. | 
| `quarter_category` | Temporal / Trimestral | 4 categorías discretas (Q1, Q2, Q3, Q4). | 
| `month_category` | Temporal / Meses | Categorías mensuales discretas (12 niveles). | 
| `day_category` | Temporal / Día | Categorías correspondientes al momento o tipo de día. | 
| `time_of_day` | Temporal / Horaria | Franjas del día (Mañana, Tarde, Noche, Madrugada). | 

> **Nota sobre `state`:**: se intentará priorizar `state_grouped` o `us_region`.

## Variables EXCLUIDAS de One Hot Encoding

| Variable | Motivo de Exclusión | Técnica Alternativa Recomendada | 
| ----- | ----- | ----- | 
| `city` | Alta cardinalidad (miles de ciudades únicas). OHE crearía una matriz hiper-dispersa (*sparse matrix*) con riesgo severo de *overfitting*. | *Target Encoding*, *Frequency Encoding* o descarte. | 
| `duration_seconds` | Es una variable **numérica continua**, no categórica. | Escalado cuantitativo (`StandardScaler`, `MinMaxScaler`) o transformación logarítmica. | 
| `is_weekend` | Es una variable binaria intrínseca ($0/1$ o `True/False`). | No requiere transformación adicionales. |

**Se realiza Ordinal Encoder**

| `Duracion_clasificacion` | Duración del evento | Rangos cualitativos discretos de duración (Ej: Corta, Media, Larga). | 
| `duration_category_detailed` | Duración detallada | Rangos cualitativos ampliados pero disjuntos y limitados en número. | 

---
## Modelo aplicado:

**Random Forest**: Se implementa el modelo de Random Forest como algoritmo, combinando múltiples árboles de decisión 
independientes para capturar interacciones no lineales complejas y mitigar el riesgo de sobreajuste 
(overfitting) a partir de las variables temporales, geográficas y de duración.

---

## Conclusiones Generales

El desarrollo de este proyecto permitió aplicar las distintas etapas de un proceso de aprendizaje automático supervisado, desde la exploración y el preprocesamiento de los datos hasta el entrenamiento, la evaluación y la comparación de diferentes modelos de clasificación.


**Cumplimiento del objetivo del proyecto**

Se logró desarrollar un modelo de clasificación multiclase capaz de intentar predecir la categoría *shape* (forma) de los reportes de avistamientos UFO/UAP/OVNI, basado en la variable objetivo *shape_grouped* utilizando información descriptiva y temporal de los registros históricos; implementando y evaluando un sistema de clasificación supervisada sobre datos reales aportados por los testigos de elos avistamientos.


**Importancia del preprocesamiento de los datos**

La etapa de limpieza y transformación resultó muy importante para mejorar la calidad del conjunto de datos. Se realizaron tratamientos de valores nulos, normalización de variables, transformación de atributos, ingeniería de características y reducción de categorías poco representadas.
Estas decisiones permitieron construir un conjunto de datos más adecuado para el enfoque de entrenamiento del modelo.


**Resultados y evaluación de los modelos**

Se observó que el tratamiento del desbalance de clases influye significativamente en los resultados.
El modelo Random Forest con balanceo permitió mejorar la capacidad de reconocer algunas categorías minoritarias, aunque esto también produjo un aumento de las falsas predicciones. Por ejemplo, la categoría Fireball (Bola de fuego) alcanzó un Recall del 53 %, pero una Precision del 18 %. Esto significa que el modelo consiguió recuperar una proporción mayor de los registros reales de esa categoría, aunque también clasificó incorrectamente numerosos registros como Fireball.

Por lo tanto, los resultados deben interpretarse considerando conjuntamente Precision, Recall y F1-score, y no únicamente la exactitud general (*Accuracy*).

**Limitaciones del modelo**

Los resultados obtenidos muestran que todavía existen dificultades para distinguir correctamente algunas categorías. La distribución desigual de los registros, la similitud entre determinadas descripciones y la limitada información disponible en los reportes representan desafíos importantes para la clasificación.

En consecuencia, el modelo no debe considerarse un sistema de identificación de objetos ni una herramienta capaz de verificar la naturaleza real de los avistamientos.

Su alcance se limita exclusivamente a clasificar los reportes según las formas descriptas por los testigos.


**Aporte y posibilidades de desarrollo**

Más allá de las limitaciones encontradas, el proyecto permitió construir una base de trabajo para continuar investigando la aplicación de técnicas de Ciencia de Datos y Aprendizaje Automático sobre registros históricos de avistamientos UFO/UAP.

Los resultados obtenidos son un punto de partida para experimentar con nuevas características, técnicas de balanceo, selección de variables y algoritmos de clasificación.

# Prueba con datos artificiales

Al final del notebook que presenta el modelo se incluye una versión del programa de clasificación con la utilización de datos artificiales de ejemplo donde se puede clasificar, en un ejemplo hipotético,alguna forma de avistamiento de un testigo según estado, dia y horario. Predice y clasifica la forma.
Sirve para demostrar de forma práctica cómo el modelo toma nuevas entradas —como un avistamiento hipotético determinado por el estado, el día y el horario y devuelve una predicción de la categoría de forma (`shape_grouped`).


## Conclusiones generales sobre el modelo

En función del objetivo en este proyecto y de los resultados obtenidos mediante el modelo Random Forest con balanceo de clases, los resultados permiten observar que el modelo consigue aprender algunos patrones de los registros históricos, puede reconocer determinadas categorías de forma de OVNI mejor que otras; pero en general tiene grandes dificultades para distinguir las siete categorías de formas definidas en shape_grouped, alcanzando un rendimiento predictivo limitado.

Eso podría estar relacionado a la naturaleza del problema: la forma reportada es una descripción subjetiva del testigo y las variables de contexto (cuándo, dónde, cuánto duró) aportan muy poca información sobre ella.

Por eso dicho modelo no alcanza a predecir con precisión la forma de un objeto volador no identificado a partir de las características temporales, geográficas, de duración de los avistamientos que se presentaron como variables de entrada, pues la forma ( especificadas en shape o shape_grouped) es una percepción del testigo, no una consecuencia de la hora, la estación o el estado donde ocurre. Esas variables describen el contexto, no el objeto.


En términos generales, el proyecto permitió cumplir el propósito académico y técnico de desarrollar un proceso completo de aprendizaje automático supervisado aplicado a un problema de clasificación multiclase.
Si bien los resultados del modelo seleccionado todavía presentan limitaciones en su capacidad predictiva, el trabajo permitió comprender la importancia de la calidad de los datos, el tratamiento del desbalance de clases y la correcta interpretación de las métricas de evaluación.

---

