# Análisis Exploratorio de Datos de la Pandemia de COVID-19 en EE.UU.

Este estudio consiste en un análisis exploratorio de datos (EDA) sobre la pandemia de COVID-19 en los Estados Unidos, utilizando datos diarios a nivel estatal. El análisis se realizó utilizando bibliotecas de Python como `pandas`, `numpy`, `matplotlib` y `seaborn`.

## Obtención y Preparación de los Datos

### Obtención de Datos:
- Los datos se obtuvieron de una API a través de la URL [https://api.covidtracking.com/v1/states/daily.csv](https://api.covidtracking.com/v1/states/daily.csv) utilizando la biblioteca `requests`.
- Se creó un DataFrame de `pandas` a partir de estos datos.
- Se seleccionaron las columnas relevantes para el análisis.
- La columna `date` se convirtió al formato `datetime`.
- Los datos fueron ordenados por estado y fecha.

## Análisis Descriptivo y Datos Faltantes

### Análisis Inicial:
- Se realizó un análisis descriptivo inicial del DataFrame utilizando `df.info()`, `df.describe()` y la herramienta `ydata-profiling`.
- Los histogramas de las variables revelaron una fuerte asimetría positiva con una gran acumulación de datos en los valores de 0.

### Datos Faltantes:
- Se identificó una cantidad significativa de datos faltantes en varias columnas, incluyendo `death`, `hospitalizedCurrently` y `hospitalizedCumulative`.
- Se calculó el porcentaje de datos faltantes para estas columnas, revelando múltiples estados con ausencia total de datos, lo que llevó a optar por no imputar los datos.
- Se visualizaron los estados con más del 15% de datos faltantes por columna.
- Los valores faltantes en la columna `death` (la única con menos del 15%) se imputaron utilizando la mediana, ya que la distribución no sigue una forma normal.

## Análisis de Casos Positivos

### Identificación de los Estados con Más Casos:
- Se determinó que los estados con el mayor número de casos positivos son California (CA), Texas (TX), Florida (FL) y Nueva York (NY), siendo California el estado con más de 3.5 millones de casos.

### Análisis del 80% de los Casos Positivos:
- Se identificaron los estados que representan aproximadamente el 80% del total de casos positivos reportados, enfocando el análisis en las áreas más afectadas.

## Análisis de Outliers

### Análisis de Muertes Diarias (`deathIncrease`):
- Se analizaron las tendencias de muertes diarias (`deathIncrease`) para los estados que representan el 80% de los casos positivos.
- Se crearon diagramas de caja para visualizar la distribución y se aplicó una función para eliminar los valores atípicos por estado utilizando el rango intercuartílico (IQR).
- Los valores atípicos, como aumentos negativos de muertes (o “resucitaciones”), se consideraron errores de datos y se ajustaron.

### Análisis de Casos Positivos y Hospitalizaciones:
- Se realizaron análisis similares para los casos positivos (`positiveIncrease`) y hospitalizaciones (`hospitalizedIncrease`), eliminando valores atípicos.

## Análisis de Tendencias Temporales

### Media Móvil:
- Se calculó una media móvil de `deathIncrease` agrupada por estado para suavizar las fluctuaciones diarias y observar las tendencias a lo largo del tiempo.
- Se identificaron tres olas de infecciones por COVID-19, siendo la tercera la de mayor mortalidad.
  ![image](https://github.com/user-attachments/assets/50fcc8f7-3ff1-4848-9728-04180dc1abd8)


## Tasa de Mortalidad y Hospitalización

### Cálculo de las Tasas:
- Se calculó la tasa de mortalidad (`deathIncrease / positiveIncrease`) y la tasa de hospitalización (`hospitalizedIncrease / positiveIncrease`) por estado.

### Estados con las Tasas Más Altas:
- Se identificaron los estados con las tasas de mortalidad más altas, incluyendo Nueva Jersey (NJ), Massachusetts (MA) y Connecticut (CT), tres estados ubicados en el noreste del país, una región densamente poblada.
![image](https://github.com/user-attachments/assets/d0d51970-741e-4c9e-99bb-98d4c0bbde19)

## Análisis de Correlación

### Matriz de Correlación:
- Se calculó la matriz de correlación entre las variables numéricas del conjunto de datos.
- Se revelaron altas correlaciones entre:
    - El total de tests realizados y los casos positivos/negativos.
    - Las muertes y los casos positivos.
    - El incremento diario de casos positivos y hospitalizaciones diarias.
    - 
  ![image](https://github.com/user-attachments/assets/5bfff451-88ea-4823-96ae-f686e8dbabe8)
