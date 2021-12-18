# NLP-IMDb


## Introducción

El proyecto tiene como finalidad desarrollar un modelo de **procesamiento de lenguaje natural (NLP)** que permita utilizar los algoritmos de aprendizaje automático sobre, en este caso, 50 mil críticas provenientes de Internet Movie Database IMDb. A partir de ello, creamos un predictor que permita distinguir críticas positivas y negativas.

La iniciativa para la elección de esta temática fue haber realizado, previamente, nuestro proyecto de Data Analytics sobre un dataset de Kaggle de la misma industria; es por esto que nos propusimos continuar con la misma temática y hacer un análisis integral sobre la industria cinematográfica y recomendaciones de IMDb. Ergo, planteamos como objetivos de nuestro proyecto final lograr un mayor entendimiento de lo que compete el modelo NLP en Python, para poner en práctica estos conocimientos en futuros análisis; y que el modelo desarrollado para el dataset de IMDb permita que, al ingresar una nueva crítica, automáticamente el código pueda discernir qué valor (positivo o negativo) tendrá la misma.

## Objetivos del Proyecto

Podemos resumir los **objetivos del presente** **trabajo** de la siguiente manera:


1) Aprender todo aquello que esté relacionado con el procesamiento del lenguaje natural (NLP) tanto en terminos teóricos (conceptos asosciados, teorías que fueron desarrollando esta disciplina, entre otros) como en términos practicos con las librerías e hiperparámetros asociados al mismo.
2) Aprender sobre la manipulación y limpieza del dataset obtenido en pos de hacer un modelo mas eficiente y robusto, para ello utilizaremos todas las herramientas aprendidas a lo largo del curso que sean útiles para la obtención del resultado buscado.
3) Desarrollar y buscar un modelo que provea los mejores resultados a la hora de clasificar la review de una película, buscando la manera de que dicho modelo pueda ser usado por un usuario de manera facil e intuitiva.


## Preguntas de Investigación

Como mencionamos anteriormente, en el presente trabajo se utilizará un dataset de IMDb que contiene 50000 reviews de diferentes películas y, para cada una de ellas, una clasificación que puede ser 0 (review negativa) o 1 (review positiva) basada en la puntuación que el usuario finalmente le otorgó a la película. Al encontrarnos ante este dataset y combinarlo con los objetivos planteado, nos surjen necesariamente una serie de preguntas que buscaremos responder a lo largo del trabajo para que dichos objetivos puedan ser cumplidos. De esta manera, las **preguntas de investigación** que surgen son:

- ¿Cuantas criticas negativas y positivas tiene el dataset? ¿Es un dataset equilibrado? en caso de que no ¿Qué técnica sería mejor utilizar para compensar este desbalanceo?
- En las review,¿Cuales son las palabras que mas se repiten? ¿Son coherentes con el tipo de industria sobre la que estamos trabajando? ¿Hay elementos que no sean palabras y pueda perjudicar al modelo? en caso de que si ¿Qué podemos hacer para corregirlo?
- Una vez que contemos con las review de manera correcta, ¿Cómo transformamos estas reviwew en un formato que sea asimilable por un modelo? ¿Qué modelos supervisados de clasificación existen y cual usamos? 
- Por último, ¿Cómo funciona el modelo? ¿Qué métricas podemos usar para medir los resultados del mismo? ¿Clasifica bien una nueva review que le enviamos?

A través de las diferentes lineas de código se iran respondiendo estas preguntas que servirán de guia para definir los pasos a seguir a lo largo de todo el proyecto.

## Pasos del proyecto

<br>

El proyecto se realizará integramente en una notebook con código Python, a modo de guía, los **pasos que se seguirán** serán los siguiente: 

1) Lectura del dataset de IMDb.
2) Exploración y Limpieza de datos: 
        a) Análisis de variable a predecir.
        b) Analisis de reviews con Nube de Palabras.
        c) Eliminación de marcadores HTML, emoticones irrelevantes.
        d) Obtención de palabras raíz mediante el algoritmo de Porter.
        e) Utilización de stopwords para eliminar palabras vacías.
