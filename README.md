# Proyecto: Análisis y Clustering de Nanotiendas (MIT LIFT Lab)

Este repositorio contiene un análisis de datos en profundidad realizado en colaboración con el **MIT LIFT Lab**. 
El objetivo es identificar patrones y segmentar "nanotiendas" (pequeños comercios) en Sonora, México, para entender sus características y factores de éxito.

El proyecto abarca el ciclo completo de análisis de datos, desde la limpieza y preprocesamiento de una base de datos de encuestas (`.xlsx`) hasta la aplicación de modelos de machine learning no supervisado (Clustering y PCA) para descubrir estructuras ocultas en los datos.

##  Objetivos Clave

1.  **Limpieza y Preprocesamiento:** Transformar los datos crudos de una encuesta (con valores nulos, texto y formatos inconsistentes) en un conjunto de datos numérico y limpio, listo para el análisis.
2.  **Ingeniería de Características (Feature Engineering):** Crear nuevas variables significativas (como 'Antigüedad' y 'Horas Abierto') a partir de los datos existentes.
3.  **Análisis Exploratorio (EDA):** Entender la relación entre las variables clave (ej. antigüedad, horas de trabajo, edad del dueño) mediante un mapa de calor de correlación.
4.  **Segmentación de Tiendas (Clustering):** Utilizar K-Means para agrupar las tiendas en clusters distintos basados en sus características operativas y demográficas.
5.  **Visualización:** Usar Análisis de Componentes Principales (PCA) para visualizar los clusters en un gráfico 2D.

##  Herramientas y Librerías

* **Python 3**
* **Pandas:** Para la carga, manipulación y limpieza de datos.
* **Numpy:** Para operaciones numéricas.
* **Matplotlib & Seaborn:** Para la visualización de datos (mapa de calor, gráfico de dispersión).
* **Scikit-learn:** Para las siguientes tareas de Machine Learning:
    * `StandardScaler`: Estandarización de características.
    * `KMeans`: Para el algoritmo de clustering.
    * `silhouette_score`: Para la validación y selección del número óptimo de clusters.
    * `PCA`: Para la reducción de dimensionalidad.
* **Google Colab:** Como entorno de desarrollo.

---

##  Metodología y Pipeline del Proyecto

El análisis se estructuró en los siguientes pasos:

### 1. Carga y Filtrado de Datos
* Se cargó la hoja `Tec_Norte` del archivo `Datos_Primarios.xlsx`.
* Se creó un DataFrame (`Son`) filtrado para contener exclusivamente las **102 entradas** del campus "Sonora Norte".

### 2. Limpieza y Preprocesamiento (Data Cleaning)
Esta fue la fase más intensiva del proyecto:
* **Manejo de Nulos (Imputación y Eliminación):**
    * Se eliminó una fila (`toDrop`) que contenía valores nulos en columnas críticas (ej. `Latitud Aproximada`), reduciendo el dataset a 101 entradas útiles.
    * Se imputaron valores nulos en columnas categóricas de sentimiento (ej. `¿tuviste más... clientes?`) con el valor neutral (`'Igual'`), asumiendo que la falta de respuesta indicaba una falta de cambio.
    * Se imputaron valores nulos en columnas numéricas (ej. `Edad del dueño`, `Año de apertura`) con la **media** de la columna después de una limpieza inicial.
* **Transformación de Datos (Text-to-Numeric):**
    * **Codificación Ordinal:** Se convirtieron respuestas categóricas (ej. "Aumente", "Disminuya", "Permanezca igual") a valores numéricos (`1`, `2`, `3`) para permitir el análisis de correlación.
    * **Limpieza de Texto:** Se eliminaron respuestas no numéricas (ej. 'No sabe / No contesta') de columnas como `Edad del dueño o dueña` antes de convertirlas a tipo `float`.
    * **Conversión Directa:** Valores como `'0 - Sólo trabaja el dueño o dueña'` se transformaron al entero `0`.

### 3. Ingeniería de Características (Feature Engineering)
Se crearon dos nuevas variables de alto valor para el análisis:
1.  **`Horas Abierto`**: Se calcularon las horas de operación diarias restando `Horario de cierre` menos `Horario de apertura`.
2.  **`Antigüedad`**: Se calculó la antigüedad del negocio restando el `Año de apertura del negocio` del año actual (2024).

### 4. Análisis Exploratorio de Datos (EDA)
* Se generó un resumen estadístico (`.describe()`) de todas las variables numéricas.
* Se creó un **mapa de calor de correlación** (`sns.heatmap`) para visualizar la relación lineal entre todas las variables numéricas del dataset.

### 5. Machine Learning: Clustering (K-Means)
El objetivo era segmentar las tiendas en grupos con características similares.
1.  **Selección de Características:** Se seleccionó un subconjunto de variables clave para el clustering: `Antigüedad`, `Horas Abierto` y `Edad del dueño o dueña`.
2.  **Estandarización:** Los datos se escalaron usando `StandardScaler` para asegurar que ninguna variable dominara el modelo debido a su escala.
3.  **Optimización de K:** Se utilizó el **método del codo** y el **Silhouette Score** para determinar el número óptimo de clusters. El Silhouette Score más alto se obtuvo con **k=4 clusters**.
4.  **Entrenamiento:** Se entrenó el modelo K-Means con `n_clusters=4` y se asignó una etiqueta de cluster a cada tienda.

### 6. Visualización con PCA (Análisis de Componentes Principales)
Para visualizar los 4 clusters (que existían en 3 dimensiones), se utilizó PCA para reducir la dimensionalidad a 2 componentes.
* Se aplicó PCA a los datos escalados.
* Se generó un **gráfico de dispersión (scatter plot)** de los dos componentes principales (Componente 1 vs. Componente 2).
* Los puntos en el gráfico se colorearon según su etiqueta de cluster (k=4), permitiendo una visualización clara de la separación y la estructura de los grupos de nanotiendas.

##  Resultados

El resultado final es un análisis completo que no solo limpia y prepara los datos, sino que también identifica **4 segmentos distintos** de nanotiendas en Sonora basados en su antigüedad, horas de operación y la edad de sus dueños.

*(El notebook `.ipynb` en este repositorio contiene todo el código, la limpieza detallada, el análisis y las visualizaciones).*
