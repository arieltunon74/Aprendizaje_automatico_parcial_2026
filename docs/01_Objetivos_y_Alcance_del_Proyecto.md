
# Objetivo General

**Intentar clasificar la categoría de la forma de un reporte mediante la aplicación de técnicas de Aprendizaje Automático supervisado mediante clasificación multiclase.**

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

# Alcance del proyecto

El proyecto se centra en el análisis de datos de avistamientos de objetos voladores no identificados (UFO), utilizando el dataset NUFORC como fuente de información, con el propósito de evaluar la capacidad de distintos algoritmos de Aprendizaje Automático supervisado para clasificar la forma reportada de los objetos.

**Importante**: 

El modelo estaría aprendiendo a partir de reportes humanos registrados en NUFORC, no estaría identificando científicamente qué objetos son realmente OVNIS/ UFO/ UAP.

El modelo NO busca determinar la existencia de vida extraterrestre ni comprobar la naturaleza de los objetos observados.

---

## Tipo de problema

**Clasificación supervisada multiclase**

## Problema planteado para resolver con un modelo de aprendizaje automático supervisado

¿Es posible clasificar los reportes de avistamientos de objetos voladores no identificados (UFO - OVNI - UAP) según la forma descrita por los testigos, utilizando sus características temporales, geográficas y de duración?

---

## Acerca de las variables predictoras

Se trataran o unificarán según el caso, las variables como `occurred_date_time` que contengan día, mes, año , horas, minutos y que contengan ubicación geeográfica como `state` para generar otros tipos de variables para la implementación de los modelos, es decir que a partir de ellas se podrán generar nuevas características derivadas que permitan representar mejor la información y evaluar su utilidad para la implementación de los modelos de Aprendizaje Automático.

Se utilizarán como variables predictoras todas las variables disponibles en el conjunto de datos, excepto las variables `summary` y `details_url` que ambos contienen campos de texto con las descripciones de los testigos que vieron los OVNIS. EL PROCESAMIENTO DE DICHOS TEXTOS NO SERÁ TENIDO EN CUENTA, dentro del alcance de este proyecto, pues hay que implementar otros modelos de aprendizaje que no vimos en clase.

`posted_date` se conservará inicialmente para evaluar su posible utilidad en el desarrollo del modelo, es decir que su inclusión como variable predictora dependerá de los resultados del análisis exploratorio y de su relevancia para el objetivo de clasificación.
Las fechas están representadas como texto y podrían convertirse a un tipo temporal.

---

## Medidas de prevención de dataleak - Justificación de la elección de las variables

En el proyecto de clasificación de formas de OVNIs, las variables excluidas para evitar la fuga de datos (data leakage) y el sobreajuste incluyen principalmente las siguientes:

La variable original `shape`: Fue descartada por tratarse de la fuente directa de la cual se derivó la variable objetivo (`shape_grouped`), lo que constituiría una fuga directa de la etiqueta a predecir.

Fechas de publicación posteriores (`posted_date`, `posted_year`, `posted_month`, `posted_dayofweek`): Excluidas porque la fecha en que se reporta o publica un avistamiento en la base de datos ocurre después de este, representando información futura que no estaría disponible en un escenario de predicción real.

Versiones redundantes de duración (duration en formato de texto o variantes previas): Se descartaron para evitar duplicidad, conservando únicamente la variable numérica estandarizada (`duration_seconds`).

Variables de alta cardinalidad específica (`city`): Se omitieron campos como la ciudad exacta para evitar un sobreajuste (overfitting) severo, priorizando en su lugar atributos espaciales y contextuales más amplios como `state_grouped` y `us_region`.

Esta selección rigurosa garantiza que el modelo aprenda a partir de patrones temporales, espaciales y cuantitativos reales (`duration_seconds`, años, estaciones, etc.) y no de indicios directos de la respuesta o información del futuro.
El entrenamiento (la división de los datos y la definición de la estrategia) ocurrió lógicamente primero, pero operativamente el escalado se ajustó exclusivamente dentro del conjunto de entrenamiento para evitar fugas de datos (data leakage).


