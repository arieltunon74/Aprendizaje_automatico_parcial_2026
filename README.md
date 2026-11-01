# PROYECTO DE APRENDIZAJE AUTOMÁTICO

# Clasificación de la forma reportada en avistamientos de OVNIS en Estados Unidos mediante aprendizaje automático

## Autor: Ariel Tuñón
## Institución: Centro Politécnico Superior Malvinas Argentinas  

## Descripción

Este repositorio contiene el proyecto que tiene como objetivo desarrollar un modelo de aprendizaje automático supervisado capáz de clasificar los reportes de avistamientos de UFO/UAP (OVNIS, objetos voladores no identificados) según la forma (shape) con la que los testigos describieron dichos objetos observados.

Para ello, se identificarán y analizarán características temporales, geográficas y de duración para poder detectar posibles patrones de relaciones, regularidades o características que el modelo puede aprender a partir de los datos para intentar predecir la forma reportada en los avistamientos registrados en los Estados Unidos de América.

La variable objetivo del modelo será shape, es decir, la forma con la que los testigos describieron al objeto volador no identificado, mientras que las demás características disponibles se emplearán como variables predictoras para evaluar la capacidad de los algoritmos de aprendizaje automático para identificar patrones y estimar la categoría correspondiente a cada avistamiento.

El modelo intentará predecir la categoría de forma de un reporte, pero cabe aclarar que sno anticipará cuándo o dónde ocurrirá un avistamiento.

---

# Tipo de problema

Clasificación supervisada multiclase

# Objetivo General

Intentar clasificar la categoría de la forma de un reporte mediante la aplicación de técnicas de Aprendizaje Automático supervisado mediante clasificación multiclase.
Se busca identificar patrones y evaluar la capacidad de los modelos de aprendizaje automático para predecir la forma reportada del objeto (shape) según las características disponibles.

Clasificación: el modelo asigna una categoría
Predicción: el modelo estima cuál es la categoría más probable según los patrones aprendidos
Variable objetivo: shape (forma reportada del objeto según los testigos)

Cabe aclarar que no anticipará cuándo o dónde ocurrirá un avistamiento; No identifica visualmente el objeto ni verifica qué era realmente.

---

# Objetivos Específicos

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

Importante:

Este análisis NO busca determinar la existencia de vida extraterrestre ni comprobar la naturaleza de los objetos observados.
El modelo estaría aprendiendo a partir de reportes humanos registrados en NUFORC, no estaría identificando científicamente qué objetos son realmente OVNIS/ UFO/ UAP. 

---

# Fuente de los Datos

Los datos utilizados provienen de la siguiente organización:

NUFORC (National UFO Reporting Center o Centro Nacional de Informes de Ovnis) 

Es una organización privada y sin fines de lucro en el estado de Washington, Estados Unidos, dedicada a recibir, registrar, analizar y difundir públicamente reportes de avistamientos de UFO/OVNIS y UAP (Fenómenos Aéreos No Identificados). Fue creada en el año 1974 y lleva operando más de 50 años como un punto central de recepción de testimonios.
Web Site: https://nuforc.org/ 

La fuente se encuentra en idioma inglés de origen, por lo que los nombres de las columnas, las categorías y las descripciones de los avistamientos están expresados en dicho idioma.

Existen datasets derivados de estos registros de NUFORC que contienen más de 120.000 observaciones, con variables como datetime, city, state, country, shape, duration, comments, latitude y longitude. El dataset primario utilizado para este proyecto se extrae del siguiente repositorio: 

https://www.kaggle.com/datasets/thaddeussegura/ufo-sightings

Data scraped from the National UFO reporting center – By Thaddeus Segura - (DbCL) v1.0 

**clean\_ufo\_data.csv (23.34 MB)**

---

# Acerca de la fuente de información:

Cada entrada en la base de datos de NUFORC es un avistamiento informado, acompañado de múltiples atributos que describen aspectos propios del evento. Entre estos atributos se encuentran marcadores temporales como fecha de publicación y la fecha y hora exactas en que ocurrió el avistamiento. Esto permite realizar análisis cronológicos para identificar patrones o tendencias basados en períodos de mayor o menor actividad. 
La información geográfica también se detalla, con campos que indican la ciudad, el estado o provincia de EEUU y también de otras partes del mundo (en blanco).

**UFO y UAP** son dos siglas en inglés utilizadas para referirse a fenómenos observados en el cielo cuya naturaleza no está identificada. 

 UFO (Unidentified Flying Object): Objeto Volador No Identificado (OVNI). Es un objeto observado en el aire que no ha podido identificarse. 

 UAP (Unidentified Anomalous Phenomena): Fenómenos Anómalos No Identificados. Es un término más amplio que incluye observaciones inexplicables en el aire, el espacio, el mar o entre distintos medios. Anteriormente, UAP también se utilizaba para Unidentified Aerial Phenomena (Fenómenos Aéreos No Identificados). 

**Importante**: que algo sea un UFO / OVNI o UAP no significa que sea de origen extraterrestre. Puede tratarse de aviones, drones, globos, fenómenos atmosféricos u objetos cuya naturaleza todavía se desconoce. Por lo tanto, el objetivo no es determinar si un avistamiento corresponde realmente a una nave extraterrestre, sino analizar los patrones existentes en los reportes registrados por los testigos y que fueron recolectados en la base de datos de NUFORC para luego utilizar modelos de Aprendizaje Automático para intentar predecir la categoría de forma informada en un nuevo registro. 


---


## Características Generales

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

El dataset final fue construido mediante la integración de las columnas...

Cada fila representa un avistamiento informado, acompañado de múltiples atributos que describen aspectos propios del evento. 

---

# Diccionario de Variables

| Variable | Descripción |
|-----------|-------------|



---

# Metodología

El proyecto fue desarrollado siguiendo las etapas clásicas de un flujo de trabajo de Ciencia de Datos:

1. Obtención de datos.
2. Limpieza y preparación.
3. Integración de datasets.
4. Construcción de variables derivadas.
5. Análisis exploratorio de datos.

   En progreso...

---

# Modelos Utilizados

En progreso...

---

# Organización del Proyecto

El repositorio se encuentra organizado siguiendo los principios de la plantilla Cookiecutter Data Science.

<a target="_blank" href="https://cookiecutter-data-science.drivendata.org/">
    <img src="https://img.shields.io/badge/CCDS-Project%20template-328F97?logo=cookiecutter" />
</a>

```
PROYECTO_APRENDIZAJE_AUTOMATICO/
│
├── README.md
├── requirements.txt
│
├── data/
│   ├── raw/
│   │   └── clean_ufo_data.csv
│   ├── interim/
│   │   └── dataset_procesado.csv
│   └── processed/
│
├── docs/
│   ├── 01_Objetivos_y_Alcance_del_Proyecto.md
│   └── 02_Analisis_exploratorio.md
│
├── models/
│   └── .gitkeep
│
├── notebooks/
│   ├── .gitkeep
│   ├── 01 - Preprocesamiento y Escalado/
│   │   └── 01_Limpieza_y_Preprocesamiento_.ipynb
│   └── 02 - Modelos/
│
└── reports/
    ├── .gitkeep
    └── figures/
        └── .gitkeep

```
---

# Tecnologías Utilizadas

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-Learn
- Jupyter Notebook
- Git
- GitHub

---

# Principales Resultados

En progreso...

