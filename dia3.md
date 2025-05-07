# Cuál es la peor operación que le puedo pedir a un ordenador?

Ordenar datos.

# Distinct

Qué tal se llevan las BBDD con el distinct? MALAMENTE
Un distinct, lo primero que hace es ORDENAR LOS DATOS... después los procesa secuencialmente comparando cada dato (fila) con la anterior... si son iguales elimina la actual (duplicada)

# Qué otras operaciones con datos acaban haciendo un order by (y por tanto debemos limitar mucho su uso?)

- order by
- distinct
- group by
- having
- join
- union = union all + distinct
    union all [GUAY(sin problema)]

Una cosa importante. Hemos dicho que cuando llevamos los datos a una herramienta de BI, los debemos llevar muy muy muy preprocesados.
En el caso de Quicksight, al traer datos tenemos 2 opciones:
- Tirar de la BBDD
- Importar los datos a su motor de procesamiento SPICE

Las BBDD que tal se llevan con las ordenaciones? FATAL!
Y es por eso que en las BBDD existe el concepto de índice.

# INDICE

Por qué un índice nos ayuda a ejecutar consultas más rápido? a identificar datos más rápido? a hacer una búsqueda más rápido?

Cuál es la forma más básica de hacer una consulta? Quiero buscar tal juego... por su nombre?   FULLSCAN!
SELECT * FROM JUEGOS WHERE NOMBRE = 'Federico';

FULLSCAN es ir mirando dato a dato, del primero al último, hasta que encuentre el dato que busca.
Si tengo 1000000 de juegos... potencialmente tendré que hacer 1000000 de comparaciones.
Si la tabla tiene configurado ese campo como UNIQUE... en cuanto se encuentra el primer juego que coincide, se para la búsqueda.

El tener los datos preordenados me serviría para poder hacer la búsqueda más rápida?
Si los datos están preordenados, podemos aplicar otro algoritmo de búsqueda: BÚSQUEDA BINARIA!
Cada vez que hemos buscado una palabra en el DICCIONARIO, lo que hemos hecho ha sido una búsqueda binaria.

Cuando busco ZAPATO en un diccionario no abro por la mitad... mi cerebro ya sabe por donde cae más o menos zapata en el diccionario.
Yo se que la z está al final. También sé que de la z cuántas palabras hay? pocas si lo comparo por ejemplo con la A, E, M, que tienen muchas.

Las BBDD tampoco son imbéciles... y cuando buscan algo.. tampoco abren por la mitad... Las BBDD poco a poco van entendiendo la "distribución" de los datos. Generando ESTADISTICAS!

Todo esto está muy bien:
 1.000.000
   500.000
   250.000
   125.000
    62.500
    31.250
    15.625
     7.812
     3.906
     1.953
       977
       488
       244
       122
        61
        30
        15
         7
         3
         1  En 20 operaciones... en el peor caso he encontrado un dato de relevancia entre 1M de datos.
Ahora... para poder usar este algoritmo necesito los datos ordenados. Si los datos no están ordenados necesito hacer un FULLSCAN.
Ahora bien... si tengo una tabla con 30 campos... puedo ordenarlos por 1 de ellos... y si quiero hacer búsquedas por 10 campos???
ESTOY JODIDO... solo para una puedo hacer el algoritmo de búsqueda binaria. Para el resto de columnas me toca hacer un FULLSCAN = RUINA !!!!

Para eso creamos los INDICES.
Un ÍNDICE NO ES SINO UNA **COPIA** ORDENADA DE LOS DATOS.

INDICE DE PLATOS DE COMIDA:
    TITULO (duplicado)                              UBICACION
    Corderito asado con patatas panaderas           pag 17.

INDICE por tipos de comida
    ARROCES
    TORTILLAS
    PASTA
    ENSALADAS
    PLANTOS PRINCIPALES
        Corderito asado con patatas panaderas           pag 17.

Las BBDD tienen índices...
Las herramientas de BI NO tienen índices.. o si tienen algo.. es muy limitado.

Si pongo a Quick Sight a trabajar contra mi BBDD.. tirando queries cada vez que sea necesario, podrá aprovecharse de los índices que tenga la BBDD. Eso si... tengo un problemilla... Para cada dato que quiero sacar, necesito ir a la BBDD (demora)
Si pongo a Quick Sight a trabajar con datos preimportados (SPICE) no tengo índices... y por tanto no puedo hacer búsquedas rápidas. Pero tengo un problema menos... no tengo que ir a la BBDD cada vez que quiero un dato (velocidad).

