

# Clasificación de la forma reportada en avistamientos de OVNIS en Estados Unidos mediante aprendizaje automático
---

![Imagen de portada](reports/figures/02%20-%20formas%20-%20shape.jpg)

 
 ## Índice

 Accesos rápidos:


- [1. Descripción del Proyecto](#descripción-del-proyecto)
- [2. Relevancia del problema](#relevancia-del-problema)
- [3. Pregunta e Hipótesis](#relevancia-del-problema)
- [4. Tipo de Problema](#4-tipo-de-problema)
- [5. Objetivo General](#objetivo-general)
 - [5.1. Objetivos Especificos](#objetivos-específicos)
- [6. Fuente de los Datos](#fuente-de-los-datos)
 - [6.1. Acerca de la fuente de información](#acerca-de-la-fuente-de-información)
- [7. Organización del proyecto](#organización-del-proyecto)
- [8. Conclusiones Generales](#6-conclusiones-generales)
- [9. Mejor modelo seleccionado](#7-Mejor-Modelo-Seleccionado)
- [10. proyectos a futuro](#8-Aporte-a-Tierra-del-Fuego)
- 📘 [10. Notebooks del Proyecto](#9-notebooks-del-proyecto)
- 📄 [11. Informes Tecnicos del Proyecto](#10-informes-tecnicos-del-proyecto)
- 🎥 [12. Video Presentacion del Proyecto](#11-video-presentacion-del-proyecto)

---

## Descripción del proyecto

Este proyecto que tiene como objetivo desarrollar un modelo de aprendizaje automático supervisado capáz de clasificar los reportes de avistamientos de UFO/UAP (OVNIS, objetos voladores no identificados) según la forma con la que los testigos describieron dichos objetos observados.

[⬆️ Volver al índice](#Índice)

---

## Relevancia del problema

Este proyecto utiliza el conjunto de datos **NUFORC UFO Sightings**, una recopilación de reportes de avistamientos de objetos voladores no identificados (OVNIs) registrados por testigos. A partir de su análisis, se estudiarán las características temporales, geográficas y de duración de los avistamientos ocurridos en los Estados Unidos de América. 
El modelo intentará predecir la categoría de forma de un reporte OVNI, pero cabe aclarar que no anticipará cuándo o dónde ocurrirá un avistamiento.
El modelo NO busca determinar la existencia de vida extraterrestre ni comprobar la naturaleza de los objetos observados.

[⬆️ Volver al índice](#Índice)

### Pregunta de Investigación e Hipótesis

¿Es posible predecir con precisión la forma de un objeto volador no identificado a partir de las 
características temporales, geográficas, de duración de los avistamientos?

[⬆️ Volver al índice](#Índice)

## Tipo de problema

Clasificación supervisada multiclase

[⬆️ Volver al índice](#Índice)

## Objetivo General

Intentar clasificar la categoría de la forma de un reporte mediante la aplicación de técnicas de Aprendizaje Automático supervisado mediante clasificación multiclase. Se busca identificar patrones y evaluar la capacidad de los modelos para predecir la forma reportada del objeto (shape) según las características disponibles.

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
│   Readme.md
│   requirements.txt
│
├───data
│   ├───interim
│   │       Datos intermedios.txt
│   │
│   ├───processed
│   │       A confirmar.txt
│   │       dataset_procesado.csv
│   │
│   └───raw
│           clean_ufo_data.csv
│
├───docs
│       01_Objetivos_y_Alcance_del_Proyecto.md
│       02_Analisis_exploratorio.md
│
├───models
│       Pendiente.txt
│
├───notebooks
│   ├───01 - Preprocesamiento y Escalado
│   │       01_Limpieza_y_Preprocesamiento_.ipynb
│   │       02_Datos_Limpios_y_Preparados_.ipynb
│   │
│   └───02 - Modelos
│           Pendiente.txt
│
└───reports
    └───figures
            Pendiente.txt

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

## 8. Conclusiones Generales

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

[⬆️ Volver al índice](#Índice)

## 9. Notebooks del Proyecto

- 📘 [`01_Limpieza_y_Preprocesamiento.ipynb`](notebooks/01 - Preprocesamiento y Escalado/01_Limpieza_y_Preprocesamiento_.ipynb)
- 📘 [`02_Datos_Limpios_y_Preparados.ipynb`](notebooks/01 - Preprocesamiento y Escalado/02_Datos_Limpios_y_Preparados.ipynb)
- 📘 [`01_Entrenamiento_del_Modelo.ipynb`](notebooks/Validacion_Optimizacion_Metricas_TEA.ipynb)

## 10. Informes Tecnicos del Proyecto

- 📄 [`Objetivos y alcance del proyecto`](docs/01_Objetivos_y_Alcance_del_Proyecto.md)
- 📄 [`Análisis exploratorio`](docs/02_Analisis_exploratorio.md)

[⬆️ Volver al índice](#Índice)


## 11. Video Presentacion del Proyecto

Podés acceder al video de presentación en el siguiente enlace de Google Drive:

[🎥 Ver video en Google Drive](https://drive.goo.....)

> Este video resume el objetivo, metodología y resultados del proyecto de clasificación de la forma reportada en avistamientos de OVNIS en Estados Unidos mediante Aprendizaje Automático.

[⬆️ Volver al índice](#Índice)
