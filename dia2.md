
# BI

Aplicar técnicas estadísticas básicas para la toma de decisiones en una empresa.

OJO A LOS TIPOS DE DATOS:
- Tipos de datos, desde el punto de vista informático:
    - Numérico
    - Texto
    - Fecha
    - Booleano
  Y esto tiene impacto en Consumo de memoria, almacenamiento, velocidad de procesamiento, etc.
- Tipos de datos, desde el punto de vista de la estadística:
    - Cualitativo
        - Nominal               CLASIFICAR LOS DATOS
        - Ordinal               CLASIFICAR Y ORDENAR LOS DATOS   
    - Cuantitativo              CLASIFICAR, ORDENAR Y HACER OPERACIONES MATEMÁTICAS
        - De intervalo                                                  Sumas/restas 
        - De razón (si hay cero absoluto)                               Sumas/restas/multiplicaciones/divisiones

Esto es lo primero que debemos identificar en un conjunto de datos.

# Analizar los datos

## Analizar variable a variable
 
- Tabla de frecuencias (frecuencias absolutas y relativas. Ambas acumuladas) -> Gráfico de barras/sectores
  Las reservamos solo a variables cualitativos y cuantitativos con pocas modalidades. 

  VARIABLE 1: Número de hijos de una entidad familiar: 0,1,2,3,4,5,6,8,10 -> Esto si lo puedo representar en una tabla de frecuencias.
  VARIABLE 2: Salario anual de una persona: 0,1000.01,1030.89... Infinitos valores diferentes. No puedo representarlo en una tabla de frecuencias.

  Si tengo una variable cuantitativa como la segunda, qué puedo hacer? Rebajar el nivel de la variable  -> Convertirla en Ordinal (agrupar en intervalos)

    Para las variables cuantitativas, además tenemos otros 2 gráficos:
    - Histograma 
    - Boxplot (diagrama de caja y bigotes)

- Estadísticos:
  - Tendencia central (media, mediana, moda)                                        POR DONDE VAN LOS TIROS

                          MODA         MEDIANA      MEDIA
         Nominal            √
         Ordinal            √            √
         Cuantitativas      (√)          √            √   (Usaremos una u otra en función de la simetría de los datos)
                                         ^            ^
                                     ASIMETRICA    SIMETRICA
                                     En la media influyen los Manolos y Gertrudis

  - Dispersión (varianza, desviación típica, rango, coeficiente de variación)       CUANTO CAMBIAN LOS DATOS CON RESPECTO AL POR DONDE
                                                                                    VAN LOS TIROS
    Puede haber distintos conjuntos de datos que produzcan la misma medida de tendencia central... Para diferenciarlos OBLIGATORIAMENTE debo dar una medida de dispersión.

        MEDIANA ->          Rango semi-intercuartílico (Q3-Q1)/2
                                Si abrimos un rango de un rango semi-intercuartílico alrededor de la mediana, tenemos al menos el 50% de los datos

        MEDIA ->            Desv. típica
                                Si abrimos un rango de una desv. típica alrededor de la media, tenemos al menos el 50% de los datos
Y se acabó!

## Analizar variables 2 a dos:

- NOMINAL x NOMINAL

  Tabla de frecuencias de doble entrada. -> Gráfico de barras agrupadas/apiladas
    - Chi cuadrado para ver si hay relación... más bien algunos estadísticos basados en chi cuadrado:
      - Cramér's V          0-1: 0=no relación, 1=relación perfecta
      - Phi
      - Contingencia

- NOMINAL x ORDINAL

  De entrada lo mismo de arriba.
  Estudio de diferencia de medianas
    Calculamos la mediana de cada grupo (grupos establecidos en base a los valores de la variable cualitativa) y comparamos entre si a ver si hay diferencia. Si hay diferencia es que hay relación entre las variables.

    NIVEL DE INGRESOS MEDIANO en CADIZ es igual al de MADRID? 
    Si: La provincia no influye en el nivel de ingresos
    No: La provincia influye en el nivel de ingresos

- NOMINAL x CUANTITATIVO
  
  De entrada lo mismo de arriba.
  Adicionalmente siempre y cuando la media sea representativa:
    Estudio de diferencia de medias
    Calculamos la media de cada grupo (grupos establecidos en base a los valores de la variable cualitativa) y comparamos entre si a ver si hay diferencia. Si hay diferencia es que hay relación entre las variables.

- ORDINAL x ORDINAL

  Hacemos lo mismo que su fueran 2 nominales.
  (hay cosas más avanzadas, como la R de Spearman, pero no es necesario)

