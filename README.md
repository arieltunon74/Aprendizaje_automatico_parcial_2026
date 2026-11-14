
![Banner del proyecto](reports/figures/01%20-%20BANNER.png)

---

### Alumno: Ariel Tuñon
### Parcial de Aprendizaje Automático 2026
### Politécnico Superior Malvinas Argentinas

---

 ## Índice

 Accesos rápidos:


- [1. Descripción del Proyecto](#descripción-del-proyecto)
- [2. Relevancia del problema](#relevancia-del-problema)
- [3. Pregunta e Hipótesis](#relevancia-del-problema)
- [4. Tipo de Problema](#Tipo-de-problema)
- [5. Objetivo General](#objetivo-general)
 - [5.1. Objetivos Especificos](#objetivos-específicos)
- [6. Fuente de los Datos](#fuente-de-los-datos)
 - [6.1. Acerca de la fuente de información](#acerca-de-la-fuente-de-información)
- [7. Organización del proyecto](#organización-del-proyecto)
- 📘 [08. Notebooks del Proyecto](#9-notebooks-del-proyecto)
- 📄 [09. Informes Tecnicos del Proyecto](#10-informes-tecnicos-del-proyecto)
- 🎥 [10. Video Presentacion del Proyecto](#11-video-presentacion-del-proyecto)

---

## Descripción del proyecto

Este proyecto que tiene como objetivo desarrollar un modelo de aprendizaje automático supervisado capáz de clasificar los reportes de avistamientos de UFO/UAP (OVNIS, objetos voladores no identificados) según la forma con la que los testigos describieron dichos objetos observados.

---

## Relevancia del problema

Este proyecto utiliza el conjunto de datos **NUFORC UFO Sightings**, una recopilación de reportes de avistamientos de objetos voladores no identificados (OVNIs) registrados por testigos. A partir de su análisis, se estudiarán las características temporales, geográficas y de duración de los avistamientos ocurridos en los Estados Unidos de América. 
El modelo intentará predecir la categoría de forma de un reporte OVNI, pero cabe aclarar que no anticipará cuándo o dónde ocurrirá un avistamiento.
El modelo NO busca determinar la existencia de vida extraterrestre ni comprobar la naturaleza de los objetos observados.

### Pregunta de Investigación e Hipótesis

¿Es posible predecir con precisión la forma de un objeto volador no identificado a partir de las 
características temporales, geográficas, de duración de los avistamientos?

[⬆️ Volver al índice](#Índice)

## Tipo de problema


Clasificación supervisada multiclase


## Objetivo General

Intentar clasificar la categoría de la forma de un reporte mediante la aplicación de técnicas de Aprendizaje Automático supervisado mediante clasificación multiclase. Se busca identificar patrones y evaluar la capacidad de los modelos para predecir la forma reportada del objeto (shape) según las características disponibles.

![Imagen de portada](reports/figures/02%20-%20formas%20-%20shape.jpg)

[⬆️ Volver al índice](#Índice)

### Objetivos específicos

Se buscará desarrollar modelos de aprendizaje automático que permitan predecir la forma reportada por los testigos en dichos avistamientos, a partir de las características disponibles en el conjunto de datos.

**Clasificación**: el modelo asigna una categoría

**Predicción**: el modelo estima cuál es la categoría más probable según los patrones aprendidos

**Variable objetivo: shape** Es la forma con la que los testigos describieron al objeto volador no identificado, mientras que las demás características disponibles se emplearán como variables predictoras para evaluar la capacidad de los algoritmos de aprendizaje automático para intentar identificar patrones y estimar la categoría correspondiente a cada avistamiento reportado.

Cabe aclarar que NO anticipará cuándo o dónde ocurrirá un avistamiento; No identifica visualmente el objeto ni verifica qué era realmente.


[⬆️ Volver al índice](#Índice)

---

## Fuente de los Datos

Los datos utilizados provienen de la organización NUFORC (National UFO Reporting Center o Centro Nacional de Informes de Ovnis) 
Es una organización privada y sin fines de lucro en el estado de Washington, Estados Unidos, dedicada a recibir, registrar, analizar y difundir públicamente reportes de avistamientos de UFO/OVNIS y UAP (Fenómenos Aéreos No Identificados). Fue creada en el año 1974 y lleva operando más de 50 años como un punto central de recepción de testimonios.
Web Site: https://nuforc.org/ 

La fuente se encuentra en idioma inglés de origen, por lo que los nombres de las columnas, las categorías y las descripciones de los avistamientos están expresados en dicho idioma. Existen datasets derivados de estos registros de NUFORC que contienen más de 120.000 observaciones, con variables como datetime, city, state, country, shape, duration, comments, latitude y longitude. El dataset primario utilizado para este proyecto se extrae del siguiente repositorio: https://www.kaggle.com/datasets/thaddeussegura/ufo-sightings

Data scraped from the National UFO reporting center – By Thaddeus Segura - (DbCL) v1.0


[⬆️ Volver al índice](#Índice)

### Acerca de la fuente de información:

Cada entrada en la base de datos de NUFORC es un avistamiento informado, acompañado de múltiples atributos que describen aspectos propios del evento. Entre estos atributos se encuentran marcadores temporales como fecha de publicación y la fecha y hora exactas en que ocurrió el avistamiento. Esto permite realizar análisis cronológicos para identificar patrones o tendencias basados en períodos de mayor o menor actividad. 
La información geográfica también se detalla, con campos que indican la ciudad, el estado o provincia de EEUU y también de otras partes del mundo (en blanco).

**UFO y UAP** son dos siglas en inglés utilizadas para referirse a fenómenos observados en el cielo cuya naturaleza no está identificada. 

 UFO (Unidentified Flying Object): Objeto Volador No Identificado (OVNI). Es un objeto observado en el aire que no ha podido identificarse. 

 UAP (Unidentified Anomalous Phenomena): Fenómenos Anómalos No Identificados. Es un término más amplio que incluye observaciones inexplicables en el aire, el espacio, el mar o entre distintos medios. Anteriormente, UAP también se utilizaba para Unidentified Aerial Phenomena (Fenómenos Aéreos No Identificados). 

**Importante**: que algo sea un UFO / OVNI o UAP no significa que sea de origen extraterrestre. Puede tratarse de aviones, drones, globos, fenómenos atmosféricos u objetos cuya naturaleza todavía se desconoce. Por lo tanto, el objetivo no es determinar si un avistamiento corresponde realmente a una nave extraterrestre, sino analizar los patrones existentes en los reportes registrados por los testigos y que fueron recolectados en la base de datos de NUFORC para luego utilizar modelos de Aprendizaje Automático para intentar predecir la categoría de forma informada en un nuevo registro.


[⬆️ Volver al índice](#Índice)

---

# Organización del Proyecto

El repositorio se encuentra organizado siguiendo los principios de la plantilla Cookiecutter Data Science.

<a target="_blank" href="https://cookiecutter-data-science.drivendata.org/">
    <img src="https://img.shields.io/badge/CCDS-Project%20template-328F97?logo=cookiecutter" />
</a>

```
|   Readme.md
|
+---data
|   +---interim
|   |       dataset_procesado-tests.csv
|   |       Datos intermedios.txt
|   |
|   +---processed
|   |       dataset_procesado.csv
|   |
|   \---raw
|           clean_ufo_data.csv
|           Dataset_crudo_from_Kaggle.com.txt
|
+---docs
|       01_Objetivos_y_Alcance_del_Proyecto.md
|       02_Analisis_exploratorio.md
|       Readme.md
|
+---models
|       Prueba_y_entrenamiento_con_otros_Modelos.ipynb
|       Readme.md
|
+---notebooks
|   +---01 - Preprocesamiento y Escalado
|   |       01_Limpieza_y_Preprocesamiento.ipynb
|   |       02_Datos_Limpios_y_Preparados.ipynb
|   |
|   \---02 - Modelos
|           01_Entrenamiento_del_Modelo.ipynb
|
\---reports
    \---figures
            01 - BANNER.png
            02 - formas - shape.jpg
            03-UFO-UAP-OVNIS.jpg
            04-DISTRIBUCION_shape_Y_shape_grouped.jpg
            05-EEUU-REGIONES.jpg
            06-DISTRIBUCIÓN_REGIONES_EEUU.jpg
            07-DISTRIBUCIONES_TEMPORALES.jpg
            08-AVISTAMIENTOS_POR_AÑO.jpg
            09-MATRIZ_CONFUSION_RANDOM_FORESTjpg.jpg
            10-RANDOM_FOREST_ESQUEMA.jpg
            11-CARACTERISTICAS_EN_RANDOM_FOREST.jpg
            12-DISTRIBUCIÓN_REAL_Y_PREDICHA_RANDOM_FOREST.jpg
            13-METRICAS_POR_CATEGORIAS_RANDOM_FORESTjpg.jpg
            14-CURVAS_ROC_RANDOM_FOREST.jpg
            15-HEATMAP_AVISTAMIENTOS POR DIA Y HORA.jpg

```
Tecnologías Utilizadas

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-Learn
- Jupyter Notebook
- Git
- GitHub

[⬆️ Volver al índice](#Índice)
---

## 9. Notebooks del Proyecto

- 📘 [`01_Limpieza_y_Preprocesamiento.ipynb`](notebooks/01%20-%20Preprocesamiento%20y%20Escalado/01_Limpieza_y_Preprocesamiento.ipynb)

- 📘 [`02_Datos_Limpios_y_Preparados.ipynb`](notebooks/01%20-%20Preprocesamiento%20y%20Escalado/02_Datos_Limpios_y_Preparados.ipynb)

- 📘 [`01_Entrenamiento_del_Modelo.ipynb`](notebooks/02%20-%20Modelos/01_Entrenamiento_del_Modelo.ipynb)


## 10. Informes Tecnicos del Proyecto

- 📄 [`Objetivos y alcance del proyecto`](docs/01_Objetivos_y_Alcance_del_Proyecto.md)

- 📄 [`Análisis exploratorio`](docs/02_Analisis_exploratorio.md)


[⬆️ Volver al índice](#Índice)


## 11. Video Presentacion del Proyecto

Podés acceder al video de presentación en el siguiente enlace de Google Drive:

[🎥 Ver video en Google Drive](https://drive.goo.....)

> Este video resume el objetivo, metodología y resultados del proyecto de clasificación de la forma reportada en avistamientos de OVNIS en Estados Unidos mediante Aprendizaje Automático.


[⬆️ Volver al índice](#Índice)