---

## ESTADO FINAL DEL DATASET DESPUÉS DEL PREPROCESAMIENTO

Resultado del proceso de limpieza, transformación y preparación de los datos, con el objetivo de obtener un conjunto de datos consistente y adecuado para el desarrollo de modelos de Aprendizaje Automático.

Después del preprocesamiento, el dataset principal cuenta con 111.741 filas (instancias) y 28 columnas adicionales, generadas principalmente mediante la transformación de variables numéricas en categóricas y la creación de nuevas características derivadas.

Filtrando haciendo foco de las observaciones en Estados Unidos, el dataset considera  99,202 filas

Sin embargo  aplicó un filtrado en los avistamientos Ligth y Unknown por no tener una forma de objeto definida para clasificar, considerando el dataset 62,273 filas y 27 columnas adicionales luego de este filtrado.

Asimismo, se realizó un análisis de las variables disponibles para determinar su utilidad como predictoras. Se decidió excluir summary y details_url, mientras que la posible utilidad de date_posted se evaluará durante el desarrollo de los modelos.

Se descartaron las categorías light, other y unknown por considerarse poco específicas o ambiguas. Asimismo, se eliminaron las categorías delta, crescent, round, diamond, hexagon, flare, dome y pyramid debido a su baja frecuencia de aparición en el conjunto de datos, con el objetivo de reducir la cantidad de clases y facilitar el proceso de clasificación multiclase.

En caso necesario, luego se retomará el análisis de las categorías light, other y unknown por tener muchas frecuencias.

También se contempló el tratamiento de variables temporales y geográficas. A partir de occurred_date_time, se podrán obtener características como año, mes, día, hora, día de la semana y estación del año. Para la variable state, se podrán realizar agrupaciones geográficas o generar nuevas características que permitan representar mejor la ubicación de los avistamientos.

Por otra parte, se evaluó la distribución de las categorías de la variable objetivo shape, con el propósito de identificar las categorías adecuadas para el problema de clasificación multiclase y definir su tratamiento según su frecuencia y representatividad.

El resultado es un conjunto de datos preparado para continuar con el análisis exploratorio, la selección de características y la implementación y evaluación de diferentes algoritmos de clasificación multiclase.

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

Random Forest (con balance de clases)

---

## Modelos de aprendizaje automático supervisados que se probaron: 

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

## Conclusiones Generales

El desarrollo de este proyecto permitió aplicar las distintas etapas de un proceso de aprendizaje automático supervisado, desde la exploración y el preprocesamiento de los datos hasta el entrenamiento, la evaluación y la comparación de diferentes modelos de clasificación.


**Cumplimiento del objetivo del proyecto**

Se logró desarrollar un modelo de clasificación multiclase capaz de intentar predecir la categoría *shape* (forma) de los reportes de avistamientos UFO/UAP/OVNI, basado en la variable objetivo *shape_grouped* utilizando información descriptiva y temporal de los registros históricos.

De esta manera, se cumplió el objetivo de implementar y evaluar un sistema de clasificación supervisada sobre datos reales aportados por los testigos de elos avistamientos.

**Importancia del preprocesamiento de los datos**

La etapa de limpieza y transformación resultó muy importante para mejorar la calidad del conjunto de datos. Se realizaron tratamientos de valores nulos, normalización de variables, transformación de atributos, ingeniería de características y reducción de categorías poco representadas.

Estas decisiones permitieron construir un conjunto de datos más adecuado para el enfoque de entrenamiento del modelo.

**Resultados y evaluación de los modelos**

Se observó que el tratamiento del desbalance de clases influye significativamente en los resultados.

El modelo Random Forest con balanceo permitió mejorar la capacidad de reconocer algunas categorías minoritarias, aunque esto también produjo un aumento de las falsas predicciones.
Por ejemplo, la categoría Fireball (Bola de fuego) alcanzó un Recall del 53 %, pero una Precision del 18 %. Esto significa que el modelo consiguió recuperar una proporción mayor de los registros reales de esa categoría, aunque también clasificó incorrectamente numerosos registros como Fireball.