- ORDINAL x CUANTITATIVO

  Básicamente como si fuera NOMINAL x CUANTITATIVO

- CUANTITATIVO x CUANTITATIVO

  Diagrama de dispersión (scatter plot)
    - Correlación de Pearson (r) -> [-1,-1]
    - Si miro el signo: 
        - Positivo: Cuando una variable aumenta, la otra también
        - Negativo: Cuando una variable aumenta, la otra disminuye
    - Si miro el valor absoluto:
        - 0: No hay relación
        - 1: Relación perfecta

Luego hay cosas más raras... para tipos de datos más especiales:
- Nube de palabras
- Mapas de calor

El problema es que si tengo un conjunto de datos de 50 variables... 50 tomadas de 2 en 2... 50*49/2 = 1225 estudios de correlación.
ESTO ES UNA LOCURA... no acabo.
Ahí es donde entra el ojo experto de negocio! Discrimina las relaciones principales.
    Color de los ojos con el salario de una persona? NO DEBERÍA !

Cuidado que a veces nos encontramos con sorpresas... en un sentido y en otro.
La estadística muestra relaciones... pero a veces son fruto de la casualidad.... o de otras cosas...

ALTURA DE UNA PERSONA y CONOCIMIENTOS DE MATEMÁTICAS. GUARDAN RELACION! NO... y lo sabemos que no...
OJO... si miro un conjunto de individuos entre 5 y 18 años... Hay relación entre esas variables? GIGANTE
Los altos van a saber mucho más de matemáticas que los bajos. Hay una variable MEDIADORA que es la edad.
Ambas guardan relación con la edad... y a través de esa variable presentan una relación entre si... Pero no es una relación real.
Es lo que llamamos una relación espuria.


----

# Proyecto: BI sobre ventas de videojuegos:

Nombre              CUALITATIVA(NOMINAL) -> IDENTIFICADOR!
Plataforma          CUALITATIVA(NOMINAL)
Año                 CUANTITATIVA(Ud. de medida? año)
                    Intervalo o razón? Intervalo (no hay cero absoluto)
Genero              CUALITATIVA(NOMINAL)
Editorial           CUALITATIVA(NOMINAL)
Ventas NA           CUANTITATIVA(Ud. de medida? millones de unidades)
Ventas EU           CUANTITATIVA(Ud. de medida? millones de unidades)
Ventas JP           CUANTITATIVA(Ud. de medida? millones de unidades)
Ventas Otros        CUANTITATIVA(Ud. de medida? millones de unidades)
Ventas Global       CUANTITATIVA(Ud. de medida? millones de unidades)

OJO con las columnas VENTAS... qué son realmente? FRECUENCIAS !!!!!

Tenemos un conjunto de datos con algo más de 16.000 datos... básicamente una linea por juego/plataforma.
Este conjunto es un RESUMEN de otro conjunto de datos más grande.
De hecho, lo que tenemos delante es una tabla de frecuencias de un conjunto de datos más grande.
El conjunto de datos en bruto sería:

JUEGO               PLATAFORMA  AÑO     GENERO              EDITORIAL   FECHA VENTA
Super Mario Bros    NES         1985  Plataformas           Nintendo    1985-09-13
Super Mario Bros    NES         1985  Plataformas           Nintendo    1985-09-13
Super Mario Bros    NES         1985  Plataformas           Nintendo    1985-09-13
Super Mario Bros    NES         1985  Plataformas           Nintendo    1985-09-13
Super Mario Bros    NES         1985  Plataformas           Nintendo    1985-09-13
Super Mario Bros    NES         1985  Plataformas           Nintendo    1985-09-14
Super Mario Bros    NES         1985  Plataformas           Nintendo    1985-09-14
Super Mario Bros    NES         1985  Plataformas           Nintendo    1985-09-14
Super Mario Bros    NES         1985  Plataformas           Nintendo    1985-09-14
Super Mario Bros    NES         1985  Plataformas           Nintendo    1985-09-14
Super Mario Bros    NES         1985  Plataformas           Nintendo    1986-09-14
... y así 1 millón de filas... Y las hemos consolidado en una... añadiendo la columna de ventas,
que no es sino el número de filas que había en el conjunto de datos en bruto.
Hemos contado cuantas ventas de un juego había en el conjunto de datos en bruto y lo hemos puesto en la tabla de frecuencias.
---

Ya conozco los tipos de datos que tengo... por dónde sigo?

Lo primero, vamos a entender en detalle cada dato que tengo... hacemos un análisis de cada variable por separado.

