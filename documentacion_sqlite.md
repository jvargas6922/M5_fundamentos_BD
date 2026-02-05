Comandos básicos de SQL en SQLite (Guía para principiantes)
🗄️ BASES DE DATOS
    Crear una base de datos
    -- En SQLite, se crea al conectarse por primera vez
    sqlite3 escuela.db

    Eliminar una base de datos
    -- Simplemente eliminar el archivo .db
    -- En terminal: rm escuela.db

    Usuarios y permisos
    -- SQLite NO maneja usuarios ni permisos
    -- La seguridad se gestiona a nivel de archivo del sistema operativo


    Crear una tabla
    CREATE TABLE estudiantes (
        id_estudiante INTEGER PRIMARY KEY AUTOINCREMENT,
        nombre TEXT,
        email TEXT,
        edad INTEGER,
        created_at DATETIME DEFAULT CURRENT_TIMESTAMP
    );


    Lo que hace cada atributo:
        INTEGER PRIMARY KEY AUTOINCREMENT: número automático
        PRIMARY KEY: identificador único
        TEXT: texto (SQLite no requiere especificar longitud)
        DATETIME: fecha y hora


    Eliminar una tabla
    DROP TABLE estudiantes;

CAMPOS (COLUMNAS)
    Agregar un campo nuevo
        ALTER TABLE estudiantes ADD COLUMN telefono TEXT;

    Editar tipo de un campo
        -- SQLite NO permite modificar tipos de columnas directamente
        -- Se debe recrear la tabla:
        -- 1. Crear tabla temporal
        CREATE TABLE estudiantes_temp (
            id_estudiante INTEGER PRIMARY KEY AUTOINCREMENT,
            nombre TEXT,
            email TEXT,
            edad INTEGER,
            telefono TEXT  -- nuevo tipo
        );
        -- 2. Copiar datos
        INSERT INTO estudiantes_temp SELECT * FROM estudiantes;
        -- 3. Eliminar tabla original
        DROP TABLE estudiantes;
        -- 4. Renombrar tabla temporal
        ALTER TABLE estudiantes_temp RENAME TO estudiantes;

    Renombrar un campo
        -- SQLite 3.25.0+ (versiones recientes)
        ALTER TABLE estudiantes RENAME COLUMN telefono TO celular;

    Eliminar un campo
        -- SQLite NO permite eliminar columnas directamente en versiones antiguas
        -- En SQLite 3.35.0+ (versiones recientes):
        ALTER TABLE estudiantes DROP COLUMN celular;
        
        -- En versiones antiguas, se debe recrear la tabla sin esa columna

REGISTROS (DATOS)
    Insertar un registro
        INSERT INTO estudiantes (nombre, email, edad) VALUES ('Juan Pérez', 'juan@mail.com', 25);

    Insertar varios registros
        INSERT INTO estudiantes (nombre, email, edad) VALUES
        ('Ana Díaz', 'ana@mail.com', 22),
        ('Pedro Soto', 'pedro@mail.com', 30);

    Ver registros
        SELECT * FROM estudiantes;

    Ver registros con filtro
        SELECT * FROM estudiantes WHERE edad > 25;

    Editar un registro
        UPDATE estudiantes
        SET edad = 26
        WHERE id_estudiante = 1;


!!! Siempre usar WHERE, si no, se actualiza toda la tabla !!!
                        IMPORTANTE
                        
                        IMPORTANTE
!!! Siempre usar WHERE, si no, se borra todos los registros de toda la tabla !!!

    Eliminar un registro
        DELETE FROM estudiantes WHERE id_estudiante = 1;

    CONSULTAS ÚTILES
    Ordenar resultados
        SELECT * FROM estudiantes ORDER BY edad DESC;

    Limitar resultados
        SELECT * FROM estudiantes LIMIT 5;

    Contar registros
        SELECT COUNT(*) FROM estudiantes;

    CONDICIONES
    AND / OR
        SELECT * FROM estudiantes WHERE edad > 20 AND edad < 30;

    LIKE (búsqueda por texto)
        SELECT * FROM estudiantes WHERE nombre LIKE '%Juan%';

    IN
        SELECT * FROM estudiantes WHERE edad IN (22, 25, 30);

CLAVES FORÁNEAS (MUY IMPORTANTE)

    Habilitar claves foráneas en SQLite
        -- Por defecto están deshabilitadas
        PRAGMA foreign_keys = ON;

    Crear tabla relacionada
        CREATE TABLE cursos (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            nombre TEXT
        );

        CREATE TABLE inscripciones (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            estudiante_id INTEGER,
            curso_id INTEGER,
            FOREIGN KEY (estudiante_id) REFERENCES estudiantes(id_estudiante),
            FOREIGN KEY (curso_id) REFERENCES cursos(id)
        );


    Qué hace:
        Relaciona estudiantes con cursos.

    DELETE (Borrar todo)
        DELETE FROM estudiantes;
        -- Para reiniciar el AUTOINCREMENT:
        DELETE FROM sqlite_sequence WHERE name='estudiantes';

📌 Borra todos los datos y reinicia el ID.

TRANSACTIONS
BEGIN TRANSACTION;

UPDATE estudiantes SET edad = 40 WHERE id_estudiante = 2;

ROLLBACK; -- deshace
-- COMMIT; -- confirma

COMANDOS QUE DEBES RECORDAR SÍ O SÍ
    Comando	Para qué sirve
        CREATE	Crear
        DROP	Eliminar
        ALTER	Modificar (limitado en SQLite)
        INSERT	Agregar datos
        SELECT	Consultar
        UPDATE	Editar datos
        DELETE	Eliminar datos
        WHERE	Filtrar
        ORDER BY	Ordenar
        LIMIT	Limitar


