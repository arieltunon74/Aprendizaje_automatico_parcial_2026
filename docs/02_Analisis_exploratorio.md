# ANÁLISIS EXPLORATORIO - DESCRIPCIÓN DEL DATASET

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
(`int64`); las otras ocho columnas aparecen con tipo `object`. 
Las fechas están representadas como texto y podrían convertirse a un tipo temporal
pero EL PROCESAMIENTO DE DICHOS TEXTOS NO SERÁ TENIDO EN CUENTA dentro del alcance de este proyecto.

---

# Reporte de Limpieza y Estandarización del Dataset

## DETECCIÓN DE VALORES NULOS - DUPLICADOS - INCOSISTENCIAS (EN EL DATASET)

### No se detectaron valores duplicados

## Conteo de Valores Nulos

A continuación se presenta la cantidad de valores nulos detectados en cada una de las columnas del dataset, ordenados de mayor a menor frecuencia:
```
| Columna | Valores Nulos |
| :--- | :---: |
| `state` | **8,714** |
| `duration` | **4,372** |
| `shape` | **4,098** |
| `city` | **261** |
| `occurred_date_time` | **61** |
| `summary` | **37** |
```
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
|---|---|---|
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

| Término | Significado | Descripción |
|---|---|---|
| **Sighting** | Avistamiento | Observación visual de un objeto o fenómeno, generalmente realizada por uno o varios testigos. |
| **UFO** | Unidentified Flying Object (Objeto Volador No Identificado - OVNI) | Término utilizado para describir un objeto observado en el cielo cuya identidad no ha podido determinarse. |
| **UAP** | Unidentified Anomalous Phenomena (Fenómenos Anómalos No Identificados) | Término más amplio que UFO, utilizado para referirse a fenómenos anómalos que no han podido identificarse en diferentes entornos. |

## 4. Consideraciones sobre las variables

- **Variable objetivo (`shape`):** Es la categoría que el modelo de aprendizaje automático intentará predecir.
- **Variables predictoras:** podrán seleccionarse a partir de las características temporales, geográficas y de duración de los avistamientos.
- **Identificadores y referencias:** `id` y `details_url` se utilizan principalmente para identificar y consultar los registros, por lo que no se consideran inicialmente variables predictoras.
- **Información textual:** `summary` contiene descripciones de los testigos, no se tendrá en cuenta para los análisis.
- **Fecha de publicación:** `posted_date` puede utilizarse para generar características temporales y evaluar su posible aporte al modelo.



## 6. Consideraciones sobre el dataset

La cantidad de registros y los tipos de datos indicados corresponden a
la carga inicial observada en el notebook 01_Limpieza_y_Preprocesamiento.ipynb.

Los datos nulos, las inconsistencias, las categorías poco frecuentes y las transformaciones
que se apliquen se documentarán en las etapas posteriores del
proyecto, sin confundir esta descripción del origen y la composición del
dataset con el informe completo del análisis exploratorio o del
preprocesamiento.

> **Nota:** los reportes son descripciones aportadas por los 
> testigos y recopiladas por NUFORC. La categoría `shape` refleja la
> forma reportada; no es una verificación independiente de la
> naturaleza del objeto observado.