CUAL ES LA BUENA !!!! BUFFF dificil.
En general, importa los datos me ofrece mucho mejor rendimiento.... si tengo los datos estructurados de forma adecuada.

AQUI HAY OTRO TEMA al usar herramientas de BI. Los índices son críticos si quiero buscar datos sueltos.
En BI (a priori) no buscamos datos sueltos! Quiero todos los datos: ESTADISTICAS
Me trae más cuenta hacer el FULLSCAN que acceder por un índice.
Además, estas herramientas guardan una cache de resultados.
Si pedimos a Quicksight que actualice los datos (reimporte) a su motor spice cada noche... Quicksight sabe que la misma query ejecutada a los largo del mismo día va a dar el mismo resultado... y lo tiene cacheado.
Si le pido que trabaje online con la BBDD... agárrate a la silla! La BBDD si tiene una cache... posiblemente el camino de ida y vuelta me mate.

Todo este tingleo, solo lo necesitamos tener en cuenta cuando empecemos a meter en nuestros cuadros de mando FILTROS!

---

Nombre


---

Si lo que analizo son Juegos:
   Qué es el Nombre? Identificador

Si lo que analizo son ventas:
    Qué es el Nombre? Dimensión (Variable categórica/nominal/cualitativa)

---
JUEGO     11.000 registros

    Nombre    | Editorial   | Fecha de salida   | Género     | Ventas

    En este caso, la columna Nombre es única... Es el identificador.

    ^^^^^^^^^^    SELECT Nombre, Editorial, Fecha de salida, Género, sum( Ventas ) as Ventas
                    FROM JUEGOSxPlataforma GROUP BY Nombre;

JUEGOS x PLATAFORMA  16.000 registros

    Nombre    | Editorial   | Plataforma   | Fecha de salida   | Género     | Ventas

    La combinación Nombre/plataforma es única. Es el identificador.


    ^^^^^^^^^^    SELECT Nombre, Editorial, Plataforma, Fecha de salida, Género, count(*) as Ventas , count_if( region = 'NA') as VentasNA, count_if( region = 'JP') as VentasJP, count_if( region = 'EU') as VentasEU, count(*) as VentasGlobales
                    FROM VENTAS GROUP BY Nombre, Plataforma;

VENTAS 8.800 Millones de registros

    NUMERO DE VENTA | Jugador    | Fecha Venta | Juego(Nombre)   | Región | Editorial  | Plataforma   | Género | Fecha publicación
                1     Felipe       2023-10-01   Super Mario Bros     NA       Nintendo    Switch      Plataformas | 2023-10-01
                2     Juan         2023-10-01   Super Mario Bros     JP       Nintendo    Switch      Plataformas
                3     Juan         2023-10-01   Call of Duty         NA       Activision  PS5         Shooter
                4     Juan         2023-10-01   Call of Duty                  Activision  PS5         Shooter
                5     Juan         2023-10-01   Call of Duty                  Activision  PS5         Shooter
                6     Juan         2023-10-01   Call of Duty                  Activision  PS5         Shooter
                7     Juan         2023-10-01   Wii Sports                    Nintendo    Switch      Deportes
    
    En este caso qué sería el ID?    Un id autogenerado. NUMERO DE VENTA
    Qué es la columna Juego(Nombre)? VARIABLE NOMINAL

---

Qué variables hay?
    Juego
    Editorial
    Plataforma
    Genero
    Fecha publicación -> AÑO/MES
    Región
    Ventas global (FRECUENCIA)  

---

Estudios a nivel de juego:
Qué plataforma tiene más juegos?
Que año se publican más juegos?
Cambios de tendencia en la publicación de juegos?
(Si hago estudios de juegos, no tiene sentido hablar de zonas)

Estudios a nivel de ventas:
Qué plataforma tiene más ventas?
Que año se venden más juegos?
Cambios de tendencia en la venta de juegos?
En qué zonas se venden más juegos?          Si hago estudios de ventas, tiene sentido hablar de zonas


Estudiar los cambios de tendencia (variable temporal: FECHA / AÑO) de VENTAS de juegos x zona geográfica

AÑO X #JUEGOs

AÑO X Ventas

AÑO X Ventas X Zonas

---

Altura      Cuanti
Edad        Cuanti
Sexo        Cuali (Dicotómico) 

