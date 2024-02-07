![Steam](https://github.com/Rafaelandresmg/Proyecto-Individual-N-1-Machine-Learning-Operations-Mlop-/blob/main/Assets/Proyecto%20png%201.png) 
<br />
# Proyecto MLOps: Sistema de Recomendación de Videojuegos para Usuarios de Steam

### Descripción del Proyecto
El presente proyecto personifica una fase trascendental de LABS en el bootcamp de Henry, donde se orienta en la práctica de  soft skills y habilidades técnicas necesarias en el mercado laboral. Fue proporcionado un caso de negocio existente utilizando un Dataset público de la industria de videojuegos, específicamente de la plataforma en línea STEAM.

### Objetivo
La finalidad de este proyecto es generar el primer modelo de Machine Learning (end to end) que de solucion a un problema de negocio en Steam, a través de un enfoque que abarca asignaciones de Data Engineering (ETL, EDA, API) hasta la puesta en marcha del Modelo. es importante indicar que se busca un rápido desarrollo y tener un Producto Mínimo Viable (MVP).<br />
<br />

## Etapas del Proyecto <br />
![Etapas](https://github.com/Rafaelandresmg/Proyecto-Individual-N-1-Machine-Learning-Operations-Mlop-/blob/main/Assets/Proyecto%20png%202.png) 
<br />
**1. Ingeniería de Datos (ETL y API)** <br />

- **1.1 *Transformaciones de Datos:*** Inicialmente, Se entregaron  tres (3) archivos en formato JSON, los cuales están almacenados en el siguiente repositorio público en **[Google Drive](https://drive.google.com/drive/folders/1HqBG2-sUkz_R3h1dZU5F2uAzpRn7BSpj).** Se ejecutaron las transformaciones necesarias para  la carga de los conjuntos de datos con el formato adecuado. Dichas transformaciones se realizaron con el propósito de mejorar  el rendimiento de la API y el entrenamiento del modelo, a continuacion se describiran los archivos recibidos.  <br />
  + [australian_user_reviews.json]: Contiene las reseñas de juegos  realizadas por usuarios. Se hace referencia al notebook [ETL_user_reviews](Notebooks/ETL_user_reviews.ipynb) para observar con detalle el procesamiento de las reseñas, con el cual se genero un nuevo archivo con datos tratados, [user_reviews_cleaned.csv](Datasets/Archivos_Limpios/user_reviews_cleaned.csv).<br />
  + [output_steam_games.json] : Proporciona información sobre los juegos disponibles en la plataforma Steam. Incluye datos sobre los géneros, etiquetas, especificaciones, desarrolladores, año de lanzamiento, precio y otras caracteristicas destacadas de cada juego. En el notebook [ETL_steam_game](Notebooks/ETL_steam_game.ipynb) se puede revisar el proceso de limpieza y transformación de datos, el cual culmina con el cual se genero un nuevo archivo llamado [steam_games_cleaned.csv](Datasets/Archivos_Limpios/steam_games_cleaned.csv). <br /> 
  + [australian_users_items.json]: El archivo australian_users_items.json contiene información sobre los ítems relacionados con usuarios australianos. Este conjunto de datos ha pasado por un proceso de Extracción, Transformación y Carga (ETL), que se detalla en el notebook [ETL_user_items](Notebooks/ETL_user_items.ipynb). Como resultado de este proceso, se generó un nuevo archivo [user_items_cleaned.csv](Datasets/Archivos_Limpios/user_items_cleaned.csv) con el fin de permitir su manipulación y análisis, proporcionando una estructura más afable para su integración en el modelo.<br />
  
- **1.2 *Feature Engineering:*** Se creo la columna **``` sentiment_analysis ```**  con el fin de realizar un análisis de sentimiento a las reseñas de los usuarios. Se utilizo la biblioteca NLTK (Natural Language Toolkit) con el analizador de sentimientos de Vader, que nos proporciona una puntuación compuesta que puede ser utilizada para clasificar la polaridad de las reseñas en negativas (valor '0'), neutrales (valor '1') o positivas (valor '2'). A las reseñas escritas ausentes, se les asignó el valor de '1'. Para observar el desarrollo en el notebook [ETL_user_reviews](Notebooks/ETL_user_reviews.ipynb) y para profundizar un poco más en el análisis en podemos visualizar el [EDA_Análisis Exploratorio de Datos](Notebooks/EDA_AnálisisExploratorioDatos.ipynb). <br />

- **1.3 *Desarrollo de API:*** Implementé una API con FastAPI y se deployó en Render, ésta proporciona cinco (5) consultas sobre información de videojuegos. Puede ver el detalle del código en los notebooks [Funciones](Notebooks/Funciones.ipynb) y [Consultas](Notebooks/Consultas.ipynb).<br />
  + Endpoint 1 (Developer): Devuelve Cantidad de items y porcentaje de contenido Free por año según empresa desarrolladora.<br />
  + Endpoint 2 (UserData): Devuelve cantidad de dinero gastado por el usuario, el porcentaje de recomendación en base a reviews.recommend y cantidad de items.<br />
  + Endpoint 3 (UserForGenre): Devuelve el usuario que acumula más horas jugadas para el género dado y una lista de la acumulación de horas jugadas por año de lanzamiento.<br />
  + Endpoint 4 (Best_Developer_year): Devuelve el top 3 de desarrolladores con juegos MÁS recomendados por usuarios para el año dado. (reviews.recommend = True y comentarios positivos)<br />
  + Endpoint 5 (Developer_reviews_analysis): Según la empresa desarrolladora, se devuelve un diccionario con el nombre de la desarrolladora como llave y una lista con la cantidad total de registros de reseñas de usuarios que se encuentren categorizados con un análisis de sentimiento como valor.<br />
Para acceder a la funcionalidad completa de la API y explorar las recomendaciones de juegos, puedes visitar este enlace [URL de la API](). En este sitio, encontrarás las diversas funciones desarrolladas. ¡Disfruta explorando!.
  
**2. Análisis Exploratorio de Datos (EDA)** <br />
El fin del Analisis Exploratorio de los Datos es indagar en las relaciones entre variables, la identificacion de outliers y l la busqueda de patrones interesantes en los datos. El notebook [EDA_Análisis Exploratorio de Datos](NoteBooks\EDA_JSON.ipynb)<br />

**3. Modelo de Aprendizaje Automático** <br />
EL Modelo de Aprendizaje Automatico requerido es un sistema de recomendación con uno de los criterios solicitados:
- **3.1 *[Sistema de Recomendación ítem-ítem](NoteBooks\PLN_y_ML.ipynb)***: Se desarrolo un modelo de recomiendaciones de juegos similares en base a un juego inicial, utilizando similitud del coseno. Con CountVectorizer se convirtieron los textos de la columna 'specs' en vectores numéricos para posterior calcular la similitud del coseno.<br />
Se utilizó la métrica de **similitud del coseno**, ya que mide el coseno del ángulo entre dos vectores. Cuanto más cercano a 1, más similares son los vectores. Este método fue clave para determinar qué tan parecidos son los juegos entre sí. Esto se utiliza para generar recomendaciones, ya que los juegos con vectores similares son considerados como recomendaciones potenciales.<br />

**4. Implementación de MLOps** <br />
**Deploy del Modelo:** Desplegué el modelo de recomendación como parte de la API, la cual puedes consultar acá: **[URL de la API](https://proyecto-individual-nro-1-machine.onrender.com/docs)**. <br />

**5. Video Explicativo** <br />
Grabé un video explicativo que muestra el funcionamiento de la API, consultas realizadas y una breve explicación de los modelos de ML utilizados [Youtube]([https://www.youtube.com/watch?v=P4vFLH5vnMA](https://www.youtube.com/watch?v=2u4_NdXinjE)).<br />
<br />

## Estructura del Repositorio <br />
**1. [/Notebooks](Notebooks/):** Incluye los Jupyter Notebooks con el Código completo y bien comentado donde se realizaron las extracciones, transformaciones y carga de datos (ETL), análisis exploratorio de los datos (EDA), y el archivo con Diccionario de datos, MVP, Pautas del proyecto[Varios](Notebooks/Varios.ipynb).<br />

**2. [/Datasets](Datasets/):** Incluye los datasets utilizados en una versión tratada y procesada de dichos archivos. Las fuentes de datos iniciales se encuentra almacenadas en la carpeta input en el siguiente repositorio [Google Drive](https://drive.google.com/drive/folders/1HqBG2-sUkz_R3h1dZU5F2uAzpRn7BSpj)<br />
- **3.1 *Archivos_API:*** Contiene los datasets en formato csv consumidos por la API.<br />
- **3.2 *Archivos_Limpios:*** Contiene los archivos depurados después de haber realizado el ETL.<br />
- **3.2 *Archivos_ML:*** Contiene los archivos consumidos por la API para hacer el sistema de recomendación.<br />

**3. [/assets](assets/):** Carpeta con imágenes y recursos utilizados en el desarrollo del proyecto.<br />

**4. [/Video](Video/):** Contiene el video explicativo del proyecto, el cual se encuentra publicado en [Youtube](https://www.youtube.com/watch?v=t3N0ePA_D34&t=1s).<br />
<br />

## Ejecutar la API (en su máquina local) <br />
1. Clonar el repositorio <br />
```
https://github.com/Rafaelandresmg/Proyecto-Individual-N-1-Machine-Learning-Operations-Mlop-
```
2. Crear entorno virtual<br />
```
python3 -m venv <nombre_del_entonto>
```
3. Vaya al directorio del entorno virtual y actívelo<br />
- 3.1. Para Windows:
```
Scripts/activate
```
- 3.2. Para Linux/Mac:
```
bin/activate
```
4. Instalar los requerimientos<br />
```
pip install -r requirements.txt
```
5. Ejecute la API con uvicorn<br />
```
uvicorn main:app --reload
```

## Autor <br />
#### Rafael Miranda. <br />
Para cualquier duda/sugerencia/recomendación/mejora respecto al proyecto con toda libertad puedes contactarme por []()<br />
