# Quicksight??

Herramienta de Business Intelligence de Amazon Web Services (AWS).
Comparada con otras herramientas de BI... tiene claros y oscuros.

## Contras

- Ofrece MUCHA menos funcionalidad que otras herramientas de BI.

## Pros

- Integración con AWS.
- Facilidad de uso.
- (Coste)

# Business Intelligence

Se trata de aportar datos para una toma de decisiones informada con respecto a decisiones de negocio.
Básicamente se trata de aplicar técnicas BÁSICAS de estadística (nivel instituto... poco más) a los datos que tenemos.

El tener datos... no significa que entienda los datos.
    -> 20.000 nóminas. 
La estadística descriptiva nos ayuda a entender los datos... y para eso... lo que haces es ir RESUMIENDO/DESCARTANDO INFORMACIÓN.

## Estadística descriptiva

Variable a variable:
- Montar una tabla de frecuencias -> Representar de forma gráfica
- Resumiendo aún más: ESTADÍSTICOS -> NUMERO

Junte variables:
- Juntaré 2 variables y miraré si tienen relación entre ellas. ESTADÍSTICOS, TABLA DE FRECUENCIAS, GRÁFICO.

Los tipos de datos juegan un papel fundamental... y por desgracia, salvo en muy muy muy contadas apps, los tipos de datos que las apps identifican NO SON NADA RELEVANTES para los estudios que vamos a hacer. Necesitamos identificar los tipos de datos desde el punto de vista ESTADÍSTICO.


### Tipos de datos
Estos son tipos de datos informáticos: Es lo que vamos a ver en Quicksight.
- Enteros
- Strings
- Flotantes
- Booleanos
- Fechas
ME DAN IGUAL !!!!

Lo que vamos a hacer son análisis estadísticos... y para eso los tipos de datos que nos interesan son:
- Cualitativos: No tienen una unidad de medida... y por ello noo puedo bajo ningún concepto hacer operaciones matemáticas con ellos ... al menos operaciones cuyo resultado tenga sentido real.
  - Nominales:       Viene de nombre. 
                     En una escala nominal tenemos nombres... sin relación entre ellos..
                     La única relación es que son excluyentes entre sí.
                     COLOR DE PELO: Castaño, rubio, moreno, pelirrojo.
                                      |        |      |         |
                     COLOR DE PELO:   1        2      3         4
                     Qué nos permite una escala nominal? Que puedo hacer si tengo una variable medida sobre una población a la que aplico una escala nominal? CLASIFICARLOS
                     Los rubios aquí... Los morenos pa'lla
  - Ordinales:       Es un dato NOMINAL.. son nombres... lo que pasa es que entre ellos hay una relación de
                     orden... con respecto a la magnitud de los que sea que están midiendo:
                        ALTOS, MEDIOS, BAJOS 
                    Estas variables me permiten CLASIFICAR A LOS SUJETOS Y TAMBIÉN ORDENARLOS
- Cuantitativos:     Que lo puedo cuantificar... es decir son CANTIDADES... y para que algo sea una cantidad debe tener una UNIDAD DE MEDIDA.... y eso me permite hacer operaciones matemáticas, que tengan sentido real.
  - De intervalo:       NO HAY CERO ABSOLUTO. Es decir, el cero no significa que no haya nada.
                        Ejemplo: Temperatura (Celsius, Fahrenheit). El cero es otro valor más -... como cualquier otro valor.
                        + - 
  - De razón:           Es la que tiene un CERO ABSOLUTO. Es decir, el cero significa que no hay nada.
                        *, - + /
                         1 hijo    = NOMBRE
                         17 hijos
                         23 hijos
                        Los datos cuantitativos puedo CLASIFICARLOS, ORDENARLOS Y HACER OPERACIONES MATEMÁTICAS CON ELLOS.

    NOMINAL < ORDINAL < CUANTITATIVA 

    Siempre puedo bajar el grado con el que estoy midiendo una variable (el nivel de detalle).. pero no puedo subirlo.

DATO: HIJOS QUE TIENE UNA FAMILIA
       
       CUANTITATIVA        ORDINAL         NOMINAL 
        1 hijo              POCOS           TIENE
        0 hijos     >>      NO TIENE  >     NO TIENE
        4 hijos             MUCHOS          TIENE

Lo primero que tengo que hacer antes de comenzar cualquier tipo de estudio sobre unos datos es identificar los tipos de datos que tengo desde un punto de vista ESTADÍSTICO.
Desde un punto de vista informático... DEBE INTENTAR TRANSFORMAR TODO A NÚMEROS (habrá cosas que no tengan sentido: IDENTIFICADORES)

