# Proyecto: Análisis de Factores de Éxito en Nanotiendas (MIT LIFT Lab)

Este proyecto es un análisis de datos en profundidad realizado en colaboración con el **MIT LIFT Lab**. El objetivo principal es identificar los factores clave que contribuyen a la longevidad, el éxito y la resiliencia de las "nanotiendas" (pequeños comercios familiares) en México.

Este notebook específico (`.ipynb`) documenta la **Fase 1: Limpieza y Preprocesamiento de Datos** de la sub-base de datos "Sonora Norte".

## Objetivo del Análisis

El propósito de este notebook no es el modelado final, sino preparar el conjunto de datos para un análisis estadístico y de machine learning posterior. Un conjunto de datos limpio y bien estructurado es la base para cualquier insight confiable.

El análisis se enfoca en transformar los datos crudos de una encuesta (en formato `.xlsx`) en un DataFrame de Pandas listo para el análisis.

##  Herramientas Utilizadas

* **Python**
* **Pandas:** Para la carga, manipulación y limpieza de datos.
* **Numpy:** Para operaciones numéricas fundamentales.
* **Google Colab:** Como entorno de desarrollo.

##  Proceso Detallado de Limpieza y Transformación

El conjunto de datos original (`Datos_Primarios.xlsx`) contenía 43 columnas y 102 entradas para el campus "Sonora Norte".

### 1. Carga y Filtrado

* Se cargó la hoja "Tec_Norte" del archivo Excel.
* Se creó un DataFrame (`Son`) filtrado para contener exclusivamente las 102 entradas del campus **"Sonora Norte"**.

### 2. Manejo de Valores Nulos (Imputación y Eliminación)

Se identificaron y trataron los valores nulos de manera estratégica:

* **Eliminación de Filas:** Se detectó una fila con valores nulos en columnas críticas (ej. `Latitud Aproximada`) que carecía de datos útiles. Esta fila fue eliminada (`Son.drop()`), reduciendo el conjunto de datos a **101 entradas útiles**.
* **Imputación Estratégica:** En columnas de sentimiento (ej. `¿tuviste más, menos, o el mismo número de clientes?`), los valores nulos `NaN` se imputaron con el valor neutral (`'Igual'` o `'El mismo número de clientes'`).
    * **Justificación:** Se asumió que la ausencia de respuesta indicaba una falta de cambio significativo, siendo la opción neutral la imputación más lógica y menos sesgada.

### 3. Transformación de Datos (Object a Numérico)

Para preparar los datos para el modelado, varias columnas de tipo `object` (texto) fueron transformadas:

* **Conversión Directa:** Columnas que representaban números como texto (ej. `¿Cuántas personas trabajaron...`) fueron convertidas. El valor `'0 - Sólo trabaja el dueño o dueña'` se transformó limpiamente al valor numérico `0`.
* **Codificación Ordinal:** Las respuestas categóricas con un orden inherente (ej. "aumente", "disminuya", "permanezca igual") fueron codificadas numéricamente para reflejar su escala (ej. `Disminuya` = 1, `Permanezca igual` = 2, `Aumente` = 3). Esto se aplicó a múltiples columnas de expectativas (trabajadores, clientes, etc.).

##  Resultados de esta Fase

El resultado de este notebook es un DataFrame de Pandas (`Son`) completamente limpio, sin valores nulos y con las variables categóricas relevantes codificadas numéricamente.

* **Entradas Finales:** 101
* **Columnas:** 43
* **Estado:** Listo para la Fase 2 (Análisis Exploratorio de Datos y Modelado).

##  Próximos Pasos

Con este conjunto de datos limpio, los siguientes pasos en el análisis (probablemente en un notebook separado) son:

1.  **Análisis Exploratorio de Datos (EDA):** Creación de visualizaciones para entender la distribución de las variables y encontrar correlaciones.
2.  **Modelado de Machine Learning:** Aplicación de modelos como K-means clustering (para segmentar los tipos de tiendas) y Regresión Lineal/Logística (para identificar qué variables predicen el éxito).
