# ANÁLISIS EXPLORATORIO - DESCRIPCIÓN DEL DATASET

## 1. Descripción general

Este proyecto utiliza el conjunto de datos **NUFORC UFO Sightings**, una
recopilación de reportes de avistamientos de objetos voladores no
identificados (UFO / OVNIs). El dataset contiene información sobre la
fecha y hora del avistamiento, la ubicación informada, la forma descrita
por el testigo, la duración estimada y el texto del reporte, entre otros
campos.

El conjunto de datos se emplea como fuente para un proyecto académico de
aprendizaje automático supervisado cuyo objetivo es evaluar la capacidad
de distintos algoritmos para clasificar la forma reportada, representada
por la variable `shape`.

## 2. Procedencia y origen de los datos

La versión utilizada se identifica como **"NUFORC UFO Sightings - Data
scraped from the National UFO Reporting Center"**, publicada en Kaggle
por **Thaddeus Segura**. Según la descripción del conjunto, los
registros fueron recopilados mediante extracción de información (*web
scraping*) de reportes publicados por el **National UFO Reporting Center
(NUFORC)**.

-   **Plataforma de distribución:** Kaggle.
-   **Dataset:** `ufo-sightings`.
-   **Autor de la publicación en Kaggle:** Thaddeus Segura.
-   **Fuente original de los reportes:** National UFO Reporting Center
    (NUFORC).
-   **Archivo utilizado en el notebook:** `clean_ufo_data.csv`.

El archivo se carga en el notebook mediante `kagglehub`, utilizando el
identificador `thaddeussegura/ufo-sightings`. Por lo tanto, Kaggle es la
plataforma desde la que se obtiene la copia utilizada en el proyecto,
mientras que NUFORC es la fuente original de los reportes recopilados.

**Dataset:** NUFORC UFO Sightings - Data scraped from the National UFO reporting center – By Thaddeus Segura - (DbCL) v1.0

## 3. Cantidad de registros y dimensiones

En la carga inicial del archivo `clean_ufo_data.csv`, el notebook
registra las siguientes dimensiones:

-   **Cantidad de instancias (filas):** 120.785.
-   **Cantidad de variables (columnas):** 9.

Estas cifras corresponden al dataset cargado inicialmente, antes de los
filtros y las transformaciones posteriores realizados durante el trabajo.

## 4. Variables disponibles originalmente

  -----------------------------------------------------------------------
  Variable                            Descripción
  ----------------------------------- -----------------------------------
  `id`                                Identificador numérico del reporte.

  `occurred_date_time`                Fecha y hora informadas para el
                                      avistamiento.

  `city`                              Ciudad asociada al reporte.

  `state`                             Estado o región administrativa
                                      informado en el registro.

  `shape`                             Forma descrita para el objeto
                                      observado. Es la variable objetivo
                                      del proyecto.

  `duration`                          Duración del avistamiento expresada
                                      originalmente como texto.

  `summary`                           Resumen textual de la descripción
                                      del testigo.

  `details_url`                       Dirección web del reporte detallado
                                      en NUFORC.

  `posted_date`                       Fecha en la que se generó el reporte.    
                                    

  -----------------------------------------------------------------------

## 5. Tipos de datos

  -----------------------------------------------------------------------
  Variable                Tipo de dato en pandas  Tipo de información
  ----------------------- ----------------------- -----------------------
  `id`                    `int64`                 Numérica entera;
                                                  identificador.

  `occurred_date_time`    `object`                Fecha y hora
                                                  almacenadas como texto.

  `city`                  `object`                Categórica/textual.

  `state`                 `object`                Categórica/textual.

  `shape`                 `object`                Categórica/textual;
                                                  variable objetivo.

  `duration`              `object`                Texto que representa
                                                  una duración.

  `summary`               `object`                Texto descriptivo.

  `details_url`           `object`                Texto; dirección web.

  `posted_date`           `object`                Fecha almacenada como
                                                  texto.
  -----------------------------------------------------------------------

En esta versión, `id` es la única columna reconocida como numérica
(`int64`); las otras ocho columnas aparecen con tipo `object`.

`posted_date` se conservará inicialmente para evaluar su posible utilidad en el desarrollo del modelo, es decir que su inclusión como variable predictora dependerá de los resultados del análisis exploratorio y de su relevancia para el objetivo de clasificación.
Las fechas están representadas como texto y podrían convertirse a un tipo temporal.
EL PROCESAMIENTO DE DICHOS TEXTOS NO SERÁ TENIDO EN CUENTA dentro del alcance de este proyecto.

---

# Reporte de Limpieza y Estandarización del Dataset

## DETECCIÓN DE VALORES NULOS - DUPLICADOS - INCOSISTENCIAS (EN EL DATASET)

### No se detectaron valores duplicados

## Conteo de Valores Nulos

A continuación se presenta la cantidad de valores nulos detectados en cada una de las columnas del dataset, ordenados de mayor a menor frecuencia:

