# Seguridad y control de acceso a los datos.

La idea es que vamos a generar cuadros de mando.
Esos de cuadros de mando van a tener un control de acceso: Quién puede ver el cuadro de mando.
El tema es que esto no es suficiente. Es un mínimo.
Lo que ocurre es que en muchas ocasiones me interesa que distintas personas accedan al mismo cuadro de mando pero viendo diferentes datos.

Me interesa que la gente de Europa vea las cuentas (ventas) de Europa.
Mientras que la gente de japón vea las cuentas de Japón.
Y los de USA vean las cuentas de USA.

El cuadro de mando es el mismo... pero le aplicamos diferentes datos en base al usuario que se conecta.

En nuestro caso, tenemos la información de la región dónde? En una columna de un conjunto de datos (el conjunto de datos se crea desde un excel... pero eso no es relevante).
Me gustaría poder mostrar/ocultar columnas en función del usuario.

Otro caso... Quizás hay gente que tengo trabajando en distintas plataformas. Y me interesa que ciertos usuarios vean solo los datos de esas plataformas.

En nuestro caso, la información de la plataforma la tenemos dónde? en una columna... pero de una fila.

JUEGOS

    Nombre          Plataforma       Ventas EU     Ventas USA
    Counter-Strike  PC                  5000          7000
    Counter-Strike  PS4                 2000          3000

Al jefe de la región EU le quiero permitir acceder a qué datos? LIMITO LAS COLUMNAS a las que puede acceder.

    Nombre          Plataforma       Ventas EU
    Counter-Strike  PC                  5000  
    Counter-Strike  PS4                 2000  

Al jefe de la plataforma PC le quiero permitir acceder a qué datos? LIMITO LAS FILAS a las que puede acceder.

    Nombre          Plataforma       Ventas EU     Ventas USA
    Counter-Strike  PC                  5000          7000


Estas son las opciones que me va a permitir el Quicksight:
- Usuarios
- Grupos de usuarios (cuya finalidad es facilitar el mantenimiento de los permisos)
- Conjuntos de datos
   - Podemos definir quién tiene acceso al conjunto de datos (Usuario o Grupo de usuarios) y con que privilegios (lectura o escritura).                                     FÁCIL
   - Adicionalmente podemos limitar las columnas a las que puede acceder el usuario o grupo de usuarios.                                                              FÁCIL
   - Adicionalmente podemos limitar las filas a las que puede acceder el usuario o grupo de usuarios. Hay 2 formas de hacerlo:
     - Tablas de permisos.                                     Dificultad MEDIA
       - Más laboriosa de mantener en el tiempo.
     - TAGS de usuario.                                        Dificultad ALTA (más avanzada... requiere de conocimientos más avanzados de programación)
       - Más fácil de mantener en el tiempo.
- Análisis/Paneles
  - Podemos definir quién tiene acceso al análisis/panel (Usuario o Grupo de usuarios) y con que privilegios (lectura o escritura)
  - La información (permisos) de a quñé datos (filas/columnas) puede acceder el usuario o grupo de usuarios se hereda de los conjunto de datos que se utilizan en el análisis/panel.
---

    Nombre          Plataforma       Ventas            Region
    Counter-Strike  PC                  5000           EU
    Counter-Strike  PC                  7000           USA
    Counter-Strike  PS4                 2000           EU
    Counter-Strike  PS4                 3000           USA

---

# Seguridad y control de acceso a las aplicaciones (mundo web)

- Identificación            Decir quien soy
- Autenticación             Comprobar que eres quien dices ser
                            ^^^^^^^^^^^^^
                            No la gestiona el propio Quicksight
                            La delega en una herramienta externa que yo configuro la que quiera configurar.

- Autorización              Sabiendo que eres quien dices ser, 
                            saber qué puedes hacer (limitar lo que puedes hacer)
                            ^^^^^^
                            La gestiona el propio Quicksight

