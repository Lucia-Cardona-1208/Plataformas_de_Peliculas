# Plataformas de Peliculas
## Fuente de datos: Kaggle
https://www.kaggle.com/datasets/ruchi798/movies-on-netflix-prime-video-hulu-and-disney/data
## Presentación: Google Slides
https://docs.google.com/presentation/d/1uyG7JdMYfyQYjEqo6LNL2MP1qP5c0o580WGRrJTFDqo/edit#slide=id.ga7274a1822_0_430
## Descripción:
Para realizar este proyecto se hallaron datos de Netflix, Disney+, Prime Video y Hulu; clasificación de los datos: 
* El título o nombre de la película.
* Año en que la subieron a la plataforma.
* La edad sugerida para ver la película.
* La calificación que le asignó el sitio web estadounidense de revisión y reseñas de cine y tv llamada Rotten Tomatoes.
* La verificación de si la película nombrada está o no en cada plataforma.
  
Luego de tener estos datos se realizó la limpieza de datos necesaria, identificar los valores y sus tipos, eliminar los espacios nulos (vacíos), se verificó que todo estuviera bien y realizar histogramas y gráficos.
Al obtener los datos ya limpios realicé en Power BI el análisis a partir de gráficos para una mejor visualización.

## Documentación del desarrollo deL proyecto
![image text](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d0/Google_Colaboratory_SVG_Logo.svg/2560px-Google_Colaboratory_SVG_Logo.svg.png)
![image](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f8/Python_logo_and_wordmark.svg/1200px-Python_logo_and_wordmark.svg.png)
![image](https://www.trecebits.com/wp-content/uploads/2023/04/google-slides.webp)
![image](https://repository-images.githubusercontent.com/272519458/f865b658-123b-4f18-9e98-eb64e1bb5ff1)
## Queries y scripts de Python:

### Importar librería y lectura de archivo
#importación de Pandas y lectura de archivo
import pandas as pd
csv_path=('https://docs.google.com/spreadsheets/d/e/2PACX-1vQ-ts_lsvOSHcT_XBvoev_kIyV1cotw044BeDn3oehs7WLujetsLsqP9CFBTr_sfrYSWgejyni0S9Rg/pub?gid=299857629&single=true&output=csv')
df = pd.read_csv(csv_path, sep=",")

#Imprimir las primeras cinco filas de un dataframe para probar que todo está bien.
df.head()

### Variables y reemplazar datos
#Ver los tipos de valores de cada columna
df.dtypes

df['Netflix'] = df['Netflix'].astype('string')
df['Hulu'] = df['Hulu'].astype('string')
df['Prime Video'] = df['Prime Video'].astype('string')
df['Disney+'] = df['Disney+'].astype('string')
df.dtypes

#Remplazar "0" por "no" y "1" por "si" en las columnas "Netflix" "Hulu" "Prime Video" "Disney+"
df['Netflix'] = df['Netflix'].replace({"0":"No", "1":"Si"})
df['Hulu'] = df['Hulu'].replace({"0":"No", "1":"Si"})
df['Prime Video'] = df['Prime Video'].replace({"0":"No", "1":"Si"})
df['Disney+'] = df['Disney+'].replace({"0":"No", "1":"Si"})

#Cambiar títulos a las columnas
df.columns= ['Enumeración','ID','Título_Película', 'Año', 'Edad', 'Calificación(tomatómetro)', 'Netflix', 'Hulu', 'Prime_Video', 'Disney+', 'Type']

#Imprimir las primeras cinco filas de un dataframe para probar que todo está bien.
df.head()

### Eliminar columnas y datos nulos
#Eliminar columnas
df=df.drop('Enumeración',axis=1)
df=df.drop('ID',axis=1)
df=df.drop('Type',axis=1)

#Nos ayuda para ver los nombres de las columnas.
df.columns

#Imprimir las primeras cinco filas de un dataframe para probar que todo está bien.
df.head()

#Con este eliminamos las filas con datos nulos.
df=df.dropna(axis=0)

#Imprimir las primeras cinco filas de un dataframe para probar que todo está bien.
df.head()

#Para visualizar todos los datos.
df

### Histogramas y diagramas
#Importando las bibliotecas necesarias para visualización de datos y análisis exploratorio

import matplotlib.pyplot as plt  # Biblioteca para crear gráficos y visualizaciones estáticas, animadas e interactivas en Python

import seaborn as sns  # Biblioteca para crear gráficos estadísticos atractivos e informativos en Python


#Utilizando Seaborn para crear un diagrama de distribución (histograma y KDE) para la columna 'Año' del DataFrame df

sns.distplot(df['Año'])

#Creando un histograma para la columna 'Año' del DataFrame df
#figsize=(6,6) especifica las dimensiones del gráfico en pulgadas

df['Año'].hist(figsize=(6,6))

#Mostrando el gráfico en pantalla

plt.show()

#Creando una figura con dimensiones específicas (10x10 pulgadas)
fig=plt.figure(figsize=(20,50))
#Creando un diagrama de caja (boxplot) para comparar la distribución de los precios entre los diferentes estilos de carrocería
sns.boxplot(x="Edad", y="Año", data=df)
#Mostrando el gráfico en pantalla
plt.show()

### Descargar el archivo csv
df.to_csv('Plataformas_Peliculas.csv')

from google.colab import files
files.download('Plataformas_Peliculas.csv')