| Columna              | Valores Nulos |
| :--------------------| :-----------: |
| `state`              | **8,714**     |
| `duration`           | **4,372**     |
| `shape`              | **4,098**     |
| `city`               | **261**       |
| `occurred_date_time` | **61**        |
| `summary`            | **37**        |

---

## Estandarización de la Variable Objetivo (`shape`)

Para homogenizar las distintas variantes del campo `shape` (forma)
se aplicó un diccionario de reemplazo que unifica el formato a mayúscula inicial (Title Case) y corrige sinónimos o variaciones especiales.

### Diccionario de Transformación (Python)

```python
# Diccionario para unificar variaciones de shape
reemplazos_shape = {
    # Minúsculas a su formato con mayúscula inicial
    "light": "Light",
    "other": "Other",
    "triangle": "Triangle",
    "circle": "Circle",
    "sphere": "Sphere",
    "cylinder": "Cylinder",
    "rectangle": "Rectangle",
    "cigar": "Cigar",
    "fireball": "Fireball",
    "oval": "Oval",
    "delta": "Delta",
    "unknown": "Unknown",
    "flash": "Flash",
    "egg": "Egg",

    # Sinónimos o variantes especiales
    "TRIANGULAR": "Triangle",
    "changed": "Changing",
    "changing": "Changing"
}
```
---

# DICCIONARIO DE DATOS

## 1. Descripción de las variables

Traducciones al español y la terminología utilizada en el proyecto de Aprendizaje Automático.


| Nombre de la columna | Traducción al español | Descripción |
|----|---|---|
| `id` | Identificador | Identificador numérico único del reporte. |
| `occurred_date_time` | Fecha y hora del avistamiento | Fecha y hora informadas en las que ocurrió el avistamiento. |
| `city` | Ciudad | Ciudad asociada al lugar del avistamiento. |
| `state` | Estado o región | Estado o región administrativa donde se informó el avistamiento. |
| `shape` | Forma | Forma aparente del objeto descrita por el testigo. Es la variable objetivo del proyecto. |
| `duration` | Duración | Tiempo de duración del avistamiento, expresado originalmente como texto. |
| `summary` | Resumen | Resumen textual de la descripción proporcionada por el testigo. |
| `details_url` | URL del reporte detallado | Dirección web que permite acceder al reporte original en NUFORC. |
| `posted_date` | Fecha de publicación | Fecha en la que el reporte fue publicado en NUFORC. |

## 2. Categorías de la variable objetivo `shape`

La variable `shape` es la forma aparente del objeto descrita por el testigo. 
Es una variable categórica nominal que constituye el objetivo de la clasificación supervisada multiclase.

### Otras categorías de valores posibles de `shape` (Forma del OVNI)

| Categoría (inglés) | Traducción al español |
|---|---|
| `Light` | Luz |
| `Circle` | Círculo |
| `Triangle` | Triángulo |
| `Fireball` | Bola de fuego |
| `Sphere` | Esfera |
| `Disk` | Disco |
| `Oval` | Ovalado |
| `Formation` | Formación |
| `Changing` | Cambiante |
| `Cigar` | Cigarrillo o forma cilíndrica |
| `Diamond` | Diamante |
| `Cylinder` | Cilindro |
| `Rectangle` | Rectángulo |
| `Flash` | Destello |
| `Teardrop` | Lágrima |
| `Cone` | Cono |
| `Cross` | Cruz |
| `Chevron` | Chevrón o forma de V |
| `Egg` | Huevo |
| `Unknown` | Desconocido |
| `Other` | Otra forma |

## 3. Glosario de términos

```
| Término      | Significado | Descripción |
|--------------|-------------|-------------|
| **Sighting** | Avistamiento| Observación visual de un objeto o fenómeno, generalmente realizada por uno o varios testigos. |
| **UFO**      | Unidentified Flying Object (Objeto Volador No Identificado - OVNI) | Término utilizado para describir un objeto observado en el cielo cuya identidad no ha podido determinarse. |
| **UAP**      | Unidentified Anomalous Phenomena (Fenómenos Anómalos No Identificados) | Término más amplio que UFO, utilizado para referirse a fenómenos anómalos que no han podido identificarse en diferentes entornos. |
```

## 4. Consideraciones sobre las variables

- **Variable objetivo (`shape`):** Es la categoría que el modelo de aprendizaje automático intentará predecir.
- **Variables predictoras:** podrán seleccionarse a partir de las características temporales, geográficas y de duración de los avistamientos.
- **Identificadores y referencias:** `id` y `details_url` se utilizan principalmente para identificar y consultar los registros, por lo que no se consideran inicialmente variables predictoras.
- **Información textual:** `summary` contiene descripciones de los testigos, no se tendrá en cuenta para los análisis.
- **Fecha de publicación:** `posted_date` puede utilizarse para generar características temporales y evaluar su posible aporte al modelo.

## 5. DICCIONARIO

# Diccionario de Variables del dataset pre-procesado y definitivo.