Número del DNI: 23000000T
Desde un punto de vista estadístico... es un dato nominal.
Y desde un punto de vista informático?
    Depende de como lo quiera guardar:
    - Como texto... Y cuánto ocupa ese datos como texto? 
       Cuántos bytes ocupa un carácter en un HDD? o en RAM? Depende del juego de caracteres que usemos.
       ASCII: 1 byte            256 caracteres
       ISO-8859-1: 1 byte       256 caracteres
       UNICODE:
        UTF-8:                  1 byte (normalitos), 2 bytes (griegos), 4 bytes (chinos)
        Pero ... en los DNIS.. solo usamos caracteres simplones. con ASCII o UTF-8... 1 byte me sobra.
        23000000T -> 9 caracteres = 9 bytes
    - Y si guardo el número por un lado y la letra por otro?
       En 1 byte puedo representar cuántos números diferentes? 256 = 2^8... 
       En 2 bytes = 2^16 = 256*256 = 65536
       En 3 bytes = 2^24 = 256*256*256 = 16777216
       En 4 bytes = 2^32 = 256*256*256*256 = 4294967296         ESTE SI!
       Y la letra otro byte... 
       Si guardo número y letra por separado... 4 bytes + 1 byte = 5 bytes
    - La letra del DNI cómo se calcula? Dividiendo el número entre 23 y tomando el resto.
      - RESTO 0 -> T   
      - RESTO 1 -> R
      - ....
      - RESTO 22 -> Z
      Por ende.. puedo calcular la letra desde el número... y no necesito guardarla.
      Y si solo guardo el número me ocupa 4 bytes.

                                x 10.000.000 de datos
      texto: 9 bytes                90M
      número + caracter: 5 bytes    50M
      número: 4 bytes               40M

    Puedo dejar los datos en menos de la mitad.. con una simple operación.
    Menos de la mitad significa:
    - Menos de la mitad de tiempo en leer los datos del HDD
    - Menos de la mitad de tiempo en leer transmitir los datos por la red
    - Menos de la mitad de tiempo en cargar los datos en RAM
    - Menos de la mitad de tiempo en procesar los datos
    Es decir... esta decisión me puede ahorrar una cantidad de tiempo (-> dinero ) aberrante.

    Ahora... con independencia del tipo de datos informático, el tipo de datos estadístico es el que es: NOMINAL.

Y esto sin meternos en el dinero que nos ahorramos en almacenamiento.
Pregunta... el almacenamiento es barato o caro? En producción es lo más caro que hay.
Tenemos la sensación de que es barato...
Quiero guardar unas pelis o fotos en casa.. y no soy tonto y voy al MediaMarkt y me compro un disco duro de 3TB por 50 euros. BARATO !!!! Western blue

En un entorno de prod.. compramos discos que cuestan 5 veces más..
Cuántas copias hago de un dato en un entorno de producción? Al menos 3. <--- REDUNDANCIA : ALTA DISPONIBILIDAD
1Tb en pro... necesito 3 discos de 1Tb ... de los caros.. de los 5x que con un 3x = 15x 
Y ahora backups (RECUPERACION ANTE CATASTROFES) x 3/4 x 2

Para tener 1 Tbs de datos en pro... comparado con casa.. Me va el coste a un 40x de lo que gasto en casa.
50 en casa... 2000 en pro.

### Tipos de datos desde el punto de vista estadístico

- Cualitativos
  - Nominales
  - Ordinales
- Cuantitativos
  - De intervalo
  - De razón

Cuando tengo un conjunto de datos.. que hago?
1º Identifico los tipos de datos que tengo (desde un punto de vista estadístico)
2º Identifico los tipos de datos que tengo (desde un punto de vista informático)
3º Intentar convertir TODO LOS QUE PUEDA a números (si no lo son ya)
4º ANALIZO??? Y qué analizo?

### PASO 1 / ANALISIS 1: TABLA DE FRECUENCIAS

    Frecuencia: Número de veces que algo se repite.

Para hacer una tabla de frecuencias lo que necesito es poder AGRUPAR/CLASIFICAR LOS DATOS.

                    Cuántos hay? (Frecuencia absoluta)
    RUBIOS              4
    MORENOS             3
    PELIRROJOS          2
    CASTAÑOS            1

