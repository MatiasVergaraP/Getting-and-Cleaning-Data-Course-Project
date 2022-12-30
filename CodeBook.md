# Code Book

El script ```run_analysis.R``` realiza la preparación de los datos siguiendo las directrices descritas en la definición del proyecto del curso.

## 1. Descargar el set de datos

El set de datos es descargado y se extrae en la carpeta de nombre ```UCI HAR Dataset```

## 2. Asignar los datos a variables

- ```features <- features.txt``` (561 obs. of 2 variables)

  Las características seleccionadas para esta base de datos proceden de las señales brutas de 3 ejes del acelerómetro y el giroscopio tAcc-XYZ y tGyro-XYZ
  
- ```activities <- activity_labels.txt``` (6 obs. of 2 variables)

  Lista de actividades realizadas cuando se tomaron las mediciones correspondientes y sus etiquetas.
  
- ```subject_test <- subject_test.txt``` (2947 obs. of 2 variables)

  Contiene datos de prueba de 9/30 sujetos voluntarios en observación.
  
- ```x_test <- X_test.txt``` (2947 obs. of 561 variables)
  
  Contiene datos de prueba de características grabadas
  
- ```y_test <- y_test.txt``` (2947 obs. of 1 variable)

  Contiene datos de prueba de las etiquetas de código de las actividades.
  
- ```subject_train <- subject_train.txt``` (7352 obs. of 1 variable)

  Contiene datos de entrenamiento de 21/30 sujetos voluntarios observados.
  
- ```x_train <- X_train.txt``` (7352 obs. of 561 variables)

  Contiene características grabadas de entrenamiento.
  
- ```y_train <- y_train.txt``` (7352 obs. of 1 variable)

  Contiene los datos de entrenamiento de las etiquetas de los códigos de las actividades.
  
## 3. Fusionar los conjuntos de entrenamiento y prueba para crear un conjunto de datos

- ```X ```(10299 obs. of 561 variables) es creada fusionando ```x_train``` y ```x_test``` usando la función ```rbind()```.
- ```Y ```(10299 obs. of 1 variable) es crada fusionando ```y_train``` y ```y_test``` usando la función ```rbind()```.
- ```Subject``` (10299 obs. of 1 variable) es creada fusionando ```subject_train``` y ```subject_test``` usando la función ```rbind()```.
- ```Merged_data``` (10299 obs. of 563 variables) es creada fusionando ```Subject```, ```Y``` y ```X ```usando la función ```cbind()```.

## 4. Extraer solo las medidas del promedio y desviación estándar para cada medida

- ```TidyData ```(10299 obs. of 88 variables) es creada seleccionando las columnas ```subject```, ```code``` y las medidas del promedio (```mean```) y la desviación estándar (```std```) de ```Merged_Data```.

## 5. Usar nombres descriptivos para las actividades en el set de datos

- Números enteros de la columna ```code``` de ```TidyData``` se reemplaza con la correspondiente actividad tomada de la segunda columna de la variable ```activities```.

## 6. Etiquetar adecuadamente el conjunto de datos con nombres descriptivos de las variables

- La columna ```code``` en ```TidyData``` es renombrada en ```activities```.
- Todos los nombres ```Acc``` se reemplazan por ```Accelerometer```.
- Todos los nombres ```Gyro``` se reemplazan por ```Gyroscope```.
- Todos los nombres ```BodyBody``` se reemplazan por ```Body```.
- Todos los nombres ```Mag``` se reemplazan por ```Magnitude```.
- Los nombres de las columnas que empiezan con ```f``` se reemplazan por ```Frequency```.
- Los nombres de las columnas que empiezan con ```t``` se reemplazan por ```Time```.

## 7. Del set de datos en el paso 4, crear un segundo conjunto de datos independiente y ordenado con la media de cada variable para cada actividad y cada sujeto

- ```FinalData``` (180 obs. of 88 variables) se crea resumiendo ```TidyData``` tomando los promedios de cada variable para cada actividad y cada sujeto, una vez agrupados por sujeto y actividad.
- Se exporta ```FinalData``` en el archivo ```FinalData.txt```.


  