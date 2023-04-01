# PRECIO DIAMANTES

Se nos da un dataframe (train.csv) con precios de diamantes y las variables:

- id: only for test & sample submission files, id for prediction sample identification
- price: price in USD
- carat: weight of the diamond
- cut: quality of the cut (Fair, Good, Very Good, Premium, Ideal)
- color: diamond colour
- clarity: a measurement of how clear the diamond is
- x: length in mm
- y: width in mm
- z: depth in mm
- depth: total depth percentage = z / mean(x, y) = 2 * z / (x + y) (43--79)
- table: width of top of diamond relative to widest point (43--95)

Queremos crear un modelo que nos prediga los precios.

## ESTRUCTURA CARPETAS

He creado una carpeta por cada modelo creado. Dentro de cada carpeta tenemos Datos que contiene todos los csv que tendremos que usar y los archivos pickle que iremos llamando.

Así mismo tenemos un archivo por cada fase del modelo: 
- Eda
- Preprocesamiento
- Entrenamiento
- Predicción

## EDA

Hacemos una visualización de los datos:
![datos](/imagenes/datos_head.jpg)

Hacemos que la variable id sea el index.

Vamos a empezar a estudiar el dataframe. Visualizamos el tipo de datos.
![info](/imagenes/info.jpg)

No tenemos nulos y vemos que las variables "cut", "color" y "clarity" son categ´ricas mientras el resto son numéricas.

En "describe" nos interesa fijarnos en la media y el 50% para ver la dispersión. Si hubiera mucha diferencia veríamos que tenemos muchos outliers. 

![describe](/imagenes/describe.jpg)

En este caso los valores son bastante parecidos.

![duplicados](/imagenes/duplicados.jpg)

Tenemos 85 duplicados. Nos creamos un dataframe con ellos para ver sus valores
![df_duplicados](/imagenes/df_duplicados.jpg)


Lo siguiente que haremos es visualizar la relación que tiene la variable respuesta con el resto de variables numéricas:

![scaterplot](/imagenes/scaterplot.jpg)

Vemos que con carat y x guarda una relación positva bastante marcada, pero para asegurarnos vamos a hacer un heatmap:

![heatmap](/imagenes/heatmap.jpg)

Carat, x, y, z son las variables con mayor relación.

Vamos a ver las variables categóricas:

![boxplot_categoricas](/imagenes/boxplot_categoricas.jpg)

En este gráfico parece que mantienen un orden. Vamos a ver la media de precio por variable para ver si es cierto o no:

![barplot](/imagenes/barplot.jpg)

En este gráfico vemos que no guardan un orden muy claro.

Vamos a ver los outliers que tenemos:
![outliers](/imagenes/outliers.jpg)

Vemos que hay valores 0 en x, y, z lo cual es imposible, dado que representan medidas de los diamates.Los eliminamos de nuestro dataframe y pasamos al preprocesamiento.

## PREPROCESAMIENTO

Las variables "depth" y "table" no tienen casi relaciones con la variable respuesta, por lo que vamos a eliminarlas.

Para la estandarización usamos Standard Scaler y para el encoding de todas las columnas usaremos One Hot Encoder.

## ENTRENAMIENTO

Separamos los datos del dataframe en train y test y utilizamos el Decision Tree Regressor para hacer el ajuste de los datos. Sacamos los parametros máximos del modelo y hacemos las predicciones sobre los dos set de datos, train y test. 

Ajustamos los parámetros y hacemos un Gradient Boosting Regressor que nos da las siguientes métricas:



![metricas](/imagenes/metricas.jpg)

### COMPARACIÓN OTROS MODELOS:



![dt2](/imagenes/dt2.jpg)
![dt1](/imagenes/dt1.jpg)
![dt3](/imagenes/dt3.jpg)
![gb](/imagenes/gb.jpg)