Sobre qué tipos variables puedo crear una tabla de frecuencias? TODAS
Ahora bien... si la variable tiene muchas MODALIDADES (los valores diferentes que puede tomar una variable) la tabla de frecuencias no me aporta valor.

    NOMINAS         Cuántas hay?
    1323.98             12
    1324.00             1
    1324.01             1
    1324.02             1
    2000.00             1
    2000.01             1
    2218.09             1
    ^^^
    Esta tabla de frecuencias me aporta algo? NO (Me ayuda a entender mejor los datos)
    Qué hacemos? Rebajar el nivel de la variable: CUANTITATIVA -> ORDINAL
    
                   Cuántas hay?    Freq. relativa  | Acumulado relativa | Acumulado absoluta
    0-1000              1000            10%             10%                 1000
    1000-2000           2000            20%             30%                 3000
    2000-3000           6000            60%             90%                 9000 *** 
    +3000               1000            10%             100%               10000
                    ---------
                        10000

       *** Tengo menos de 9000 personas que cobren hasta 3000 euros
       *** Tengo sólo un 10% de la gente que cobra más de 3000 euros

    Pregunta!: Cuándo puedo calcular datos acumulados? Cuando quiera? Cuando puedo ordenar las modalidades por algún concepto.

                   Cuántas hay?    Freq. relativa  | Acumulado relativa | Acumulado absoluta
    RUBIOS              1000            10%             10%                 1000
    MORENOS             2000            20%             30%                 3000
    PELIROJOS           6000            60%             90%                 9000 *** 
    CASTAÑOS            1000            10%             100%               10000
                    ---------
                        10000

        *** ES UN SINSENTIDO

    GRÁFICAS: Puedo representar la tabla de frecuencias : Variables nominales, ordinales
        Diagrama de barras (frec. absoluta | frec. relativa)
        Diagrama de sectores (frec. relativa)
    Esa tabla solo la sacaba para variables con pocas modalidades... 
    Si tengo una variable cuantitativa con muchas modalidades... qué gráfico pinto?
        Histograma
        Caja y bigote (boxplot)

                        BARRAS
    FRECUENCIA
        ^
        |
        |
        |                           X
     123|     X                     X   
        |     X                     X
        |     X          X          X           
        |     X          X          X           X
        +--------------------------------------------- VARIABLE
            RUBIOS    CASTAÑOS    MORENOS    PELIROJOS

                        HISTOGRAMA
    FRECUENCIA
        ^
        |
        |
        |                        X
     123|     X                  X   
        |     X                  X
        |     X       X          X           
        |     X       X          X        X
        +---------------------------------------------> VARIABLE CUANTITATIVA (escala numérica)
          0-1000  1000-2000  2000-3000  +3000  

            SALARIO


### PASO 2 / ANALISIS 2: ESTADISTICOS DESCRIPTIVOS

Reducir a un número (que tenga un sentido) un dato

- Tendencia central: POR DONDE VAN LOS TIROS?
        - Moda       Valor más frecuente
                     Se calcula desde la frecuencia (buscando la más alta).
                     Se puede calcular a cualquier tipo de variable (nominal, ordinal, cuantitativa)
        - Mediana    El valor que divide (o lo intenta)  en dos partes iguales a la población(datos)
                     Se calcula ordenando los datos y buscando el que está en el medio.
                     Se puede calcular a cualquier tipo de variable (ordinal, cuantitativa)
        - Media      Este es complicao! porque no atiende a conceptos humanos... sino matemáticos!
                     El resultado de una fórmula matemática: Sumo todo y divido entre el número de datos. 
                     Se puede calcular a cualquier tipo de variable (cuantitativa)

