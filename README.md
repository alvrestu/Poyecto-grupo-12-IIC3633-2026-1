# Recomendación de Noticias Clickbait-aware sobre el Dataset MIND

Este repositorio contiene el código, los experimentos y el documento final de investigación (paper) para el proyecto de Sistemas Recomendadores. El objetivo principal del trabajo es desarrollar un recomendador de noticias que vaya más allá de la optimización por clics, incorporando métricas de **calidad informativa**. Para ello, se diseñó un esquema que penaliza los titulares de tipo *clickbait* y promueve la novedad y la diversidad temática en las recomendaciones.

## Dataset

El proyecto utiliza el **MIND (Microsoft News Dataset)**, específicamente la versión **MIND Small**. Este dataset es un referente en la investigación de recomendación de noticias, proveyendo tanto logs de interacciones (impresiones y clics de usuarios) como contenido textual (títulos, resúmenes, categorías) necesario para el análisis semántico.

Debbido a limitaciones de tamaño de dataset no es posible añadir el dataset directamente en este repositorio. Sin embargo, se puede acceder a este directamente desde https://msnews.github.io/#getting-start . O bien acceder directamente al drive usado por nosotros que contiene la misma data https://drive.google.com/drive/folders/1fyOWrFVm6P_uJ1ZpU0Gl3enkq150kPIT?usp=sharing.

## Contenido del Repositorio

El flujo de trabajo y la experimentación se encuentran divididos en dos cuadernos de Jupyter principales:

### 1. `FeatureEngineering_MIND_(1).ipynb`
Este notebook contiene el preprocesamiento de los datos y **Feature Engineering** asociado al proyecto. Específicamente, en este notebook se realiza lo siguiente:

- Carga y limpieza de los datos `news.tsv` y `behaviors.tsv` de MIND.
- Creación de heurísticas para medir el **Clickbait Score**, basándose en expresiones regulares (patrones léxicos engañosos), exceso de mayúsculas, uso de signos de puntuación (!, ?) y la discrepancia semántica (mismatch) entre el título y el abstract calculada con TF-IDF y similitud coseno.
- Cálculo de variables de popularidad (CTR) y novedad.

### 2. `Reranking_Diversity_Clickbait.ipynb`
Este notebook contiene la evaluación de los modelos de recomendación y el **esquema de re-ranking**:
- Implementación de un modelo base interpretable basado en **TF-IDF**.
- Aplicación de una función de penalización y bonificación para ajustar los *scores* base incorporando las métricas de clickbait, novedad y diversidad (penalización por redundancia de categorías).
- Ejecución de una búsqueda de hiperparámetros (*Grid Search*) evaluada con un **Score Balanceado** para encontrar la combinación óptima de pesos que reduzca la tasa de clickbait expuesta (*HighClickbaitRate@10*) perdiendo la menor cantidad de precisión posible (*nDCG@10*).

### Documento de Investigación
- `ICML2025_Template__Copy_ (2).pdf`: Paper siguiendo estilo ICML que contiene la documentación formal del proyecto, estado del arte, metodología, análisis de resultados (trade-off) y conclusiones.

## Autores
- Clemente Campos
- Alvaro Restuccia
- Max Reyes

*Pontificia Universidad Católica de Chile*