JOIN
    JOIN (Unir tablas)
        SELECT estudiantes.nombre, cursos.nombre
        FROM estudiantes
        JOIN inscripciones ON estudiantes.id_estudiante = inscripciones.estudiante_id
        JOIN cursos ON cursos.id = inscripciones.curso_id;

    Qué hace:
        Muestra los nombres de estudiantes junto con los cursos en los que están inscritos.

LEFT JOIN (Unir tablas, incluso sin coincidencia)
        SELECT estudiantes.nombre, cursos.nombre
        FROM estudiantes
        LEFT JOIN inscripciones ON estudiantes.id_estudiante = inscripciones.estudiante_id
        LEFT JOIN cursos ON cursos.id = inscripciones.curso_id;

    Qué hace:
        Muestra todos los estudiantes, incluso si no están inscritos en ningún curso.


RIGHT JOIN (Unir tablas, incluso sin coincidencia)
        -- SQLite NO soporta RIGHT JOIN
        -- Se puede simular intercambiando las tablas con LEFT JOIN:
        SELECT estudiantes.nombre, cursos.nombre
        FROM cursos
        LEFT JOIN inscripciones ON cursos.id = inscripciones.curso_id
        LEFT JOIN estudiantes ON estudiantes.id_estudiante = inscripciones.estudiante_id;

    Qué hace:
        Muestra todos los cursos, incluso si no tienen estudiantes inscritos.

-- Uso del group by y having
-- El GROUP BY agrupa los resultados según un campo específico.
-- Lo que hace el HAVING: filtra los resultados después de agruparlos con GROUP BY.

    SELECT edad, COUNT(*) as cantidad
    FROM estudiantes
    GROUP BY edad
    HAVING COUNT(*) > 1;

-- comandos para la creacion de base de datos
    -- En SQLite se crea automáticamente al conectarse:
    sqlite3 nombre_basedatos.db

-- para conectarse a la base de datos en sqlite
    sqlite3 nombre_basedatos.db

-- para ver las tablas existentes
    .tables

-- para ver la estructura de una tabla
    .schema nombre_tabla

-- para salir de sqlite
    .quit
    -- o
    .exit

-- agregar un campo nuevo a una tabla
    ALTER TABLE nombre_tabla ADD COLUMN nombre_campo TIPO_DATO;

-- actualizar un campo en una tabla
    -- SQLite NO permite cambiar tipos directamente
    -- Se debe recrear la tabla (ver sección CAMPOS arriba)

-- eliminar un campo de una tabla
    -- En SQLite 3.35.0+:
    ALTER TABLE nombre_tabla DROP COLUMN nombre_campo;
    -- En versiones antiguas se debe recrear la tabla

-- eliminar una tabla
    DROP TABLE nombre_tabla;

-- eliminar una base de datos
    -- Eliminar el archivo .db desde el sistema operativo

-- crear un indice en una tabla
    CREATE INDEX nombre_indice ON nombre_tabla (nombre_campo);

-- eliminar un indice en una tabla
    DROP INDEX nombre_indice;

-- crear una vista
    CREATE VIEW nombre_vista AS
    SELECT columna1, columna2
    FROM nombre_tabla
    WHERE condicion;

-- consultar una vista
    SELECT * FROM nombre_vista;

-- eliminar una vista
    DROP VIEW nombre_vista;

-- Agregar campos que son claves foraneas cuando ya tenemos creada la tabla
    -- SQLite NO permite agregar FOREIGN KEY después de crear la tabla
    -- Se debe recrear la tabla con la restricción incluida

-- agregar la condicion check a un campo
    -- Se debe incluir en la creación de la tabla:
    CREATE TABLE ejemplo (
        campo INTEGER CHECK (campo > 0)
    );
    
    -- O se puede recrear la tabla para agregar la restricción

-- uso de sumatorias en consultas SQL
SELECT SUM(edad) AS suma_edades FROM estudiantes;

-- otras funciones agregadas
SELECT AVG(edad) AS promedio_edades FROM estudiantes;
SELECT MAX(edad) AS edad_maxima FROM estudiantes;
SELECT MIN(edad) AS edad_minima FROM estudiantes;

TIPOS DE DATOS EN SQLite
    SQLite usa tipos de afinidad (tipado dinámico):
        NULL: valor nulo
        INTEGER: enteros
        REAL: números de punto flotante
        TEXT: cadenas de texto
        BLOB: datos binarios
    
    Nota: SQLite acepta otros nombres como VARCHAR, DATETIME, etc.
    pero los convierte internamente a estos 5 tipos.

COMANDOS ÚTILES DE LA CLI DE SQLite
    .help               -- Muestra ayuda
    .tables             -- Lista todas las tablas
    .schema [tabla]     -- Muestra estructura de tabla(s)
    .mode [modo]        -- Cambia formato de salida (column, csv, json, etc.)
    .headers on/off     -- Muestra/oculta encabezados
    .output [archivo]   -- Redirige salida a un archivo
    .read [archivo]     -- Ejecuta comandos SQL desde un archivo
    .dump [tabla]       -- Exporta tabla en formato SQL
    .import [archivo] [tabla] -- Importa datos desde archivo CSV

DIFERENCIAS CLAVE: PostgreSQL vs SQLite
    ✅ SQLite es más simple (sin usuarios, permisos, configuración)
    ❌ SQLite NO soporta RIGHT JOIN ni FULL OUTER JOIN
    ❌ SQLite tiene limitaciones con ALTER TABLE
    ✅ SQLite es ideal para desarrollo, prototipos y aplicaciones pequeñas
    ✅ PostgreSQL es mejor para aplicaciones empresariales y concurrencia
    ✅ SQLite se almacena en un solo archivo .db
    ✅ PostgreSQL requiere un servidor de base de datos