| Nombre de la columna | Traducción al español | Descripción |
|---|---|---|
| `id` | Identificador | Identificador numérico único de cada reporte. |
| `occurred_date_time` | Fecha y hora del avistamiento | Fecha y hora originales informadas en las que ocurrió el avistamiento. |
| `city` | Ciudad | Ciudad asociada al lugar del avistamiento. |
| `state` | Estado o región | Estado o región administrativa donde se informó el avistamiento. |
| `shape` | Forma reportada | Forma aparente del objeto descrita por el testigo. Es la variable objetivo original del proyecto. |
| `duration` | Duración original | Tiempo de duración del avistamiento, expresado originalmente como texto. |
| `summary` | Resumen | Resumen textual de la descripción proporcionada por el testigo. |
| `details_url` | URL del reporte detallado | Dirección web que permite acceder al reporte original de NUFORC. |
| `posted_date` | Fecha de publicación | Fecha en la que el reporte fue publicado en NUFORC. |
| `year` | Año | Año en el que ocurrió el avistamiento, extraído de la fecha original. |
| `state_grouped` | Estado agrupado | Variable que agrupa los estados según un criterio de agrupación geográfica o de frecuencia. |
| `duration_seconds` | Duración en segundos | Duración del avistamiento convertida a un valor numérico expresado en segundos. |
| `duration_seconds_isna` | Indicador de duración ausente | Variable indicadora que identifica los registros en los que la duración en segundos está ausente (NaN). |
| `month` | Mes | Número del mes en el que ocurrió el avistamiento. |
| `hour` | Hora | Hora del día en la que ocurrió el avistamiento. |
| `day_of_week` | Día de la semana | Día de la semana en el que ocurrió el avistamiento. |
| `occurred_datetime` | Fecha y hora normalizadas | Variable que representa la fecha y hora del avistamiento en formato datetime para facilitar su procesamiento. |
| `month_category` | Categoría del mes | Variable categórica que representa el mes del año en el que ocurrió el avistamiento. |
| `north_season` | Estación del año (hemisferio norte) | Estación del año correspondiente a la fecha del avistamiento, calculada según las estaciones del hemisferio norte. |
| `day_category` | Categoría del día | Clasificación temporal del día según un criterio definido durante el preprocesamiento. |
| `Duracion_clasificacion` | Clasificación de la duración | Variable categórica que agrupa los avistamientos según su duración. |
| `time_of_day` | Franja horaria | Clasificación del horario del avistamiento en franjas del día, por ejemplo, mañana, tarde, noche o madrugada. |
| `is_weekend` | Es fin de semana | Variable booleana que indica si el avistamiento ocurrió durante un sábado o domingo. |
| `shape_grouped` | Forma agrupada | Variable que agrupa las categorías originales de `shape` según criterios definidos para el problema de clasificación. |
| `decade` | Década | Década correspondiente al año en el que ocurrió el avistamiento. |
| `duration_category_detailed` | Categoría detallada de duración | Clasificación de la duración del avistamiento en intervalos más específicos. |
| `us_region` | Región de Estados Unidos | Región geográfica de Estados Unidos a la que pertenece el estado informado. |
| `quarter_category` | Trimestre del año | Categoría que identifica el trimestre del año en el que ocurrió el avistamiento (primero, segundo, tercero o cuarto). |

## 6. Consideraciones sobre el dataset

La cantidad de registros y los tipos de datos indicados corresponden a
la carga inicial observada en el notebook 01_Limpieza_y_Preprocesamiento.ipynb.

Los datos nulos, las inconsistencias, las categorías poco frecuentes y las transformaciones
que se apliquen se documentarán en las etapas posteriores del
proyecto, sin confundir esta descripción del origen y la composición del
dataset con el informe completo del análisis exploratorio o del
preprocesamiento.

El notebook con los datos limpios para comenzar a modelar es: 02_Datos_Limpios_y_Preparados.ipynb

## 7. Características Generales

En la carga inicial del archivo `clean_ufo_data.csv`, el notebook
registra las siguientes dimensiones:


| Característica                 | Valor                     |
|--------------------------------|---------------------------|
| Cantidad de instancias (filas) | 120.785                   |
| Variables (columnas)           | 9                         |
| Unidad de análisis             | Un avistamiento reportado |
| Formato                        | CSV                       |
| Tipo de problema               | Clasificación Multiclase  | Aprendizaje Supervisado | 

---

# Dataset Final

El dataset final fue construido mediante la integración de las columnas.

`dataset_procesado.csv` - 14.5 mb


Cada fila representa un avistamiento informado, acompañado de múltiples atributos que describen aspectos propios del evento.

| Característica                 | Valor                     |
|--------------------------------|---------------------------|
| Cantidad de instancias (filas) | 79,695                    |
| Variables unificadas(columnas) | 25                        |
| Unidad de análisis             | Un avistamiento reportado |
| Formato                        | CSV                       |
| Tipo de problema               | Clasificación Multiclase  | Aprendizaje Supervisado | 