Nombre              NUBE DE PALABRAS... para ver que palabras se repiten más.
                    Extraer palabras de los nombres de los juegos...
                    Y buscar correlaciones entre esas palabras y las ventas.
                    A ver si hay palabras que por estar en el nombre del juego, hacen que se vendan más o menos.
Plataforma          TABLA DE FRECUENCIAS
                    Gráfico de barras
                    Gráfico de sectores ***
                    ¿A QUÉ PREGUNTA RESPONDE ESTA TABLA DE FRECUENCIAS?
                    Cuántos juegos hay por plataforma
                    
                    TABLA DE FRECUENCIAS 2  -  Cuántos ventas tiene una plataforma
                    Para esta tabla he de multiplicar cada fila por la columna de ventas global.
                    Cada dato o computa como 1, sino computa como "ventas globales".

    PLATAFORMA  VENTAS GLOBAL
    DS	        0,03
    DS	        0,06

    La tabla 1: 
        PLataforma    FRECUENCIA (Cuántos juegos hay por plataforma)
        DS            2

        La representaríamos en sectores

    La tabla 2:
        PLataforma    FRECUENCIA (Cuántos ventas tiene una plataforma)
        DS            0,09

        La representaríamos en barras   SI LO QUE ME INTERESA ES CONOCER LA CIFRA DE VENTAS
        O en sectores                   SI LO QUE ME INTERESA ES COMPARAR EN QUE PLATAFORMA SE VENDE 
                                        MAS QUE EN OTRA

Año                 TABLA DE FRECUENCIAS? CLARO.. tenemos pocos años
                    Gráfico? HISTOGRAMA!
                    
                    Si cada fila la sumamos 1 vez... a qué pregunta responde la tabla?
                    - Cuántos juegos hay por año
                    Si cada fila la multiplicamos por ventas globales... a qué pregunta responde la tabla?
                    - Cuántas ventas hay por año
                    
                    Si tuviera fecha de venta:
                    - Mirar si a principio de mes se vende más que a finales de mes
                    - Mirar si a principio de año se vende más que a finales de año 
                    - Mirar si alrededor de ciertas fechas se venden más juegos (navidades...)  
                  
                    Pero esa información la perdimos al agrupar por año.

Genero              TABLA DE FRECUENCIAS (2)
                    TABLA 1: Contando cada fila como 1: Cuantos juegos hay por genero
                    TABLA 2: Contando cada fila como ventas globales: Cuantas ventas hay por genero
                        Las representaría con barras o sectores
Editorial           TABLA DE FRECUENCIAS (2)
                    TABLA 1: Contando cada fila como 1: Cuantos juegos hay por editorial
                    TABLA 2: Contando cada fila como ventas globales: Cuantas ventas hay por editorial
                        Las representaría con barras o sectores

OJO EN TODAS LAS TABLAS 1 anteriores... Necesitamos consolidar previamente las plataformas... y quitarlas de en medio.

Ventas NA           
Ventas EU           
Ventas JP           
Ventas Otros        
Ventas Global       
                    Puedo saber cuántas ventas puedo esperar para un juego (si quito la información de la plataforma de en medio).
                    Y saber que los juegos pueden tener ventas entre  (MIN, MAX) 
                    Y que de media se venden 0,5 millones de unidades de un juego.
                    O de mediana... dependiendo de la simetría de los datos.

Una cosa que nos interesa por ahora de analizar esta variable es entender la forma de los datos.
Si es simétrica o asimétrica. Ya que esto condicionará el uso de la media o la mediana... no para este estudio... sino para el resto de los estudios que vamos a hacer (cuando empecemos a cruzar variables).


Quizás hay plataformas con muy pocas ventas... o editoriales con muy pocas ventas... o géneros con muy pocas ventas... y son datos que para otros estudios eliminaré.

Puedo sacar una estadística de pocos datos? NO es representativa.

---

Llega el momento de comenzar a combinar variables:

PLATAFORMA  AÑO     GENERO              EDITORIAL

PLATAFORMA x AÑO
   Pregunta a la que respondo?
      (Si no tengo en cuenta ventas)    Número de juegos que se han publicado por plataforma y año
      (Si tengo en cuenta ventas)       Número de ventas que se han realizado por plataforma y año
PLATAFORMA x GENERO
      (Si no tengo en cuenta ventas)    Número de juegos que se han publicado por plataforma y género
      (Si tengo en cuenta ventas)       Número de ventas que se han realizado por plataforma y género
