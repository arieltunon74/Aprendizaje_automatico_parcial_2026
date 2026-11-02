
# Objetivo General

**Intentar clasificar la categoría de la forma de un reporte mediante la aplicación de técnicas de Aprendizaje Automático supervisado mediante clasificación multiclase.**

Se busca identificar patrones y evaluar la capacidad de los modelos de aprendizaje automático para predecir la forma reportada del objeto (shape) según las características disponibles.

**Clasificación**: el modelo asigna una categoría
**Predicción**: el modelo estima cuál es la categoría más probable según los patrones aprendidos
**La variable objetivo (target)**: shape → forma reportada del objeto según los testigos

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

# Alcance del proyecto

El proyecto se centra en el análisis de datos de avistamientos de objetos voladores no identificados (UFO), utilizando el dataset NUFORC como fuente de información, con el propósito de evaluar la capacidad de distintos algoritmos de Aprendizaje Automático supervisado para clasificar la forma reportada de los objetos.

**Importante**: 

El modelo estaría aprendiendo a partir de reportes humanos registrados en NUFORC, no estaría identificando científicamente qué objetos son realmente OVNIS/ UFO/ UAP.

El modelo NO busca determinar la existencia de vida extraterrestre ni comprobar la naturaleza de los objetos observados.

---

## Tipo de problema

**Clasificación supervisada multiclase**

## Problema planteado para resolver con un modelo de aprendizaje automático supervisado

¿Es posible clasificar los reportes de avistamientos de objetos voladores no identificados (UFO) según la forma descrita por los testigos, utilizando sus características temporales, geográficas y de duración?

---

## Acerca de las variables predictoras

Se trataran o unificarán según el caso, las variables como `occurred_date_time` que contengan día, mes, año , horas, minutos y que contengan ubicación geeográfica como `state` para generar otros tipos de variables para la implementación de los modelos, es decir que a partir de ellas se podrán generar nuevas características derivadas que permitan representar mejor la información y evaluar su utilidad para la implementación de los modelos de Aprendizaje Automático.

Se utilizarán como variables predictoras todas las variables disponibles en el conjunto de datos, excepto las variables `summary` y `details_url` que ambos contienen campos de texto con las descripciones de los testigos que vieron los OVNIS. EL PROCESAMIENTO DE DICHOS TEXTOS NO SERÁ TENIDO EN CUENTA, dentro del alcance de este proyecto, pues hay que implementar otros modelos de aprendizaje que no vimos en clase.

`posted_date` se conservará inicialmente para evaluar su posible utilidad en el desarrollo del modelo, es decir que su inclusión como variable predictora dependerá de los resultados del análisis exploratorio y de su relevancia para el objetivo de clasificación.
Las fechas están representadas como texto y podrían convertirse a un tipo temporal.

## Modelos de aprendizaje automático supervisados que podría utilizar 

**Regresión Logística Multiclase o Multinomial**: para predecir la forma del OVNI (shape), 
permitiendo evaluar la probabilidad de pertenencia a cada clase e interpretar mediante sus 
coeficientes el impacto de las variables temporales, geográficas, de duración de cada categoría.

**Árbol de Decisión**: Se selecciona este modelo supervisado debido a su capacidad para ofrecer 
reglas de decisión claras y transparentes en la clasificación de las formas de los OVNIs (shape).

**Random Forest**: Se implementa el modelo de Random Forest como algoritmo de ensamblaje 
supervisado para predecir la forma del OVNI (shape), combinando múltiples árboles de decisión 
independientes para capturar interacciones no lineales complejas y mitigar el riesgo de sobreajuste 
(overfitting) a partir de las variables temporales, geográficas y de duración.

**K-Nearest Neighbors (KNN)**:  Se puede implementar el modelo de K-Nearest Neighbors (KNN) 
como clasificador basado en distancias para predecir la forma del OVNI (shape), asignando cada 
categoría según la clase mayoritaria de sus instancias más cercanas en el espacio vectorial de 
características.

---

# Codificación de Variables Categóricas (Dataset procesado NUFORC)

**En base al dataset original:** NUFORC UFO Sightings - Data scraped from the National UFO reporting center – By Thaddeus Segura - (DbCL) v1.0

Una técnica que se intentará en los modelos es **One Hot Encoding (OHE)** consiste en convertir variables categóricas en vectores binarios ($0$ y $1$). Su uso óptimo requiere que las variables tengan **baja a moderada cardinalidad** (pocos valores únicos) para evitar el aumento excesivo de dimensiones (*curse of dimensionality*).

## 2. Posibles variables a realizar One Hot Encoding en el Notebook

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
| `Duracion_clasificacion` | Duración del evento | Rangos cualitativos discretos de duración (Ej: Corta, Media, Larga). | 
| `duration_category_detailed` | Duración detallada | Rangos cualitativos ampliados pero disjuntos y limitados en número. | 
| `shape_grouped` | Forma del fenómeno | Agrupaciones de las formas reportadas (en caso de usarse como *feature* $X$). | 

> **Nota sobre `state`:**: se intentará priorizar `state_grouped` o `us_region`.

## 3. Variables EXCLUIDAS de One Hot Encoding

| Variable | Motivo de Exclusión | Técnica Alternativa Recomendada | 
| ----- | ----- | ----- | 
| `city` | Alta cardinalidad (miles de ciudades únicas). OHE crearía una matriz hiper-dispersa (*sparse matrix*) con riesgo severo de *overfitting*. | *Target Encoding*, *Frequency Encoding* o descarte. | 
| `duration_seconds` | Es una variable **numérica continua**, no categórica. | Escalado cuantitativo (`StandardScaler`, `MinMaxScaler`) o transformación logarítmica. | 
| `is_weekend` | Es una variable binaria intrínseca ($0/1$ o `True/False`). | No requiere transformación adicionales. | 

---