# Metodologias y decisiones adoptadas durante la limpieza del dataset:


### DISTRIBUCIÓN DE LAS FORMAS DE OVNIS (shape_grouped) - CATEGORÍA DE FORMAS AGRUPADA - VARIABLE OBJETIVO DEL MODELO DE APRENDIZAJE.

7 (siete) clases - Formas más comunes: Los avistamientos de tipo Other (Otros - conjunto de formas minoritarias) Light (Luz), Circle (Círculo), Triangle (Triángulo), Fireball (Bola de fuego), Sphere (Esféra), Disc (Disco).

---

### Fundamentación de la reducción de categorías de la variable objetivo (shape) para aplicar en la Agrupación (`shape_grouped`) de 28 clases a 7 clases para luego ser tomado como **variable objetivo del modelo**.

La reducción del número de categorías de la variable objetivo shape se plantea como una estrategia metodológica para abordar la complejidad del problema de clasificación multiclase.

Esta decisión toma como referencia el trabajo Improving Performance of Multiclass Classification by Inducing Class Hierarchies (2017), que estudia la organización jerárquica de categorías para simplificar los problemas de clasificación con múltiples clases, considerando las relaciones y confusiones entre ellas.

Sus autores proponen organizar las clases mediante jerarquías, reduciendo el número de categorías que intervienen en cada subproblema de clasificación.

Fuente: Science Direct
https://www.sciencedirect.com/science/article/pii/S1877050917308244?via%3Dihub

- Publicación: Procedia Computer Science, volumen 108, páginas 1692–1701.

---

La transformación de la variable objetivo original `shape` en un conjunto reducido de categorías consolidadas bajo la etiqueta **`shape_grouped`** responde a criterios tanto algorítmicos como inherentes al estudio de fenómenos aéreos no identificados (OVNI/UAP):

1. **Mitigación de la alta cardinalidad y clases minoritarias:**
   El análisis exploratorio reveló una marcada distribución de "cola larga", con decenas de formas marginales que presentaban frecuencias anecdóticas (ej. categorías con 1 o pocos registros, como *Dome, Flare, pyramid* o variaciones tipográficas). Mantener estas clases dispersas genera escasez de datos, impide una partición equilibrada entre entrenamiento y test, e induce un sobreajuste (*overfitting*)

2. **Tratamiento de la subjetividad y percepción del testigo:**
   En la casuística ufológica, la descripción morfológica está fuertemente condicionada por factores subjetivos y ambientales (distancia, ángulo de observación, condiciones lumínicas y agudeza visual). Un mismo evento puede ser interpretado y nombrado de forma distinta por diferentes testigos. Las categorías ultraespecíficas suelen reflejar variaciones semánticas o vocabulario individual más que diferencias físicas estructurales genuinas.

3. **Inconsistencia en los registros históricos y estandarización:**
   Las bases de datos de avistamientos recopilan reportes históricos donde los campos de texto libre o la ausencia de formularios estandarizados iniciales permitieron la proliferación de términos redundantes o aislados. Por eso se decide agruparlos en "other"

4. **Enfoque en las tipologías fenoménicas principales:**
   La literatura ufológica y estadística concuerda en que la gran mayoría de los reportes fiables se concentran en morfologías recurrentes y bien delimitadas (como luces nocturnas, esferas, triángulos, discos o círculos). Consolidar la variable objetivo permite que el modelo de aprendizaje automático supervise la clasificación centrándose en los patrones estructurales verdaderamente representativos del fenómeno estudiado, optimizando las métricas de evaluación global y la interpretabilidad de la matriz de confusión.


 Esta reducción de clases trae consecuencias para el modelo transformando un problema de clasificación inviable o altamente propenso al error por alta cardinalidad y datos insuficientes en un problema interpretable y estadísticamente viable. Si bien se sacrifica la capacidad de detectar rarezas extremas de la "Egg", "Cone" o "Cross"...se gana solidez en la identificación de los patrones principales del fenómeno estudiado.

 ---

 ## ANÁLISIS DE LAS DISTRIBUCIONES TEMPORALES DE LOS AVISTAMIENTOS OVNI

* **Estacionalidad (`north_season`):** Permite identificar en qué épocas del año (verano, invierno, etc.) ocurren más reportes. Se observa una concentración superior de avistamientos durante los meses de verano y otoño, lo cual suele correlacionarse con mayores actividades al aire libre, mejores condiciones climáticas para la observación nocturna y períodos vacacionales de los testigos.

* **Momento del día (`time_of_day`):** Ayuda a ver si predominan los avistamientos nocturnos frente a los diurnos.
La inmensa mayoría de los reportes se concentran en el período nocturno. Esto se debe a factores lógicos de visibilidad que contrastan de manera más evidente contra el cielo oscuro.

