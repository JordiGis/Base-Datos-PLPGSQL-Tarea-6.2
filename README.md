1. Investiga que son los procedimientos y las funciones en postgreSQL, intenta crear una tarea simple como crear un tabla que se llame prueba_ud6.
    ```sql
        CREATE OR REPLACE
        PROCEDURE testPostgre.crearTabla() LANGUAGE plpgsql
            AS $procedure$
                BEGIN
                    CREATE TABLE IF NOT EXISTS prueba_ud6 (
                            id int PRIMARY KEY,
                            nombre VARCHAR(100)
                        )
                END
            $procedure$
    ```
    El objetivo de este codigo es crear una tabla llamada "prueba_ud6", primero comprobando si esa tabla existe, en el caso que no exista, se creara.

2. A partir de la funciona anterior intenta crear ahora una función que genera una tabla recibiendo un nombre como parámetro.

    ```sql
        CREATE OR REPLACE
        PROCEDURE testPostgre.crearTabla(nombre VARCHAR(100)) LANGUAGE plpgsql
            AS $procedure$
                BEGIN
                    CREATE TABLE IF NOT EXISTS prueba_ud6 (
                            id int PRIMARY KEY,
                            nombre VARCHAR(100)
                        );
                    INSERT INTO prueba_ud6 (id, nombre) VALUES (1, nombre);
                END
            $procedure$
    ```
    El objetivo de la ampliación de este procedimiento es que se cree la tabla como antes, pero recibe una parametro nombre, que luego lo usa para hacer un insert con ese nombre a la tabla anterior mente creada.

3. ¿Qué diferencias crees que hay entre funciones y procedimientos?   
   La diferencia es que las funciones como las de Java tienen que devolver un valor, sino serian un método, pero en este caso en vez de método, se llamara procedimiento, por ende la diferencia es que función devuelve un valor, y el procedimiento no.

4. Realiza los siguientes procedimientos (sin ejecutarlos):
   1. Un procedimiento que devuelva el stock de un determinado artículo.
        ```sql
        CREATE OR REPLACE
        PROCEDURE testPostgre.stockArticulo(IN idArticulo int, INOUT cantidad int) LANGUAGE plpgsql
            AS $procedure$
                BEGIN
                    SELECT stock INTO cantidad 
                    FROM articulo WHERE id = idArticulo;
                END
            $procedure$
        ```
        Este procedimiento lo que hara sera una consula al stock del articulo, y almacenar ese valor en la variable cantidad.
   2. Un procedimiento que devuelva el total facturado entre 2 fechas.
        ```sql
        CREATE OR REPLACE
        PROCEDURE testPostgre.totalFacturadoFechas(IN fechaIni date, IN fechaFin date, INOUT facturado int) LANGUAGE plpgsql
            AS $procedure$
                BEGIN
                    SELECT SUM(total_facturado) INTO facturado
                    FROM facturas
                    WHERE fecha_factura BETWEEN fechaIni AND fechaFin;
                END
            $procedure$
        ```
        Este procedimiento necesita dos parametros date, que son fechas, tando la de inicio como la de fin, para filtrar entre esas dos, sumandolo todo y guardandolo en la variable facturado.
   3. Un procedimiento de tu invención que creas que te podría venir bien para futuros usos.
        ```sql
        CREATE OR REPLACE
        PROCEDURE testPostgre.reguentoUsuariosPorPais(IN Pais Varchar(100), INOUT recuento int) LANGUAGE plpgsql
            AS $procedure$
                BEGIN
                    SELECT COUNT(id) INTO recuento
                    FROM usuario
                    WHERE pais = Pais;
                END
            $procedure$
        ```
        Este procedimiento cuenta los usuarios de determinado pais, que es pasado como parametro.