PLATAFORMA x EDITORIAL
    (Si no tengo en cuenta ventas)    Número de juegos que se han publicado por plataforma y editorial
    (Si tengo en cuenta ventas)       Número de ventas que se han realizado por plataforma y editorial
AÑO x GENERO
    (Si no tengo en cuenta ventas)    Número de juegos que se han publicado por año y género
                                        ^^ OJO AQUÍ... hay que consolida juegos/plataforma
    (Si tengo en cuenta ventas)       Número de ventas que se han realizado por año y género
AÑO x EDITORIAL
    (Si no tengo en cuenta ventas)    Número de juegos que se han publicado por año y editorial
                                        ^^ OJO AQUÍ... hay que consolida juegos/plataforma
    (Si tengo en cuenta ventas)       Número de ventas que se han realizado por año y editorial
GENERO x EDITORIAL
    (Si no tengo en cuenta ventas)    Número de juegos que se han publicado por género y editorial
                                        ^^ OJO AQUÍ... hay que consolida juegos/plataforma
    (Si tengo en cuenta ventas)       Número de ventas que se han realizado por género y editorial

En que me pueden ayudar esas respuestas en la toma de decisiones para mi negocio?
Si por ejemplo soy un desarrollador de videojuegos?
- PLATAFORMA x AÑO: Ver si hay una tendencia en la publicación de juegos para una determinada plataforma. Si los tiempos van cambiando hacia una determinada plataforma u otra (cada año o pocos años van saliendo nuevas consolas al mercado... y se dejan de vender juegos para las más antiguas... o no!) y resulta que durante 3/4 años se siguen vendiendo juegos para una plataforma aunque haya salido una nueva al mercado... eso me da una pista de que quizás no tengo que dejar de desarrollar para esa plataforma.
- PLATAFORMA x GENERO: Ver qué géneros se venden más en unas plataformas u otras... Si voy a montar un juego de un determinado genero, me tendré que enfocar más en unas plataformas que en otras.
- AÑO x GENERO: Ver si hay un cambio de tendencia en los géneros de videojuegos que se venden a lo largo del tiempo.
- GENERO x EDITORIAL: Ver si más o menos todo el mundo que desarrolla videojuegos del mismo género vende más o menos lo mismo... o si hay editoriales que lo petan en un determinado género y otras que no.... para aprender de ellas, que es lo que están haciendo bien.

En este escenario... cuál va a ser la principal VARIABLE a la que no tengo que perder de vista?
Cuando hagamos el estudio, esas combinaciones de variables que hemos estudiado, presentará relación entre si o no? EN TODAS QUE SI !

Y serán verdad esas relaciones que se nos identifiquen... o algunas de ellas serán espurias? (o tendrán parte de espuria)
LA VARIABLE CLAVE VA A SER EL AÑO.
Cada año hay unas plataformas.
Cada año aparecen nuevas empresas creadores y otras que dejan de serlo.
El tiempo pasa... y afecta a todo.
El simple paso del tiempo va a hacer que todo el resto de variables presenten relaciones.
Lo interesante será identificar si además del factor tiempo, hay otros factores que influyen en la relación entre las variables.
Ver si esas relaciones que se presentan (identifiquen) se deben solo al paso del tiempo o no.

Podremos combinarlas de 3 en 3:

PLATAFORMA x AÑO x GENERO

FRECUENCIA
^
|
|   III
|   OOO
|   XXX
|   XXX
+-----------------------------------------------> AÑO
    PS      PS2     DS

Para ver evoluciones en el tiempo, nos interesará trabajar con datos relativos!

 PLATAFORMAS


PLATAFORMA x AÑO x EDITORIAL
PLATAFORMA x GENERO x EDITORIAL
AÑO x GENERO x EDITORIAL

Incluso 4 variables.
PLATAFORMA x AÑO x GENERO x EDITORIAL


Ya no hay más estudios.
En todas ellas podré incluir como factor multiplicativo la columna de ventas (globales o por región).
En base a la pregunta a la que quiera responder.

                Genero
                  ^
       TEMPORAL< JUEGOS > Plataformas
                  v
                Editoriales

Por qué tenemos los datos codificados? 
- Desde el punto de vista estadístico qué aporta? NADA !
- Desde un punto de vista informático:
  -  Velocidad de procesamiento
  -  Consumo de memoria
  -  Almacenamiento

Siempre que tenemos un conjunto de datos, vamos a tratar de convertir a números todo lo que podamos.
NOMBRE? No... no estudiamos este campo... es un identificador.

---

Qué tipo de fichero tenemos? xlsx, csv, txt, json, xml
Parquet?