* **Patrones temporales (`decade` / `day_category` / `is_weekend`):** Muestran la evolución histórica por décadas y si hay tendencias según el tipo de día.
Además según los registros, se observa que el incremento de avistamientos durante los fines de semana (especialmente viernes y sábados) responde a la disponibilidad de tiempo libre de la población y a una mayor propensión a la observación del cielo en contextos recreativos o de descanso.
`decade`: A lo largo del tiempo, con un pico masivo en las décadas de los 2000s y 2010s. Este comportamiento no necesariamente implica un aumento físico de los avistamientos, sino una mayor digitalización, acceso a internet, difusión masiva de plataformas de reporte y estandarización de formularios de avistamiento en los últimos años.

* **Duración (`Duracion_clasificacion`):** Agrupa los eventos según cuánto tiempo duraron reportados. Sugiere que la mayoría de los fenómenos se manifiestan como destellos, tránsitos rápidos o destellos transitorios más que como eventos estáticos prolongados.


CLASIFICACIÓN DE DURACIÓN EN LA COLUMNA: `Duracion_clasificacion`

### Transformación de la duración del avistamiento en categorías

La variable `duration_seconds` representa la duración de un avistamiento OVNI expresada en segundos. Se aplica la técnica de transformación denominada **categorización o *binning***, que consiste en agrupar los valores numéricos continuos en intervalos definidos. Esta transformación permite analizar la duración mediante categorías temporales y explorar patrones que podrían resultar útiles para comprender el comportamiento de los registros.


###Criterio de categorización - Referencia según la fuente: https://canadianuforeport.ca/

The Canadian UFO Survey es un sitio NO oficial donde categoriza en segundos las duraciones de los avistamientos.

https://canadianuforeport.ca/survey-data?

Los intervalos deben definirse según la distribución real de los datos y los objetivos del análisis. Por ejemplo, se pueden considerar categorías como:

- 🟢 **Muy corto:** hasta 10 segundos.
- 🔵 **Corto:** más de 10 y hasta 60 segundos.
- 🟡 **Medio:** más de 60 y hasta 300 segundos.
- 🟠 **Largo:** más de 300 segundos


## Tratamiento y conversión de la columna `duration`

###CODIFICACIÓN DE LA VARIABLE `duration`

La variable `duration` contiene la duración del avistamiento OVNI expresada en diferentes unidades de tiempo (segundos, minutos, etc.). Se creó una nueva variable numérica denominada `duration_seconds`.
Esta transformación convierte las duraciones originales a **segundos**, utilizando una unidad de medida uniforme para todos los registros.

**Ejemplos de conversión:**

| `duration` | `duration_seconds` |
|---|---:|
| 5 minutes | 300 |
| 20 minutes | 1200 |
| 20 seconds | 20 |
| 2 minutes | 120 |
| 45 minutes | 2700 |

**Objetivo de la transformación:**

- Unificar las unidades de tiempo.
- Convertir la duración en una variable numérica.


La columna `duration` también contiene valores heterogéneos, expresados en diferentes unidades de tiempo y formatos de texto libre. Para facilitar su procesamiento y análisis, se realiza una normalización de las duraciones y se genera una nueva columna numérica denominada `duration_seconds`, que expresa todos los valores en segundos.

### Ejemplos de conversión

| Valor original (`duration`) | Conversión (`duration_seconds`) | Criterio aplicado |
|---|---:|---|
| `10 seconds` | 10 | Conversión directa |
| `5 minutes` | 300 | 5 × 60 |
| `1 hour` | 3600 | 1 × 3600 |
| `<1-2 minutes` | 60 | Se toma el menor valor del intervalo (1 minuto) |
| `2 hours+` | 7200 | Se considera el valor base de 2 horas |
| `00:05` | 5 | Interpretado como 5 segundos |
| `15-20 seconds` | 15 | Se toma el menor valor del intervalo |
| `<2 minutes` | 60 | Se asigna 1 minuto como valor de referencia |
| `~2 minutes` | 120 | Se considera el valor aproximado de 2 minutos |
| `30+minutes` | 1800 | Se considera el valor base de 30 minutos |
| `7 minutes +/-` | 420 | Se considera el valor central de 7 minutos |
| `30` | 30 | Se interpreta como 30 segundos |
| `2 minutes (each)` | 120 | Se considera el valor de 2 minutos |
| `approximately 1-2 minutes` | 60 | Se toma el menor valor del intervalo |
| `1 minute roughly until I...` | 60 | Se considera el valor aproximado de 1 minuto |

### Criterios metodológicos aplicados

Para normalizar los valores se establecen los siguientes criterios:

1. **Conversión de unidades:** los minutos se convierten a segundos multiplicando por 60 y las horas multiplicando por 3600.
2. **Intervalos de duración:** cuando se informa un rango, se toma el menor valor como criterio de conversión.
3. **Duraciones aproximadas:** se utiliza el valor numérico de referencia cuando está expresado explícitamente.
4. **Valores con signo positivo (`+`):** se considera el valor mínimo indicado.
5. **Valores numéricos sin unidad:** se interpretan como segundos.
6. **Formatos horarios:** se interpretan según el formato identificado en cada registro.