3) Creación y entrenamiento del modelo: 5a) Método LogisticRegression y 5b) Método RandomForestClassifier.
4) Evaluación del modelo.
5) Creación de Interfaz Gráfica para ingresar nuevas críticas y visualizar si las mismas corresponden a valoracioens positivas o negativas.

<br>

## Librerías utilizadas

A su vez, las **librerías** a utilizar seran:
1) pandas: librería para trabajar con datos tabulares en Python, se basa en numpy y permite realizar una gran cantidad de operaciones.
2) wordcloud: librería que facilita la creación de nube de palabras, muy importante a los efectos del presente proyecto.
3) matplotlib y seaborn: librerias de visualización de datos que facilitan la comprensión de la información mostrandola graficamente.
4) re: libreria para utilizar expresiones regulares de forma de manipular texto y realizar la limpieza del mismo.
5) nltk: librería muy utilizada en el NLP ya que ofrece métodos para trabajar con texto como eliminar palabras frecuentes y las raices de las palabras.
6) sklearn: librería que cuenta con diferentes algoritmos de machine learning para el desarrollo de modelos.
7) tkinter: librería que nos permite crear interfaces gráficas que ejecuten el código de manera mas amigable para el usuario.


## Desarrollo de pasos realizados en la Notebook

En este apartado buscaremos explicar paso a paso la notebook del proyecto final, de manera que se logré entender la lógica seguida y las lineas de código ejecutadas. Para eso iremos viendo cada una de las etapas descriptas previamente. 

1) Lectura del dataset de IMDb.

En este paso lo primero que se realizó fue la importación de la librería Pandas que, como se mencionó previamente, permite trabajar con datos tabulares y ofrece métodos muy utiles para la manipulación de tablas por lo que será de mucha utilidad a lo largo de todo el proyecto. 

En segundo lugar se crea una variable llamada **df** que almacenara nuestro dataset, para eso se hace una lectura con el método de Pandas llamada **read_csv** al cual le indicamos el nombre que tiene el archivo en nuestra computadora. Además, a modo preventivo, le pasamos como parametro **encodigo="utf-8"** para unificar los diferentes formatos particulares creados en zonas distintas ya que, si bien las reviews estan en inglés, puede tener caracteres que distintas zonas, de esta manera no nos estaremos perdiendo de ninguno.

2) Exploración y Limpieza de datos

En esta etapa se busca realizar una exploración para comprender el dataset con el que estamos trabajando, ver sus particularidades y en base a eso hacer la limpieza correspondiente para que quedé optimizado de cara al futuro.

A los efectos de responder la primera pregunta de investigación planteada previamente, lo primero que realizamos fue un breve analisis de la varible a predecir, para ver si estamos en presencia de una dataset balanceado o desbalanceado y, en función de ello, si debíamos realizar algun tratamiento adicional. Para ello utilizamos la librería **seaborn** para graficar a traves de su método **countplot** ,que recibe la columna y el dataset como parámetro,la variable a predecir y obtuvimos un dataset totalmente balanceado (25000 review positivas y 25000 negativas). Esta información nos dió la certeza de que no se requeriran tecnicas como oversampling y subsampling para corregir un desbalanceo. En esta intancia nuevamente se utilizó Pandas.

Lo siguiente que se realizó fue una **nube de palabras** para poder ver a simple vista cuales son las palabras que mas se repiten en el total de las reviews y si tienen sentido con la industría con la que estamos trabajando. Para realizar esta nube de palabras necesitamos de la librería especialmente creada para eso llamada **wordcloud** con sus métodos WordCloud, STOPWORDS, ImageColorGenerator (tal vez finalmente no se usen todos pero para asegurarnos los importams desde un principio) y **matplotlib**. Una vez importadas las librerías instanciamos 