Para variables:
    -   Nominales: Siempre la moda
    -   Ordinales: Siempre la moda y la mediana
    -   Cuantitativas: Mediana y media
             ¿Cuál me interesa? Depende... depende la distribución (asimetría) de los datos.
             MUCHO CUIDADO CON LA MEDIA... ES UNA MENTIROSA PATOLÓGICA!!!

    Sease villaarriba de arriba: 10 vecinos.... con sus coches... que contaminan. Echan:

            5 g CO / día
            5 g CO / día
            5 g CO / día
            10 g CO / día
            10 g CO / día
            10 g CO / día
            10 g CO / día
            15 g CO / día
            15 g CO / día
            15 g CO / día

            |
            |        X
            |   X    X    X
            |   X    X    X
            |   X    X    X
            +-----------------
                5   10   15


            Media de contaminación en villaarriba de arriba: 10 g CO / día
            Mediana:                                         10 g CO / día

        Cuando tengo una variable simétrica, media y mediana son iguales.
        La media quiere estar con la mediana SIEMPRE... el problema es que los datos extremos tiran de ella.

    Sease villaarriba de abajo: 10 vecinos.... con sus coches...
    Pero... en este pueblo la gente está muy concienciada con el medio ambiente... y compraron todos el mismo coche.

            9x 5 g CO / día
            MANOLO: Tractor fueraborda 1000cv que echa 1000g CO / día

            |
            |   x
            |   X 
            |   X 
            |   X 
            |   X                                                                                   x
            +------------------------------------------------------------------------------------------
                5                           104,5                                                 1000
                ^                                                                               MANOLO
                MEDIANA
                ------------------- MEDIA ---->

            En variables asimétricas... la media y la mediana no son iguales.
            La media siempre querría se igual a la mediana (es una envidiosa)... pero manolo tira de ella.

            Media: 9x5 = 45 + 1000 = 1045 / 10 =                104.5 g CO / día
            Mediana:                                            5 g CO / día

    Si mi pregunta es: En qué pueblo están más sensibilizados con el medio ambiente?
    Y solo miro la media... me voy a equivocar.
          La media es un dato real... de hecho se calcula con una fórmula matemática... 
          Pero a veces... ese número no es REPRESENTATIVO de la realidad/del colectivo.
          La MEDIA está muy influida por los valores extremos.
          Mientras que a la MEDIANA no le afectan nada.
    En estadística decimos que la MEDIA es un indicador NO ROBUSTO... y la MEDIANA es un indicador ROBUSTO.
    Por contra... en estadística también decimos que la MEDIA es un indicador SUFICIENTE ya que tiene en cuenta todos los datos para su cálculo... mientras que la mediana NO.
    A ser posible usaré la media... siempre que sea representativa de la realidad.

    Pero yo no he dicho que vaya a tener en cuenta si hay datos extremos o no... para determinar si usaré la media o la mediana. Lo que vamos a usar para decidir si uso una o la otra es la asimetría:


                                            |
                                            |   x
                                            |   X 
                                            |   X 
                                            |   X 
         x                                  |   X                               x
    +---------------------------------------+---------------------------------------
       -990                                     5                              1000
     GERTRUDIS                  <---MEDIA         ----> MEDIA                  MANOLO
                                                ^
                                              MEDIANA
                                               MEDIA

    Si mis datos siguen una distribución simétrica... caso que haya Manolos... también habrá Gertrudis que los compensarán. Y media y mediana serán iguales (o muy parecidas)... y en ese caso, prefiero usar la media.

    En la práctica... miro el gráfico de reojo... así con los ojos achinaos!
        Calculo media y mediana y si se diferencian mucho-> MEDIANA
        Si se medio parecen -> MEDIA

NUNCA PUEDO DAR UN ESTADISTICO DE TENDENCIA CENTRAL (Media/mediana) Sin dar una medida de dispersión asociada!

    Portal de pisos.
    Portal 1: 4 vecinos
    Quieren comprar unos bancos para sentarse.. 2 bancos... Los hay tamaño pequeño, grande y gigante.
    Cuáles compran?
        170cm 170cm  160cm 180cm
          0     0      100   100     DIFERENCIA EN ABS CON RESPECTO A LA MEDIA
                                    MEDIA DIFERENCIAs: 50
                                    DESVIACION TÍPICA: RAIZ 50 = 7.07
        **MEDIA: 170cm                  (170-7,07)  (170+7,07) = [162.93, 177.07]
        MEDIANA: 170cm
    
    Portal 2: 4 vecinos
        170cm 170cm 170cm 170cm
          0     0     0     0       DIFERENCIA CON RESPECTO A LA MEDIA
                                    MEDIA DIFERENCIAS: 0
                                    DESVIACION TÍPICA: RAIZ 0 = 0
                                    (170-0)  (170+0) = [170, 170]
        MEDIA: 170cm
        MEDIANA: 170cm
    
    Portal 3: 4 vecinos
        160cm 160cm 180cm 180cm 
         100   100   100     100     DIFERENCIA CON RESPECTO A LA MEDIA
                                   MEDIA DIFERENCIAS: 100 cm2
                                      DESVIACION TÍPICA: RAIZ 100 = 10
                                      (170-10)  (170+10) = [160, 180]
        MEDIA: 170cm
        MEDIANA: 170cm
    
    Portal 4: 4 vecinos
        155cm 165cm 175cm 185cm   DIFERENCIA CON RESPECTO A LA MEDIA
         225   25    25     225       MEDIA DIFERENCIAS: 125
                                    DESVIACION TÍPICA: RAIZ 125 = 11.18
                                    (170-11.18)  (170+11.18) = [158.82, 181.18]
        MEDIA: 170cm
        MEDIANA: 170cm

    Portal 5: 4 vecinos
        145cm 145cm 195cm 195cm   DIFERENCIA CON RESPECTO A LA MEDIA
         625   625   625   625     MEDIA DIFERENCIAS al cuadrado: 625 = VARIANZA
                                    DESVIACION TÍPICA: RAIZ 625 = 25
        MEDIA: 170cm
        MEDIANA: 170cm

    Se parecen en algo esos portales (en cuanto a la altura de la gente que vive en ellos) NO?
    Pero si miramos solo la tendencia central! podría llegar a la errada conclusión de que son iguales o muy similares.
    Los seres humanos en seguida en cuanto oímos hablar de tendencia central nos imaginamos que todo el mundo (datos) están en torno a ese valor... y nada que ver!

