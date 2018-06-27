# Informe TP2

Para empezar a familiarizarme con el sistema de entrega, voy a primero intentar generar un resultado válido, aunque sea completamente inventado
Mi idea es luego hacer un LSH con las descripciones de los anuncios.

Tue 26 Jun 2018 07:55:54 PM -03
- Voy a usar un random forest. para ello tengo que pasar muchas variables a categóricas
Tue 26 Jun 2018 10:42:47 PM -03
- Resulta que si le disminuyo mucho los datos de entrenamiento, sigue dando el mismo resultado. Creo que tengo un overfitting horrible.
Tue 26 Jun 2018 11:15:29 PM -03
- Voy a intentar hacer un submit ahora con lo que tengo, y luego seguir intentando un random forest con mejor trato de variables categoricas.
Tue 26 Jun 2018 11:28:27 PM -03
- El randomforest necesita ser bastante profundo para andar bien, sospecho que esto significa que va a overfittear feo
Wed 27 Jun 2018 12:10:59 AM -03
- gano `{'max_features': 0.75, 'min_samples_leaf': 7, 'n_estimators': 30}` `max_features = [0.1,0.25,0.5,0.75] min_samples_leaf= [1,3,5,7] n_estimators = [1,5,10,30]`, dividiendo el set de datos en 50% entrenamiento y 50% test
- Como los que ganaron son los del borde, voy a hacer otro intento:
    -gano `{'max_features': 0.75, 'min_samples_leaf': 12, 'n_estimators': 10}`, de `max_features = [0.5,0.75] min_samples_leaf= [4,7,12,19] n_estimators = [10,30,50]`, con un score de 0.879. Es una paja no haber guardado con que score gano el otro.
Wed 27 Jun 2018 01:04:32 AM -03
- Hipótesis: testear con pocos datos es una buena forma de saber si el modelo overfittea, esto se ve en que un grid search devuelve parametros diametralmente opuestos.
Wed 27 Jun 2018 01:29:48 AM -03
- Quizas convenga tambien convertir la educacion a variable categorica
Wed 27 Jun 2018 12:37:00 PM -03
- La matriz bien entrenada logro un puntaje de  `0.8735881282835573`  con parametros  `{'max_features': 0.5, 'min_samples_leaf': 19, 'n_estimators': 50}`
La matriz poco entrenada logro un puntaje de  `0.8733397771032063`  con parametros  `{'max_features': 0.75, 'min_samples_leaf': 19, 'n_estimators': 50}`
Wed 27 Jun 2018 04:42:18 PM -03
- El rendimiento disminuyó significativamente y no puedo encontrar por qué, los parámetros de recién nunca pasaban de 0.8
- Voy a intentar
Wed 27 Jun 2018 05:06:42 PM -03
- Con solo las columnas: `['idpostulante', 'sexo', 'edad', 'nivel_educativo', 'anuncios_vistos', 'idaviso', 'nombre_zona', 'tipo_de_trabajo', 'nivel_laboral','sepostulo', 'es_entrenamiento']`, el rendimiento bajó a un horrible 0.56
- Logré un mejor 0.74 con agregando `['nombre_area','denominacion_empresa']`
Wed 27 Jun 2018 05:35:31 PM -03
- Parece que la denominacion de empresa aporta bastante. Voy a probar volver a poner todas las denominaciones (recientemente habia sacado todas las 'injunables')
    - [ x ] Logre 0.78 incluyendo todas las empresas.
    - [ x ] Logre el mismo 0.78 incluyendo todas las categorias.

# TODO informe
- [  ] Rehacer gráficos
    - [ x ] Nivel educativo
    - [ x ] Zonas de trabajo
- [  ] Hacer nuevos graficos
    - [  ] Denominacion empresa y densidad de anuncios
    - [  ] Diagrama de venn de quien vio que anuncio, y quien se postulo a que anuncio
- [  ] Hablar de random forest
    - [  ] Grid search
    - [  ] Performance sacando variables categóricas