**Resultado:** se obtiene la columna `duration_seconds`, con valores numéricos homogéneos expresados en segundos, facilitando su utilización en el análisis exploratorio y los modelos de aprendizaje automático.

### CREACIÓN Y CLASIFICACIÓN DE LOS MESES SEGÚN LAS CUATRO ESTACIONES DEL AÑO (hemisferio norte)

A partir de la fecha de cada avistamiento, se identifica el mes de observación y se lo clasifica en una de las cuatro estaciones: verano, otoño, invierno o primavera.

Esta transformación permite incorporar información estacional al dataset y explorar posibles relaciones entre la época del año y las características de los avistamientos UFO - OVNI.

### Criterio de clasificación — Hemisferio norte

| ☀️ Verano (*Summer*) | Junio, julio y agosto |
| 🍂 Otoño (*Autumn/Fall*) | Septiembre, octubre y noviembre |
| ❄️ Invierno (*Winter*) | Diciembre, enero y febrero |
| 🌸 Primavera (*Spring*) | Marzo, abril y mayo |

### Procedimiento: Guardar el resultado en la nueva columna `north_season`.


# CREACIÓN DE UNA COLUMNA PARA CLASIFICAR LOS AVISTAMIENTOS POR FRANJA HORARIA DEL DÍA

Agrupa la hora del avistamiento en categorías intuitivas (Madrugada, Mañana, Tarde, Noche). Esto es excelente para modelos predictivos porque los avistamientos de OVNIs suelen tener patrones muy marcados según la luz solar.

En esta etapa se crea una nueva variable categórica que permite clasificar los avistamientos OVNI según la franja horaria en la que fueron reportados.

###Criterio de clasificación

| Franja horaria | Intervalo |
|---|---|
| 🌙 Madrugada (*Late Night*) | 00:00 a 05:59 |
| 🌅 Mañana (*Morning*) | 06:00 a 11:59 |
| ☀️ Tarde (*Afternoon*) | 12:00 a 17:59 |
| 🌆 Noche (*Evening/Night*) | 18:00 a 23:59 |

### Procedimiento: Guardar la clasificación en la nueva columna categórica `time_of_day`

Con cuatro clases —`Late Night`, `Morning`, `Afternoon` y `Evening/Night`— para analizar la distribución horaria de los avistamientos y explorar su relación con otras variables del dataset.

## JUSTIFICACIÓN

El objetivo de esta transformación para crear la columna `time_of_day` es incorporar información sobre el momento del día en que se producen los avistamientos, con el propósito de:

Identificar patrones horarios: analizar si los reportes presentan una mayor frecuencia en determinados momentos del día.

Explorar relaciones: investigar posibles asociaciones entre la franja horaria y otras características de los avistamientos, especialmente la forma reportada (shape).

Incorporar información predictiva: proporcionar al modelo de aprendizaje automático una variable temporal adicional que le permita identificar posibles patrones asociados al horario de observación.


---

## Fin de Semana vs. Día de Semana (`is_weekend`)

Una variable binaria categórica que indica si el avistamiento ocurrió en fin de semana (Sábado, Domingo) o entre semana. Muchas veces la actividad de reportes cambia radicalmente durante el tiempo libre de las personas

---

## Agrupación de la Forma del OVNI (`shape_grouped`)

La columna `shape` (forma) suele tener muchas categorías con pocos registros (como cigar, chevron, delta, etc.). Agrupar las formas menos frecuentes en una categoría general llamada "Others" evita la maldición de la dimensionalidad al aplicar One-Hot Encoding para modelos como Regresión Logística o K-NN. Esta será la nueva VARIABLE OBJETIVO durante las prediccionees que realize el modelo.

---

## Categoría de la Década (`decade`)

Permite agrupar los años de los avistamientos por décadas (ej. 1990s, 2000s, 2010s), lo cual ayuda a capturar tendencias históricas de reporte a largo plazo.

---

# PROCEDIMIENTOS DE LIMPIEZA DEL DATASET

## FILTRADO DEL RANGO TEMPORAL DE OBSERVACIONES (1962–2021)

### Selección y justificación del período de estudio

Se decide delimitar el período de análisis entre los años **1962 y 2021**, ambos inclusive, debido a que este intervalo concentra una mayor cantidad de observaciones dentro del dataset.

La selección se fundamenta en los siguientes criterios:

- **Disponibilidad de datos:** se prioriza un período que contiene una cantidad significativa de registros, permitiendo disponer de información suficiente para el análisis.
- **Representatividad:** se busca trabajar con un conjunto de observaciones que permita analizar una mayor variedad de reportes y características.
- **Preparación para el aprendizaje automático:** se procura disponer de un volumen de datos adecuado para las etapas de entrenamiento y evaluación de los modelos.

### Criterio de selección - Alcance del proyecto

Se conservan únicamente los registros que cumplen la siguiente condición:

**1962 ≤ año de observación ≤ 2021**

De esta manera, se excluyen los registros anteriores a 1962 y posteriores a 2021, delimitando un período uniforme para las etapas posteriores del proyecto.