### Medidas de posicionamiento

Quartiles               Valor de la variable que deja un determinado % de la población por debajo de él.
                        Cuántos quartiles hay? 3
                        Q1 -> Valor que deja por debajo al 25% de la población
                        Q2 -> Valor que deja por debajo al 50% de la población
                        Q3 -> Valor que deja por debajo al 75% de la población
Deciles                 Hay 9
                        Decil 4 -> Valor que deja por debajo al 40% de la población
Percentiles             Valor de la variable que deja un determinado % de la población por debajo de él.
                        Cuántos percentiles hay? 99

De hecho, antes.. sin saberlo ya hemos usado una medida de posición? MEDIANA
    MEDIANA: Valor que deja por debajo al 50% de la población
    MEDIANA = Q2 = P50 = D5

+ Dispersión:        CUANTO CAMBIAN CON RESPECTO AL POR DONDE VAN LOS TIROS?
  - Desviación típica es la raíz de la diferencia al cuadrado con respecto a la media.
    A quién le puedo calcular una desviación típica? Cuantitativa. Y a todas se lo calcularé? Solo si elijo la media como unidad de medida de tendencia central.
    Qué significa? como la interpreto?
        Salario 2000€ de media con una desv. típica de 500€
        La interpretación me la da la regla de Chebychev:
         Si abrimos una desv. típica alrededor de la media, siempre encuentro al menos el 50% de los datos.
         Es decir, que la MAYOR PARTE DE LOS DATOS (al menos 50%) están en un rango de una desviación típica por encima y por debajo de la media.
         Donde están los datos más representativos.
  - Rango SemiIntercuartílico:  (Q3-Q1 /2)
     Lo interpretamos diciendo que si abro un rango semiintercuartílico alrededor de la mediana, ENCUENTRO AL MENOS EL 50% DE LOS DATOS.

    Pero en este caso no trabajamos con la MEDIA... sino con las medidas de posición (MEDIANA, Q1, Q3)

    Si trabajo con la media -> Doy siempre la desviación típica.
    Si trabajo con la mediana -> Doy siempre el rango semi-intercuartílico.

    BOXPLOT

        25%         50%                 25%

              RANGO INTERCUARTILICO (RI)
<------1.5 RI---------><------------><------1.5 RI--------->
           |           +--+---------+                      |        Valor atípico (outlier: MANOLO)
           |           |  |         |                      |        v
           +-----------+  |  o      +----------------------+        0
           |           |  |         |                      |
           |           +--+---------+                      |

           ---------------------------------------------------> VARIABLE
           ^           ^  ^         ^                      ^
           MIN         Q1 Q2        Q3                     MAX
       "razonable"                                     "razonable"

    En este gráfico veo muy rápido:
    - Veo donde se ubica la mayor parte (la más representativa) de la población
    - Veo si la variable tiene una distribución si
    - Veo los MAX, MIN, Q1, Q2, Q3, MEDIA

Los Manolos (Y Gertrudis) son valores atípicos (outliers)
    - Cualquier valor que esté por debajo del Q1 al menos 1.5 veces el rango intercuartílico (Q3-Q1) GERTRU
    - Cualquier valor que esté por encima del Q3 al menos 1.5 veces el rango intercuartílico (Q3-Q1) MANOLO
    - Cualquier valor que esté 2 veces la desv. típica por encima de la media                        MANOLO
    - Cualquier valor que esté 2 veces la desv. típica por debajo de la media                        GERTRU    

