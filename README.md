# Data Mining en Series Temporales
🇪🇸

| Universidad | Politécnica de Madrid (UPM) |
| --- | --- |
| Autoras | Laura García Perrín y  Xiya Sun | 
| Grado   | Ciencia de Datos e IA           |


## Introducción y Objetivos
Este repositorio contiene un proyecto final que implementa y analiza técnicas de _Data Mining_ en Series Temporales.
El **objetivo principal** es llevar a cabo un análisis temporal de tendencias climáticas para apreciar cómo cambian las 
temperaturas, la humedad, la velocidad del viento y otros parámetros a lo largo del tiempo para un cierto _dataset_. 
Formas de lograr el objetivo principal son a través de métodos estadísticos, métodos gráficos y métodos de aprendizaje 
automático.

Otros propósitos que se pueden derivar de este análisis u objetivo principal son:

* **Predicción del clima**: El análisis temporal se puede utilizar para predecir el clima futuro. Esto puede ser útil para
  el pronóstico del tiempo, la planificación de desastres y la gestión de recursos. 

* **Identificación de eventos climáticos extremos**: Esto puede ayudar a comprender mejor estos fenómenos y a desarrollar
  medidas de mitigación en caso de que resultase de interés.

* **Identificar patrones en la temperatura global**: El análisis temporal se puede utilizar para identificar patrones en
  la temperatura global, por ejemplo.

## Conjunto de Datos

El conjunto de datos con el que se trabaja se obtiene de Kaggle a través del siguiente enlace:

* https://www.kaggle.com/datasets/muthuj7/weather-dataset/data

En concreto, los datos elegidos pertenecen al dominio del clima. Son registros del tiempo atmosférico de una ciudad a lo largo de 
10 años, desde 1 de enero de 2006 al 31 de diciembre de 2016. Este conjunto de datos es estructurado y consta de 96453 instancias o filas 
y de 12 variables o columnas, tal y como se muestran en la siguiente tabla:

| Característica                 | Tipo de Datos            | Descripción                                |
|--------------------------------|--------------------------|--------------------------------------------|
| Formatted Date                 | datetime64[ns, UTC]      | Fecha y hora en formato UTC                |
| Summary                        | object                   | Resumen del clima para el día              |
| Precip Type                    | object                   | Tipo de precipitación                      |
| Temperature (C)                | float64                  | Temperatura en Cº                          |
| Apparent Temperature (C)       | float64                  | Temperatura aparente en Cº                 |
| Humidity                       | float64                  | Humedad relativa en porcentaje             |
| Wind Speed (km/h)              | float64                  | Velocidad del viento en km/h               |
| Wind Bearing (degrees)         | float64                  | Dirección del viento en grados             |
| Visibility (km)                | float64                  | Visibilidad en km                          |
| Loud Cover                     | float64                  | Cobertura de nubes                         |
| Pressure (millibars)           | float64                  | Presión atmosférica en milibares           |
| Daily Summary                  | object                   | Resumen del clima para el día              |

_Nota_. A destacar que aquellas las series temporales que recopilan información atmosférica presentan la peculiaridad de ser estacionarias, 
motivo por el cual se espera que en aplicaciones de predicción o _forecasting_ los resultados obtenidos sean bastante buenos y precisos.

## Metodología

Se van a utilizar distintos enfoques de _Data Mining_ en el conjunto de datos descrito con anterioridad, de tal forma que se 
satisfagan los objetivos planteados para el proyecto de la asignatura. Previamente, será necesario llevar a cabo un tratamiento
del conjunto de datos en aras de aumentar su calidad y utilidad para los enfoques que se plantean a continuación en la siguiente
tabla:

