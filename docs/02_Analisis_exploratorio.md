# Análisis exploratorio: descripción del dataset

## 1. Descripción general

Este proyecto utiliza el conjunto de datos **NUFORC UFO Sightings**, una
recopilación de reportes de avistamientos de objetos voladores no
identificados (UFO/OVNIs). El dataset contiene información sobre la
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
filtros y las transformaciones posteriores realizados durante el
trabajo.

## 4. Variables disponibles

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

  `posted_date`                       Fecha en la que se publicó el
                                      reporte.
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
(`int64`); las otras ocho columnas aparecen con tipo `object`. Esto
describe cómo están almacenados los datos en el DataFrame y no
necesariamente su naturaleza semántica. Por ejemplo, las fechas están
representadas como texto y podrían convertirse a un tipo temporal
durante una etapa posterior de preparación.

## 6. Consideraciones sobre el dataset

La variable `shape` contiene las categorías descriptivas de la forma
registrada en cada reporte y se utiliza como objetivo de clasificación
multiclase. Las demás variables constituyen la información disponible
para estudiar y preparar posibles características predictoras, de
acuerdo con el alcance del proyecto.

La cantidad de registros y los tipos de datos indicados corresponden a
la carga inicial observada en el notebook. Los valores ausentes, las
inconsistencias, las categorías poco frecuentes y las transformaciones
que se apliquen se documentarán en las etapas correspondientes del
proyecto, sin confundir esta descripción del origen y la composición del
dataset con el informe completo del análisis exploratorio o del
preprocesamiento.

> **Nota:** los reportes representan descripciones aportadas por
> testigos y recopiladas por NUFORC. La categoría `shape` refleja la
> forma reportada; no constituye una verificación independiente de la
> naturaleza del objeto observado.