Y con esto y un bizcocho... HEMOS ACABADO... o al menos la primera parte!
Estas son las cosas que vamos a hacer cuando queramos analizar UNA VARIABLE. Y no hay más Tomás!!!!
La segunda parte es empezar a juntar variables y ver si tienen relación entre ellas.

# Correlación entre variables (2 a dos)

## NOMINAL x NOMINAL

    SEXO x COLOR DE PELO

    TABLA DE FRECUENCIAS DE DOBLE ENTRADA

                | RUBIO | MORENO | CASTAÑO | PELIRROJO |
    |-----------|-------|--------|---------|-----------|    
    | HOMBRE    |   10  |   20   |   30    |     5     |
    | MUJER     |   20  |   10   |   5     |    10     |
    |-----------|-------|--------|---------|-----------|

    En cada casilla puedo representar: Frecuencia absoluta, frecuencia relativa
    Eso lo puedo pintar?
        GRÁFICO DE BARRAS APILADAS / AGRUPADAS

    Cómo sé si hay relación entre ellas, al ver esa tabla?

                                    SEXO                ( a priori.. lo he analizado previamente)
                       HOMBRES(50%)         MUJERES(50%)
    BUS      100           50                 50              a priori espero encontrar
                           33                 67               realidad..,. lo que cuento cuando entro
    TREN     200           100                100             a priori espero encontrar
                           105                95               realidad..,. lo que cuento cuando entro
    MERCADO  70            35                 35              a priori espero encontrar
                           30                 40               realidad..,. lo que cuento cuando entro
    MEDICO   50            25                 25              a priori espero encontrar
                            1                 49               realidad..,. lo que cuento cuando entro

    Pero es a priori!
    Ahora subo o entro y cuento
    Si los datos que encuentro se parecen a los que esperaba encontrar... entonces concluyo que no hay relación entre las variables.
    El caso del MEDICO me "escama" ... no me cuadra!!!!
    Hay mucha diferencia entre un dato y otro (esperado y el real).
    Hay una gran relación entre el sexo e ir al médico.
    Ahora voy y salgo.. y miro la puerta: GINECOLOGO ! Le encuentro explicación... la estadística no ofrece explicación... SOLO IDENTIFICA PATRONES / RELACIONES / ANOMALÍAS

    El problema es otro....dónde pongo el listón? Dómnde pongo el corte para que no sea SUBJETIVO... sino que siempre aplique el mismo criterio... y de hecho que todos apliquemos el mismo criterio.
    La estadística de nuevo nos ofrece un dato: ESTADISTICO Chi-cuadrado... que no tenemos npi de interpretar... asi que nos quedamos igual: 0-INFINITO
    Ese estadístico lo usamos para calcular otros estadísticos que si podemos interpretar:
    - V de Cramer: 0-1
    - Phi: 0-1
    - Coeficiente de contingencia: 0-1

        0 indica que no hay relación
        1 indica que hay una relación perfecta entre las variables (la máxima posible)
           1 = CAGADA !
           Si 2 variables tienen una relación de 1 significaría que NO TENGO 2 variables... tengo solo una... es la misma variable.
              PESO Kg... PESO g

    En variables nominal x nominal... la relación se da en algunas casillas de la tabla de frecuencias de doble entrada.Me interesa mirar despacio que MODALIDADES (valores) de cada variable son las que presentan relación

## NOMINAL X ORDINAL

Lo mismo que arriba y además:
Y también puedo hacer otra cosita!

Qué puedo medir en una variable ORDINAL? MEDIANA
    Estudio de diferencia de medianas entre los grupos formados por la variable nominal.

    PROVINCIA / NIVEL DE ESTUDIOS

    Nivel de estudios: Primaria, Secundaria, Bachillerato, FP, Universidad, Máster, Doctorado
    PROVINCIA: Madrid, Barcelona
    Podría calcular la mediana de estudios para Madrid:         Master
    Podría calcular la mediana de estudios para Barcelona:      FP

    La gente de Madrid tiende a tener un nivel de estudios más alto que la gente de Barcelona.
    Si las medianas me dan igual... 
    Podría calcular la mediana de estudios para Madrid:         FP
    Podría calcular la mediana de estudios para Barcelona:      FP

    La gente de Madrid tiende a tener un nivel de estudios similar al de la gente de Barcelona.

    No influye donde vives con el nivel de estudios que tienes.
    O al revés.
    No influye el nivel de estudios que tienes con el lugar donde vives.
    O en general: No hay relación entre el lugar donde vives y el nivel de estudios que tienes.