| Técnica               | Objetivo                                  | Descripción                                                                 |
|-----------------------|-------------------------------------------|-----------------------------------------------------------------------------|
| KMeans                | Análisis de conjunto de datos             | Agrupar datos en k-clusters para identificar patrones y obtener información.|
| (S)ARIMA              | Lanzamiento de predicciones               | Modelo estadístico para pronosticar series temporales.                      |
| Random Forest Regressor | Lanzamiento de predicciones             | Método de aprendizaje en conjunto para regresión que utiliza múltiples árboles de decisión.|
| CNNs                  | Clasificación de series temporales        | Redes neuronales convolucionales para el análisis y clasificación de series temporales. |

## Método de Evaluación

Una vez implementadas las distintas técnicas de _Data Mining_, se procederá a evaluarlas en función de ciertas métricas. De esta forma se 
pretende alcanzar una forma tangible de poder medir su alcance y de analizar las limitaciones de cada enfoque. Para cada técnica de _Data Mining_
se implementa un método Python.

| Método                | Modelo Usado             | Métricas de Evaluación                                                             | Visualización          | Observaciones                                                                 |
|-----------------------|--------------------------|------------------------------------------------------------------------------------|------------------------|--------------------------------------------------------------------------------|
| `eval_clust`          | KMeans                   | Silhouette Score, Inertia, Davies-Bouldin Index, Calinski-Harabasz Index           | No aplicable           | Evalúa calidad del agrupamiento mediante distintas métricas de cohesión y separación entre clústeres. |
| `calculate_accuracy`  | (S)ARIMA                 | MAE, MSE, RMSE, MAPE                                                               | No aplicable           | Mide la precisión de las predicciones para series temporales.                                             |
| `eval_model`          | Random Forest Regressor  | MAE, MSE, RMSE, MAPE, R-squared                                                    | Gráfica de dispersión  | Compara los valores verdaderos con las predicciones y proporciona métricas de regresión.                 |
| `eval_cnn`            | CNNs                     | Matriz de confusión, Informe de clasificación (precision, recall, F1-score, etc.) | No especificado        | Sugerido para evaluar la clasificación de series temporales mediante CNNs.                               |

## Apéndice: Tiempo de Ejecución (segundos) para cada Método Implementado

| Método                             | Tiempo de Ejecución (segundos)    |
|------------------------------------|-----------------------------------|
| `impute_precip_type_na_as_snow`    | 5.153655290603638                 |
| `preprocess_weather_data`          | 6.1320366859436035                |
| `preprocess_data`                  | 0.0000455379486083944             |
| `find_optimal_clusters`            | 28.561754941940308                |
| `apply_kmeans`                     | 9.563373565673828                 |
| `visualize_clusters`               | 12.803064584732056                |
| `eval_clust`                       | 126.71682500839233                |
| `plot_acf_pacf`                    | 5.634672403335571                 |
| `plot_seasonal_decompose`          | 1.1513631343841553                |
| `fit_sarima`                       | 131.5040798187256                 |
| `train_sarima`                     | 97.52052307128906                 |
| `forecast_sarima`                  | 1.5710036754608154                |
| `calculate_accuracy`               | 0.6643753051757812                |
| `categorizar` (primera invocación) | 0.22289395332336426               |
| `categorizar` (segunda invocación) | 0.08489227294921875               |
| `prepare_rf`                       | 42.450777530670166                |
| `visualizar_pred`                  | 10.665130376815796                |
| `crear_series_temporales`          | 0.131911039352417                 |
| `recurrence_plot` (primera invocación) | 0.22237372398376465           |
| `recurrence_plot` (segunda invocación) | 0.28394293785095215           |
| `plot_recurrence_plots`            | 4.226735830307007                 |
| `recurrence_plot` (tercera invocación) | 0.32770562171936035           |
| `recurrence_plot` (cuarta invocación) | 0.35254359245300293           |
| `prepare_training_data`            | 22.50136160850525                 |
| `preparar_datos`                   | 0.002007007598876953              |
| `build_model`                      | 1.4650955200195312                |
| `train_and_evaluar_model`          | 11.480260133743286                |