Por lo tanto, los resultados deben interpretarse considerando conjuntamente Precision, Recall y F1-score, y no únicamente la exactitud general (*Accuracy*).

**Limitaciones del modelo**

Los resultados obtenidos muestran que todavía existen dificultades para distinguir correctamente algunas categorías. La distribución desigual de los registros, la similitud entre determinadas descripciones y la limitada información disponible en los reportes representan desafíos importantes para la clasificación.

En consecuencia, el modelo no debe considerarse un sistema de identificación de objetos ni una herramienta capaz de verificar la naturaleza real de los avistamientos.

Su alcance se limita exclusivamente a clasificar los reportes según las formas descriptas por los testigos.

**Aporte y posibilidades de desarrollo**

Más allá de las limitaciones encontradas, el proyecto permitió construir una base de trabajo para continuar investigando la aplicación de técnicas de Ciencia de Datos y Aprendizaje Automático sobre registros históricos de avistamientos UFO/UAP.

Los resultados obtenidos constituyen un punto de partida para experimentar con nuevas características, técnicas de balanceo, selección de variables y algoritmos de clasificación.

**Conclusión final**

En términos generales, el proyecto permitió cumplir el propósito académico y técnico de desarrollar un proceso completo de aprendizaje automático supervisado aplicado a un problema de clasificación multiclase.

Si bien los resultados del modelo seleccionado todavía presentan limitaciones en su capacidad predictiva, el trabajo permitió comprender la importancia de la calidad de los datos, el tratamiento del desbalance de clases y la correcta interpretación de las métricas de evaluación.

## Conclusiones generales sobre el modelo

En función del objetivo en este proyecto y de los resultados obtenidos mediante el modelo Random Forest con balanceo de clases, los resultados permiten observar que el modelo consigue aprender algunos patrones de los registros históricos, puede reconocer determinadas categorías de forma de OVNI mejor que otras; pero en general tiene grandes dificultades para distinguir las siete categorías de formas definidas en shape_grouped, alcanzando un rendimiento predictivo limitado.

Eso podría estar relacionado a la naturaleza del problema: la forma reportada es una descripción subjetiva del testigo y las variables de contexto (cuándo, dónde, cuánto duró) aportan muy poca información sobre ella.

Por eso dicho modelo no alcanza a predecir con precisión la forma de un objeto volador no identificado a partir de las características temporales, geográficas, de duración de los avistamientos que se presentaron como variables de entrada, pues la forma ( especificadas en shape o shape_grouped) es una percepción del testigo, no una consecuencia de la hora, la estación o el estado donde ocurre. Esas variables describen el contexto, no el objeto.

El modelo alcanzó una accuracy de 21,1 % y un F1 macro de 0,19 sobre siete clases, un desempeño comparable al de una predicción aleatoria. Observando las métricas obtenidas, el “buen” desempeño de Fireball (recall 53 %) podría estar relacionado con el balanceo de clases, su precisión es de sólo 18 %, o sea que el modelo identifica una parte de los casos reales, pero también clasifica incorrectamente como Fireball muchos registros de otras categorías. Lo mismo ocurre con las formas Disc y Triangle. El rendimiento limitado no se debe principalmente a la elección del algoritmo, sino a la baja relación entre las variables predictoras y la variable objetivo.

El rendimiento obtenido indica que todavía existen oportunidades de mejora mediante la experimentación con otros algoritmos y diferentes estrategias de tratamiento de las variables que no implementamos como por ejemplo tomar como variable objetivo 'duration_seconds' como un problema de regresion, también realizar pruebas con modelos de aprendizaje no-supervisados. Otra alternativa que puede quedar como objeto de otra línea de investigación es analizar el texto de los reportes (columna ´summary´ en el dataset original) mediante análisis de texto con modelos NLP (Procesamiento del Lenguaje Natural), que es información importante de estos eventos pero que el modelo actualmente no ve porque no fue considerada dentro del alcance del proyecto; todas estas propuestas quedan delimitadas para otros proyectos en el futuro.