## NOMINAL X CUANTITATIVA

Lo mismo de arriba y además:
Un estudio de diferencias de medias... siempre y cuando la media sea representativa de los grupos.

    SALARIO / EMPRESA de 1000 individuos

               MEDIA salario
    BBVA        4.800 € / mes
    Sabadell    1.200 € / mes
    CaixaBank   2.500 € / mes

    Como las medias son diferentes concluyo que hay una relación entre la empresa y el salario.
    Y eso lo puedo pintar.... y ver visualmente muy guay!

    Si la variable nominal solo puede tomar 2 valores (dicotómica), puedo pintar un 2 histogramas juntos.. unidos por la base: pirámide poblacional.
    Si la nominal no es dicotómica... puedo pintar un boxplot múltiple:
        - Si todas las cajas son iguales        -> NO HAY RELACION
        - Si alguna caja es diferente           -> HAY RELACION

## ORDINAL X ORDINAL

Igual que si tenemos una ordinal x nominal... que hemos contado arriba...
Solo que ahora decido que variable usar como nominal y cuál como ordinal.

## ORDINAL X CUANTITATIVA

Lo tratamos igual que si fuera una nominal x cuantitativa.

## CUANTITATIVA X CUANTITATIVA

No hay tabla que pintar... las tablas de frecuencia ya hemos dicho que si tengo variables cuantitativas... en general son complejas... tienen demasiados valores.

Hay un estadístico: Coeficiente de correlación de Pearson (r) que me dice si hay relación entre las variables.
    -1 < r < 1
    Signo:
        - r < 0 -> Relación inversa (cuando una sube la otra baja)
        - r > 0 -> Relación directa (cuando una sube la otra también sube)
    Valor absoluto:
    0-1
        - r = 0 -> No hay relación entre las variables
        - r = 1 -> Relación perfecta entre las variables (la máxima posible)

GRÁFICO: DISPERSION
    Si los puntos se alinean de alguna forma peculiar... tenemos relación
    Si los puntos aparecen desparramados... no hay relación

Y HASTA AQUÍ! NO HAY MÁS !

# Correlación entre variables (a 3 bandas)

Cuantitativa x Cuantitativa x Nominal:
Gráfico de dispersión... donde las bolitas las pongo de colores... en base a la variable nominal (grupos)

Más de esto... el cerebro no nos da de sí a los humanos... y ya pasamos a delegar a las máquinas: Machine Learning y del Data Mining.

# Correlación entre variables (a 4 bandas)

OLVIDATE.. el cerebro humano ya no da! ----> DATA MINING
No es ya Business Intelligence... es Data Mining.

Para variables harto raras... hay otro tipo de estudios que podemos hacer... pero son cosas ya muy especiales:
- Texto: Nube de palabras (para ver las palabras que más se repiten)

Estas cosas son las que representaremos en los cuadros de mando:
- Tablas de frecuencias de 1 variables
- Gráficos de 1 variable: Barras, sectores, histogramas, boxplot
- Indicadores: Media, mediana, moda, desv. típica, rango semi-intercuartílico, Total, Máximo, Mínimo
- KPI: Indicadores de negocio.... = Indicador estadístico + objetivo de negocio (gráficos de potenciometro, cuentarevoluciones, velocímetros, etc)
- Tablas de frecuencias de 2 variables
- Gráficos de 2 variables: Barras apiladas, agrupadas, pirámide poblacional, boxplot múltiple, dispersión
- Indicadores: Coeficiente de correlación.
- Otras aventurillas: gráfico de nube de palabras...

En los cuadros de mando meteremos también algunos filtros.

---

## Palabrotas en el mundo de los datos.

### Almacenes de datos
- BBDD                      Programas (y los datos que gestionan esos programas) que tenemos en nuestros
                            entornos de producción.
                            Las BBDD de los entornos de producción están pensadas para manejar datos que están vivos... que necesitan de GESTIÓN.
   vvv
   ETL
   vvv
- Datalake                  Almacén de datos (muchas veces usamos los mismos programas de BBDD que para montar
                            las BBDD de producción) históricos que no necesitan de gestión.
                            Guardamos datos en bruto, directamente extraídos de las BBDD de producción.
   vvv
   ETL
   vvv