---

#CREACIÓN DE LA COLUMNA `state` — AGRUPACIÓN GEOGRÁFICA

En esta etapa se analiza la variable geográfica `state`, que identifica el estado o la región administrativa en Estados Unidos asociada a cada avistamiento OVNI.

El objetivo es organizar y estandarizar la información geográfica para facilitar el análisis de la distribución espacial de los reportes e identificar posibles diferencias entre las regiones representadas en el dataset.


## JUSTIFICACIÓN

Organización geográfica: unificar y normalizar los nombres de los estados para evitar diferencias de escritura y categorías duplicadas.

Análisis espacial: identificar la distribución de los avistamientos y explorar posibles concentraciones geográficas de los reportes.

Identificación de patrones regionales: analizar si existen diferencias en las formas de los objetos reportados (shape) o (Shape_grouped) según su ubicación geográfica.

Información predictiva: incorporar la ubicación geográfica como atributo de entrada para que el modelo de aprendizaje automático pueda evaluar su posible utilidad en la clasificación de los avistamientos.

---


CONVERSIÓN DE LA VARIABLE `month` A CATEGÓRICA — MESES EN ESPAÑOL

Mapear los números de la columna `day_of_week` a nombres de días en español
Clasificación de los dias y meses del año

En esta etapa se transforma la variable `month`, que representa el mes de cada avistamiento OVNI, en una variable categórica con los nombres de los meses en español.

| Valor original | Categoría |
|---:|---|
| 1 | Enero |
| 2 | Febrero |
| 3 | Marzo |
| 4 | Abril |
| 5 | Mayo |
| 6 | Junio |
| 7 | Julio |
| 8 | Agosto |
| 9 | Septiembre |
| 10 | Octubre |
| 11 | Noviembre |
| 12 | Diciembre |

Ordenados cronológicamente y preparados para analizar la distribución mensual de los avistamientos OVNI.

## JUSTIFICACIÓN:

En esta etapa se transforman las variables temporales month y day_of_week, originalmente representadas mediante valores numéricos, en variables categóricas con los nombres de los meses y días de la semana en español para facilitar la interpretación de la información temporal y permitir un análisis más comprensible de la distribución de los avistamientos OVNI.

---

## ELIMINACIÓN DE REGISTROS CON VALOR `unknown` EN LAS COLUMNAS `state`, `shape` Y `shape_grouped`

En esta etapa se identifican y eliminan los registros que contienen el valor `unknown` en las columnas `state`, `shape` y `shape_grouped`.

### Justificación

La eliminación se realiza con el propósito de evitar registros cuya información no permite identificar correctamente la ubicación geográfica o la forma reportada del avistamiento.

Los criterios aplicados son:

- **`state`:** se eliminan los registros sin identificación geográfica válida, ya que no permiten realizar un análisis regional confiable.
- **`shape`:** se eliminan los registros cuya forma reportada es desconocida, debido a que no aportan información útil para la clasificación supervisada.
- **`shape_grouped`:** se eliminan los registros sin una categoría de forma identificable, evitando incorporar etiquetas desconocidas en la variable objetivo del modelo.

### Objetivo de la eliminación

Mejorar la consistencia del conjunto de datos, reducir categorías sin información útil y asegurar que los registros utilizados en el entrenamiento y evaluación del modelo dispongan de información identificable en las variables seleccionadas.

**Resultado:** se obtiene un conjunto de datos depurado, con categorías geográficas y etiquetas de clasificación identificables.

---

## FILTRADO GEOGRÁFICO — ELIMINACIÓN DE REGISTROS DE CANADÁ Y OTRAS UBICACIONES

En esta etapa se eliminan los registros correspondientes a estados y provincias de Canadá, así como las categorías agrupadas bajo `Other`, que representan ubicaciones fuera del alcance geográfico definido para el proyecto.

### Justificación

Se establece como criterio de investigación trabajar exclusivamente con reportes de avistamientos OVNI registrados dentro de los Estados Unidos.

Esta decisión se fundamenta en los siguientes aspectos:

- **Delimitación geográfica:** concentrar el análisis en un único país, manteniendo un ámbito territorial definido.

- **Homogeneidad de los datos:** evitar mezclar registros correspondientes a diferentes países y divisiones administrativas.

- **Consistencia del análisis:** facilitar la comparación de los avistamientos entre los distintos estados de Estados Unidos.

- **Análisis predictivo:** mantener una referencia geográfica uniforme para evaluar la posible relación entre la ubicación y las formas reportadas (`shape`).

### Criterio de selección

Se conservan únicamente los registros cuya ubicación geográfica corresponde a los estados de Estados Unidos. Se excluyen los registros identificados como provincias o estados de Canadá y otras ubicaciones que no pertenecen al territorio estadounidense obteniendo un conjunto de datos delimitado geográficamente a Estados Unidos, de acuerdo con el alcance establecido para la investigación.

---

TRATAMIENTO DE VALORES FALTANTES EN LA COLUMNA posted_date

