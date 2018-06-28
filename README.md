# Informe TP2 Organización de Datos.

Juan Pablo Capurro. 1C2018.

## Continuación de la exploración sobre los datos de entrenamiento

En la corrección se hizo notar algunas deficiencias en los gráficos, por ejemplo el de nivel educativo
Ahora el nivel educativo es, dado un postulante, cual es el titulo 'mas alto' que llegó a completar:

![alt text](https://i.imgur.com/1UNHAW3.png)

También vale la pena revisar cuántos anuncios visitan en promedio los usuarios de distintos niveles educativos:

![alt text](https://i.imgur.com/zGbQ92s.png)

Asimismo, también corresponde actualizar el gráfico que muestra la distribución de anuncios por zona:

![alt text](https://i.imgur.com/rgbWJYY.png)

Se puede ver que la cantidad de zonas en las que hay anuncios aumentó

### Relacion entre anuncios y postulantes

Puede observarse que hay pocos anuncios y postulantes que no tengan relación con el otro grupo, ya sea mediante postulaciones:

![alt text](https://i.imgur.com/yrA56vO.png)

O mediante vistas:

![alt text](https://i.imgur.com/8w3ePwB.png)

## Exploración sobre los datos de predicción
Vistas en los datos a predecir:

![](https://i.imgur.com/Yt3TdoX.png)

En este caso hay más anuncios aislados que en el set de entrenamiento.

Una cosa que despierta mi curiosidad es qué tan significativa es la muestra que hay que clasificar, respecto a todos los anuncios/vistas/postulantes:

En un tema similar: puedo asumir que todas las postulaciones que voy a predecir fueron vistas?

![](https://i.imgur.com/LNpF1jG.png)

No, no puedo.

Un problema con el que me topé fue que al procesar los datos para formar la predicción, aproximadamente el 40% de los postulantes faltaban.
Esto se solucionó al usar también los archivos de genero y edad de postulantes del set de entrenamiento

## Approach random forest

Al armar un set de entrenamiento mergeando los anuncios y los postulantes por el archivo de vistas, le di al modelo el bias de que ya todas las postulaciones eran a anuncios que ya habian sido vistos.
Si puedo mantener esta asunción, debería obtener una mejoría en rendimiento marcando como 'no se postuló' todos los anuncios que no fueron vistos, y luego usar el modelo de random forest para el resto.

![](https://i.imgur.com/Oy8yabL.png)

Parece que solo el 66% de los anuncios que tienen postulaciones fueron vistos previamente
Voy a probar generar un set de entrenamiento con proporciones parecidas

A falta de un criterio en base al cual agregar anuncios por fuera de los vistos, pruebo otros approaches:

### Variación de hiperparámetros
Usé grid search para buscar hiperparámetros, y obtuve resultados variados, pero en todos los casos sigue sin superar el bias descripto en el comienzo de la sección
Por ejemplo, logré mejorar una predicción de 0.82 a 0.879 usando los hiperparámetros: `{'max_features': 0.75, 'min_samples_leaf': 12, 'n_estimators': 10}`

Con los parámetros por defecto, logré mejor performance a medida que más variables categóricas ordenadas eran reemplazadas por sus códigos ordenados.
Por ejemplo, aportó mejoras ordenar los trabajos de menos a más fijo, con 'full time' con el código máximo o las denominaciones de empresa con códigos ascendentes según qué tantos anuncios tenía la misma.