- Datawarehouse             Almacén de datos estructurados que se utilizan para análisis, reportes, estudio
                            detallado de los datos. Aquí utilizamos modelos de datos muy especiales: Modelos en estrella, copo de nieve. La idea es poder usar esos datos de la forma más sencilla posible para un objetivo concreto.

### Tipo de estudios

- Business Intelligence     Aplicar técnicas de estadística descriptiva básica a los datos. 
                            Estudio de cada variable... o de correlaciones entre variables (2,3,4....).
                            Se hace poco... pero en según que caso se pueden llegar a aplicar técnicas de estadística inferencial.
- Data Mining               Identificar patrones más complejos de relación entre variables.
                            Es una computadora la que va a identificar esos patrones. A mi humano el cerebro no me da. Realmente cuando comenzamos con un proyecto de data mining no sabemos ni lo que buscamos.
- Machine Learning          Pedir a la computadora que haga un programa. Le damos datos.. un algoritmo base...
                            y dejamos a la computadora crear un programa que sea capaz de predecir (clasificar) un resultado.
- Deep Learning             Machine learning basado en redes neuronales profundas.


- Big Data                  La forma en la que trabajamos cuando:
                            - Tenemos un gran volumen de datos
                            - Necesitamos trabajar con datos muy complejos
                            - Necesitamos trabajar con datos que se generan a gran velocidad
                            Y las técnicas tradicionales ya no son útiles.

                            Trabajar?
                            - Almacenamiento de datos
                            - Analítica de datos
                            - Envío de datos

                            Usar en lugar de una gran computadora, una granja de commodity hardware (ordenadores de mierda) trabajando como si fueran una sola computadora.
                            En paralelo necesita de SOFTWARE que permita trabajar en paralelo:
                             - Hadoop , Spark, Hive, Cassandra, MongoDB, etc.

- ETL                       Proceso de Extracción, Transformación y Carga de datos.
                            Se trata de un proceso que se encarga de extraer datos de una o varias fuentes, transformarlos y cargarlos en un destino.
                            BBDDs Producción ---> ETL ---> Datalake

                            Hay muchas variantes:
                            - ETL: Extraigo datos, luego los transformo y finalmente los cargo en el destino.
                            - ELT: Extraigo datos, los cargo en el destino y luego los transformo.
                            - TEL: Proceso de Transformación, Extracción y Carga de datos.
                            - TELT: Proceso de Transformación, Extracción , Carga de datos y Transformación.
                            - TETL: Proceso de Transformación, Extracción, Carga y Transformación de datos.
---

Ejemplo 1: Partidas 2v2 del Clash royale.

4 teléfonos.
Cuando un jugador hace un movimiento, debe notificarse (transmitirse) a los otros 3 jugadores.
Lo que pasa es que un jugador hace un par de movimientos por segundo -> de un jugador deben salir 6 mensajes/segundo.
Pero somos 4 jugando: 24 mensajes/segundo.. en 1 partida.
En un momento dado puede haber + de 50.000 partidas en paralelo: 24 * 50.000 = 1.200.000 mensajes/segundo.
Necesito guardar esos datos?
Qué máquina en el mundo es capaz de procesar 1.200.000 mensajes/segundo? No se ha inventado ese servidor aún.

Ejemplo 2: Tengo un pincho usb de 16gbs... limpito... recién sacado del paquete.
Tengo un archivo de 6 Gbs... lo puedo guardar en el pincho? NPI
Depende del sistema de archivos que tenga el pincho (formateo)
FAT16: No ... son 2Gbs el tamaño máximo de archivo.
Podría optar por NTFS... ext4... otros formatos.. que admiten archivos más grandes...
Y si quiero guardar un archivo de 3Pbs. Qué sistema de archivos uso?

Ejemplo3: Quiero hacer la lista de la compra: PRODUCTO x CANTIDAD
- Bloc de notas
- Excel... A no ser que vaya a guardar más de 200.000 registros... y el Excel se empieza a hacer caquita.
- MYSQL... A no ser que tenga un unos pocos millones de registros... y el MYSQL se empieza a hacer caquita.
- MS SQL Server... A no ser que tenga unas decenas de millones de registros... y el SQL Server se empieza a hacer caquita.
- ORACLE DATABASE... A no ser que tenga unos pocos cientos/miles de millones de registros... y el ORACLE se empieza a hacer caquita.

Y AHORA QUE!?!?!