En el mundo de los datos (análisis, almacenamiento) no nos gustan NADA los ficheros de arriba.
Nos encanta parquet.
Parquet es un formato BINARIO... mientras que json, csv... son formatos de texto.

[
    { 'nombre': 'Mario', 'edad': 30, 'altura': 1.80 },
    { 'nombre': 'Luigi', 'edad': 35, 'altura': 1.85 },
    { 'nombre': 'Peach', 'edad': 28, 'altura': 1.70 }
]

Cuánto ocupa cada valor de edad en HDD? 2 bytes (2 caracteres)
Cuánto ocupa cada valor de altura en HDD? 4 bytes (4 caracteres)
Si lo guardo como numero? Lo podría guardar cada uno como 1 byte. Acabo de quitar 5 bytes por fila.
En cuántas filas repito la palabra 'nombre'? En todas... y edad? y altura? Vaya desparrame.

PARQUET
schema:{'nombre': 'string', 'edad': 'byte', 'altura': 'byte'}
METADATOS: {En qué byte empieza cada columna}
data: [
    [ 'Mario', 'Luigi', 'Peach' ],
    [ 30, 35, 28 ],
    [ 180, 185, 170 ]
]
Solo que una diferencia más... parquet es binario. es decir, para el número 170... no guarda en disco:
- un byte con el carácter '1'
- otro byte con el carácter '7'
- otro byte con el carácter '0'
Solo guarda el número 170 como byte... en binario: 10101010

Imaginad que quiero sacar una estadística del tipo: Pinta un histograma de la columna edad... pinta un gráfico de dispersión entre edad y altura... saca la media de la columna edad... saca la mediana de la columna altura... etc.

Si tengo un fichero JSON(CSV... y el resto de los de arriba), que datos tengo que leer de disco? TODO EL ARCHIVO... e irlo parseando.
Y si es parquet? Solo tengo que leer la columna que me interesa.

Parquet lo usamos para análisis de datos y para almacenamiento.
Para transmisión no tanto... usamos más AVRO, que es otro formato binario, pero orientado a filas.

AVRO:
schema:{'nombre': 'string', 'edad': 'byte', 'altura': 'byte'}
data: [
    [ 'Mario', 30, 180 ],
    [ 'Luigi', 35, 185 ],
    [ 'Peach', 28, 170 ]
]

Mi BBDD de producción, será la que sea... Me refiero... tendrá la estructura que tenga.
De ahí sacaré datos a un datalake. Puedo elegir aquí (y es habitual) guardarlos en parquet.

Las herramientas de BI leen datos de un DATAWAREHOUSE.
Necesito llevar los datos de un datalake a un datawarehouse (ETL).
En el datawarehouse, puedo tener también los datos en parquet... pero no es lo habitual.
Lo habitual es que los datos estén en un formato de BBDD relacional (PostgreSQL, MySQL, Oracle, SQL Server, etc.)

Si tengo 4 datos... todo vale. da igual.
Cuando tengo muchos datos... y quiero montar cuadros de mando en tiempo real... con filtro interactivos... Olvídate de excels... incluso de parquets.

SPICE es el motor de análisis de datos de AWS, que incorpora su propios sistema de almacenamiento de información.
Si traigo datos de una BBDD relacional, puedo optar en QuickSight por:
- Importar los datos a SPICE... e irlos refrescando cada X tiempo.
- O bien, dejar los datos en la BBDD relacional y que SPICE haga las consultas directamente a la BBDD sin cache de por medio.

Lo importante es entender que este tipo de herramientas : QuickSight, Tableau, Power BI... no son herramientas para transformar datos.
Son herramientas para analizar datos.
A estas herramientas les tienen que llegar los datos ya transformados y organizados de forma que puedan ser analizados mucho más rápido.

En el mundo BI, solemos usar mucho los modelos de datos en estrella o copo de nieve.

Una tabla de dimensión temporal en un modelo en estrella, que columnas suele tener?
- ID: Numérico
- Fecha : (1 a 1 con ID)
- Año
- Mes
- Día
- Año/mes
- En qué cae el día (Lunes o jueves)
- Si cae en finde
- Si es festivo

En una BBDD de producción tendríamos algo como esto? Ni de broma!

Todo este trabajo, es trabajo previo. Cuando los datos llegan a la herramienta de BI, llegan niquelados... para hacer estudios.
Puede ser que el analista precise de datos adicionales...(transformados o calculados de los anteriores). Y está bien.
Y estas herramientas si le permiten hacer eso. Pero la estructura de datos de alto nivel, ya está hecha.