En el mundo WEB hoy en día esa es una práctica habitual. El delegar la autenticación en una herramienta externa.
Esto nos permite varias cosas:
- Yo, desarrollador de una aplicación en general tengo muy pocos conocimientos de seguridad.

  Como se guarda una contraseña en una BBDD? La guardaríamos encriptada? NO
  Nunca guardamos una contraseña ni en una BBDD ni en ningún sitio.

  Lo que guardamos es un hash de una contraseña. Una huella.

  HASH (HUELLA). Básicamente la letra del DNI
  Una función que dada una entrada:
  - Siempre genera la misma salida
  - Desde la salida es imposible regenerar la entrada (la salida es un "resumen" de la entrada)
  - Haya "muy poca" probabilidad de que 2 entradas distintas generen la misma salida (colisión)
    Haya un porcentaje muy bajo de colisiones.

    En el DNI 1/24 ~= 4%... El ministerio de interior ha decidido que para ellos un 4% es un porcentaje bajo.
    En informática usamos algoritmos mucho más potentes que el del DNI... con porcentajes de colisión mucho más bajos.
    SHA256 (algoritmo de hash) tiene un porcentaje de colisión de 1/2^256

  De hecho en una bbdd buena de usuarios e identidades, lo que habitualmente se guarda es el hash del hash del hash del hash (y así hasta 1000 veces) de la contraseña.

  Estas cosas, las tiene muy controlada la gente que sabe de seguridad... no los desarrolladores.. que sabemos de desarrollo.
- Para el usuario de la app... es más cómodo tener un único sistema que le autentique en todas las aplicaciones. Así se evita tener que recordar 1000 contraseñas... y mantenerlas... etc.
- Es más, esos sistemas se desarrollan con muchas medidas de protección adicionales:
  - Autenticación basada en geolocalización
  - Autenticación multifactor (tener físicamente tu telefono móvil | reconocimiento facial)
  - Monitoreo de actividad sospechosa
    

Yo monto un sistema y delego en otro la autenticación del usuario.
El otro sistema... el que autentica, cuando autentica, genera lo que se llama un TOKEN DE SESIÓN: JWT.
En ese token se incluyen varias cosas:
- Nombre del usuario
- Email del usuario
- Fecha de caducidad del token
- Y otros metadatos:
  - Teléfono
  - ETIQUETA
        Plataforma: [PS, PS2, PS3]
- También viene un token (firma generada por el sistema que autentica) que permite comprobar a mi aplicación que los datos no han sido manipulados.

Como digo, en ese token, pueden venir metadatos extra.
Pero eso es algo que configuramos en la herramienta externa de validación (KeyCloak).

Quick sight puede usar esa información de etiquetas/metadatos para limitar el acceso a determinadas filas del conjunto de datos.

Es una forma muy limpia de hacer una integración de seguridad.
Puedo usar esas etiquetas para limitar el acceso a diferentes filas de diferentes conjuntos de datos.

Toda la información de qué puede ver o no un usuario queda "delegada" al sistema externo.
El sistema es el que aporta esos datos.
Quicksight aplica esos datos para efectivamente limitar el acceso a los datos.


---

Dataset Juegos sin limitar
Dataset Juegos con permisos

Cuadro de mando:
    Algunos elementos visuales (KPIs más generales) los sacas sobre el dataset sin limitar
Otros elementos (en la misma pestaña o en otra) con más nivel de detalle los sacas del dataset que tienes limitado.



    CONJUNTO de datos 1 -> CONJUNTO de datos 2 ->                   Dashboard
     ^^^
     Limitación de filas                                            ERROR No cuela

                                ^^^
                                Limitación de filas                 Si cuela.. es la forma de hacerlo

---

JAVA

String nombre = "Ivan";

    Estoy asignando la variable al valor Ivan!

nombre = "Pepe";  // Dónde estoy guardando el valor? en el mismo espacio de RAM donde estaba la palabra IVAN o en otro? OTRO!
Si lo hiciera en C, sería en el mismo... pero al hacerlo en JAVA se guarda en otro.


            CURSOS < INSCRIPCIONES > PERSONAS > EMPRESAS





    <iframe
        width="960"
        height="720"
        src="https://eu-west-1.quicksight.aws.amazon.com/sn/embed/share/accounts/820634527231/dashboards/66e75148-8116-4290-a99e-99063a62a642?directory_alias=Formacion">
    </iframe>