En esta etapa se identifican y eliminan los registros que presentan valores en blanco o nulos en la columna posted_date, correspondiente a la fecha de publicación del reporte.

JUSTIFICACIÓN

Por motivos de calidad, confiabilidad y consistencia de los datos, se decide eliminar las filas que no cuentan con una fecha de publicación válida y verificable.

Esta decisión se fundamenta en los siguientes criterios:

Calidad de los datos: evitar registros con información temporal incompleta en la columna analizada.

Confiabilidad: conservar observaciones que permitan identificar la fecha de publicación del reporte.

Consistencia: mantener uniformidad en los registros para facilitar las tareas de validación y análisis.

Integridad del dataset: reducir la presencia de información faltante en una variable temporal relevante para la descripción de los reportes.

Criterio aplicado

Se eliminan únicamente las filas donde ´posted_date´ presenta valores nulos o en blanco Obtiendose un conjunto de datos sin registros que carecen de una fecha de publicación identificable.

---

## ELIMINACIÓN DE COLUMNAS `id`, `summary` Y `details_url`

En esta etapa se decide eliminar completamente las columnas `id`, `summary` y `details_url`, debido a que no aportan información predictiva relevante para los modelos de aprendizaje automático seleccionados en este proyecto.

### JUSTIFICACIÓN

La eliminación se fundamenta en los siguientes criterios:

- **`id`:** es un identificador único de cada registro. Su función es identificar las observaciones, pero no aporta información significativa sobre las características del avistamiento ni sobre la variable objetivo (`shape`).

- **`summary`:** contiene descripciones textuales libres de los testigos. Al tratarse de texto no estructurado, requiere técnicas específicas de procesamiento del lenguaje natural (NLP) para poder utilizarse como atributo predictivo. Estas técnicas no forman parte del alcance del presente proyecto.

- **`details_url`:** contiene enlaces a páginas externas con información complementaria de los reportes. No constituye una variable numérica o categórica directamente utilizable por los modelos seleccionados y su procesamiento requeriría una etapa adicional de extracción y transformación de información.

### Objetivo de la eliminación

Reducir la cantidad de columnas innecesarias, evitar incorporar información que no será procesada y simplificar el conjunto de datos para las etapas de entrenamiento y evaluación de los modelos de aprendizaje automático. De esta manera se obtiene un dataset con atributos estructurados y seleccionados de acuerdo con el alcance metodológico del proyecto.

---

## NORMALIZACION DE HORAS Y FORMATOS 00:00 ENTRE `duration` Y `duration_seconds`

En esta etapa se revisan y normalizan los registros de la columna duration que presentan formatos horarios como 00:00, con el propósito de interpretar correctamente las duraciones informadas y convertirlas a valores numéricos expresados en segundos en la columna duration_seconds.

---

## MODELO IMPLEMENTADO: RANDOM FOREST

Se realizaron pruebas con otros diferentes modelos de aprendizaje automático supervisado como Regresión Logística Multinomial, Arboles de decisión y KNN; tanto para las 27 variables de shape como para las 7 de shape_grouped, pero no se obtuvieron resultados significativos, es decir que estos modelos probados presentaron un desempeño inferior según las métricas de evaluación.

El modelo elegido fue Random Forest, fue seleccionado por presentar el mejor desempeño relativo, no porque necesariamente sea el mejor algoritmo para cualquier problema de clasificación.

---

## Medidas de prevención de dataleak

En el proyecto de clasificación de formas de OVNIs, las variables excluidas para evitar la fuga de datos (data leakage) y el sobreajuste incluyen principalmente las siguientes:

La variable original `shape`: Fue descartada por tratarse de la fuente directa de la cual se derivó la variable objetivo (`shape_grouped`), lo que constituiría una fuga directa de la etiqueta a predecir.

Fechas de publicación posteriores (`posted_date`, `posted_year`, `posted_month`, `posted_dayofweek`): Excluidas porque la fecha en que se reporta o publica un avistamiento en la base de datos ocurre después de este, representando información futura que no estaría disponible en un escenario de predicción real.

Versiones redundantes de duración (duration en formato de texto o variantes previas): Se descartaron para evitar duplicidad, conservando únicamente la variable numérica estandarizada (`duration_seconds`).

Variables de alta cardinalidad específica (`city`): Se omitieron campos como la ciudad exacta para evitar un sobreajuste (overfitting) severo, priorizando en su lugar atributos espaciales y contextuales más amplios como `state_grouped` y `us_region`.

Esta selección rigurosa garantiza que el modelo aprenda a partir de patrones temporales, espaciales y cuantitativos reales (`duration_seconds`, años, estaciones, etc.) y no de indicios directos de la respuesta o información del futuro.

---


> **Nota:** los reportes son descripciones aportadas por los 
> testigos y recopiladas por NUFORC. La categoría `shape` y sahpe_groupd reflejan la
> forma reportada; no es una verificación independiente de la
> naturaleza del objeto observado.

