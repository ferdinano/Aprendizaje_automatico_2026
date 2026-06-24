# Tipo de cambio

<a target="_blank" href="https://cookiecutter-data-science.drivendata.org/">
    <img src="https://img.shields.io/badge/CCDS-Project%20template-328F97?logo=cookiecutter" />
</a>

1. Descripción Detallada del Proyecto

Este proyecto de aprendizaje automático, se centra en predecir las relaciones histórica entre los
volúmenes de otorgamiento de créditos al sector privado y las fluctuaciones de la moneda
extranjera. Utilizando un conjunto de datos que detalla la evolución mensual y anual de los
préstamos hipotecarios y prendarios (desglosados por destino como construcción, refacción,
adquisición, automotores y maquinarias, tanto en pesos como en dólares), el modelo o los
modelos buscarán patrones ocultos que conecten la liquidez del mercado crediticio con la
cotización del dólar.

2. Formulación de Objetivos

Objetivo General:   
• Desarrollar y evaluar un modelo de aprendizaje automático capaz de predecir el "Tipo
de cambio y tasa de interes" mensual basándose en los volúmenes y de “préstamos hipotecarios y
prendarios otorgados en el mercado”.   
• Desarrollar y evaluar un modelo de aprendizaje automático capaz de predecir los "Creditos de hipotecarios y prendarios" a partir de la tasa de interes y tipo de cambio" cotizados en el mercado”.   
• Desarrollar y evaluar un modelo de aprendizaje automático capaz de clasificar los distintos escenarios de los creditos y poder tomar decisiones financieras.

Objetivos Específicos:

• Identificar qué líneas de financiamiento (por ejemplo, préstamos para maquinarias vs.
adquisición de automotores) presentan un mayor poder predictivo sobre los
movimientos del tipo de cambio.
• Comparar el rendimiento de al menos tres métodos de aprendizaje automático para
determinar cuál se adapta mejor a la naturaleza volátil de los datos financieros.
• Generar una herramienta analítica que permita ilustrar de forma práctica y basada en
datos las dinámicas macroeconómicas locales y el impacto de las políticas crediticias.

3. Contexto del Problema y su Relevancia

El mercado financiero argentino presenta una dinámica macroeconómica muy particular,
donde el tipo de cambio actúa como un termómetro de las expectativas y la liquidez general.
Históricamente, el acceso al crédito a largo plazo (como los hipotecarios) y a mediano plazo
(prendarios para bienes de capital o consumo) fluctúa fuertemente en función del escenario
cambiario.
La relevancia de este problema radica en su doble utilidad:
• Analítica y Financiera: Permite observar si una expansión o contracción en líneas de
crédito específicas (como el freno en préstamos en dólares o el aumento en préstamos
para la construcción en pesos) actúa como un indicador temprano (o rezagado) de
saltos devaluatorios.
• Económica: Abordar este problema con datos reales permite materializar conceptos
macroeconómicos complejos. Como, la deuda privada, la escasez de divisas y el
comportamiento del consumidor.

4. Definición del Tipo de Problema

El problema abordado se define como un Problema de Regresión. Esto se debe a que la
variable objetivo (Target) que el modelo intentará predecir es el "Tipo de cambio", la cual es
una variable cuantitativa continua, y como modelo para al toma de decisiones empresariales se realziara una prueba con un modelo de clasificacion.

5. Modelos que se podrían utilizar

Para capturar las diferentes naturalezas matemáticas de los datos económicos, se implementarán y compararán los siguientes modelos de regresión:
  a- Support Vector Machine
  b- Arbol de Decision
Para capturar las diferentes naturalezas de los datos económicos, se implementarán un modelo de clasificaciòn:
  c- K-Means


## Project Organization

```
├── LICENSE            <- Open-source license if one is chosen
├── Makefile           <- Makefile with convenience commands like `make data` or `make train`
├── README.md          <- The top-level README for developers using this project.
├── data
│   ├── external       <- Data from third party sources.
│   ├── interim        <- Intermediate data that has been transformed.
│   ├── processed      <- The final, canonical data sets for modeling.
│   └── raw            <- The original, immutable data dump.
│
├── docs               <- Objectives and dataset description, project presentation video.    
│
├── models             <- Trained and serialized models, model predictions, or model summaries
│
├── notebooks          <- Jupyter notebooks. Naming convention is a number (for ordering), final proyect.
│                         the creator's initials, and a short `-` delimited description, e.g.
│                         `Prediccion de tipo de cambio, tasa de interes y creditos- FQ`.
│
├── pyproject.toml     <- Project configuration file with package metadata for 
│                         tipo_de_cambio and configuration for tools like black
│
├── references         <- Data dictionaries, manuals, and all other explanatory materials.
│
├── reports            <- Generated analysis as HTML, PDF, LaTeX, etc.
│   └── figures        <- Generated graphics and figures to be used in reporting
│
├── requirements.txt   <- The requirements file for reproducing the analysis environment, e.g.
│                         generated with `pip freeze > requirements.txt`
│
├── setup.cfg          <- Configuration file for flake8
│
└── 

--------

