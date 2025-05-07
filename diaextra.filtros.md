
Cuando creamos un filtro, lo que hacemos es añadir un WHERE al conjunto de datos.
Puede ser al conjunto que se utiliza en toda la hoja o solo a un elemento visual.

    TABLA VENTAS

Por defecto, que query se hace?      SELECT * FROM VENTAS

Cuando pongo un filtro, por ejemplo, nuestro filtro de RANGO por ANYO:

    SELECT * FROM VENTAS WHERE ANYO BETWEEN 2010 AND 2015

Los campos numéricos, me permiten generar filtro agrupados o no agrupados.
Si no agrupo, el filtro se aplica a cada uno de los valores (WHERE)

Pero si agrupo, el filtro deja de actuar como un WHERE y actúa como un HAVING.

Imaginad que uso para el filtro la columna VentasJP.
Quiero un valor mínimo para la columna VentasJP de 1000.

    SELECT * FROM VENTAS WHERE VentasJP > 1000

El componente visual (gráfico de anillo) VENTAS GLOBAL POR GENERO, que query tira?

    SELECT COUNT(*) FROM VENTAS GROUP BY GENERO

Al haber metido el filtro, la query real que se ejecuta es:

    SELECT COUNT(*) FROM VENTAS WHERE VentasJP > 1000 GROUP BY GENERO

Pero si el filtro lo definimos como agrupado, la query que se ejecuta es:

    SELECT COUNT(*) FROM VENTAS GROUP BY GENERO HAVING SUM(VentasJP) > 1000

---

Los análisis me permiten montar tableros en modo edición.
Esos análisis luego los publico! y lo que se genera es una vista no editable!

---

Los parámetros nos dan CONSTANTES, que puedo definir.

PARAMETRO: VALOR_MINIMO_VENTAS = 1000
Y ahora monto un filtro basado en el parámetro:

    SELECT * FROM VENTAS WHERE VentasJP > VALOR_MINIMO_VENTAS


---

Grafico de areas/Lineas

Valor: SUM(Ventas)
Eje X: MES
Agrupas por año
Filtro fecha sea desde 2 año antes del actual y hasta 1 año antes del actual