Scatter plot (2 cuantis + 1 cuali)


Seguros médicos EEUU
Zonas EEUU (Norte, sur,oeste, este)
Edad
Número hijos
Fumador
Coste que ha supuesto para la compañía de seguros

Scatter plot

COSTE
    ^
    |
    |
    |
    |
    |
    +----------------------------------------------------> EDAD


Las variables Cualitativas sirven para clasificar.
1 cuali con 10 grupos
Otra cuali con 5 grupos
Otra cuali con 4 grupos

Si cruzo las 3 tengo en total = 10x5x4 = 200 grupos NO ME DA EL CEREBRO

---

Qué puede afectar al precio?
- AÑO (inflacción)
- GENERO ????
- PLATAFORMA ???? Ya hay indicios
- EDITORIAL ????

PRECIO x AÑO = SCATTER PLOT (Dispersión)
PRECIO x GENERO = LINEAS (Precio medio/mediano)
                  BOXPLOT MULTIPLE (diagrama de caja/bigote) agrupando por la variable categórica (GENERO)
ESTO MISMO SERIA PARA CADA UNA DE LAS VARIABLES CUALITATIVAS


PRECIO x AÑO = SCATTER PLOT (Dispersión)
            x GENERO (color)
            x PLATAFORMA (color)
            x EDITORIAL (color)

----

Tablas de percentiles - Pediatras. Hablamos de individuos entre 0 y 14 años

Edad
Sexo
Altura



Peso:
Os digo... entra por la puerta alguien de 2 meses. Dadme una estimación del peso.
  Entorno a 3kg..4kg
Os digo... entra por la puerta alguien de 14 años. Dadme una estimación del peso.
  Entorno a 50 kgs
  ^^ ACERTAREMOS más o menos? BASTANTE
     Os jugáis 50€ a que acertáis 5kgs arriba/abajo?

Os digo... entra por la puerta alguien que es un niño (sexo hombre!). Dadme una estimación del peso.
  NPI
  2.5 kgs... 60 kgs
     Os jugáis 5€ a que acertáis 5kgs arriba/abajo? Ni de broma

La variable EDAD guarda mucha relación con la variable PESO.
La variable sexo guarda mucha relación con la variable PESO? NO.. muy poquita
La variable ALTURA guarda mucha relación con la variable PESO. SI
  Lo que pasa es que parte de esa relación ya la contemplamos con la variable EDAD.


Porque lo que cuenta la variable sexo no lo cuenta la variable EDAD
Hay relación entre sexo y edad? NINGUNA
En cambio si hay relación entre edad y altura
O entre fecha de publicación y plataforma
Parte de la carestía de un juego debido a la plataforma... realmente es porque esa plataforma se ha jugado en un momento determinado del tiempo... donde los precios eran más caros o más baratos.

El sexo... por si solo no nos cuenta mucho. Pero nos cuenta algo que solo el sexo nos cuenta.
Las niñas entre 9-13 años tienden a ser un poquito más altas que los niños de la misma edad.
Entre 2-5 cms.

Cuando tomamos decisiones de negocio... y nos basamos en datos (BI) (y aunque no sean decisiones de negocio... es lo mismo) me da igual equivocarme. Sabemos que nos vamos a equivocar.
No somos dios. ni omnipotentes, ni omniscientes, ni nada de nada.
Solo Dios sabe lo que va a pasar en el futuro.
Lo único que me interesa es ser capaz de CUANTIFICAR la probabilidad de equivocarme!

    Le doy a esta persona la hipoteca? o no? Me da igual equivocarme.
    Lo que me interesa, lo único que me interesa es saber si la probabilidad de que me equivoque es del 1% o del 99%.
    Si sé a priori que me equivocaré en el 25% de las decisiones... me vale!

    Ese 25% de gastos que tengo extra por las personas que no me pagan la hipoteca... 
    lo reparto entre el 75% de los que si me la pagan... 
    Y ya lo tengo compensado!

    Y si consigo rebajar esa probabilidad un 2%... menos tengo que compensar... y más barato salgo al mercado.

Compañía de seguros médicos.
Y tengo todos los datos habidos y por haber de una persona... desde que nació. Que come, que bebe.. que deportes hace y ha hecho. Su genoma.
Tengo idea de los costes que me va a ocasionar esa persona el año que viene? Soy capaz de predecirlo?
NPI.