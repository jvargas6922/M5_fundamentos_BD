Comandos básicos de SQL en PostgreSQL (Guía para principiantes)
🗄️ BASES DE DATOS
    Crear una base de datos
    CREATE DATABASE escuela;

    Eliminar una base de datos
    DROP DATABASE escuela;

    Crear usuario
    CREATE ROLE alumno WITH LOGIN PASSWORD '1234';

    Dar permisos a un usuario
    GRANT ALL PRIVILEGES ON DATABASE escuela TO alumno;


    Crear una tabla
    CREATE TABLE estudiantes (
        id_estudiante SERIAL PRIMARY KEY,
        nombre VARCHAR(100),
        email VARCHAR(150),
        edad INTEGER,
        created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
    );


    Lo que hace cada atributo:
        SERIAL: número automático
        PRIMARY KEY: identificador único
        VARCHAR: texto
        TIMESTAMP: fecha y hora


    Eliminar una tabla
    DROP TABLE estudiantes;

CAMPOS (COLUMNAS)
    Agregar un campo nuevo
        ALTER TABLE estudiantes ADD telefono VARCHAR(20);

    Editar tipo de un campo
        ALTER TABLE estudiantes ALTER COLUMN telefono TYPE VARCHAR(30);

    Renombrar un campo
        ALTER TABLE estudiantes RENAME COLUMN telefono TO celular;

    Eliminar un campo
        ALTER TABLE estudiantes DROP COLUMN celular;

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
        WHERE id = 1;


!!! Siempre usar WHERE, si no, se actualiza toda la tabla !!!
                        IMPORTANTE
                        
                        IMPORTANTE
!!! Siempre usar WHERE, si no, se borra todos los registros de toda la tabla !!!

    Eliminar un registro
        DELETE FROM estudiantes WHERE id = 1;

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

    Crear tabla relacionada
        CREATE TABLE cursos (
            id SERIAL PRIMARY KEY,
            nombre VARCHAR(100)
        );

        CREATE TABLE inscripciones (
            id SERIAL PRIMARY KEY,
            estudiante_id INTEGER,
            curso_id INTEGER,
            FOREIGN KEY (estudiante_id) REFERENCES estudiantes(id),
            FOREIGN KEY (curso_id) REFERENCES cursos(id)
        );


    Qué hace:
        Relaciona estudiantes con cursos.

    TRUNCATE (Borrar todo rápido)
        TRUNCATE TABLE estudiantes RESTART IDENTITY;

📌 Borra todos los datos y reinicia el ID.

TRANSACTIONS
BEGIN;

UPDATE estudiantes SET edad = 40 WHERE id = 2;

ROLLBACK; -- deshace
-- COMMIT; -- confirma

COMANDOS QUE DEBES RECORDAR SÍ O SÍ
    Comando	Para qué sirve
        CREATE	Crear
        DROP	Eliminar
        ALTER	Modificar
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
        JOIN inscripciones ON estudiantes.id = inscripciones.estudiante_id
        JOIN cursos ON cursos.id = inscripciones.curso_id;

    Qué hace:
        Muestra los nombres de estudiantes junto con los cursos en los que están inscritos.

LEFT JOIN (Unir tablas, incluso sin coincidencia)
        SELECT estudiantes.nombre, cursos.nombre
        FROM estudiantes
        LEFT JOIN inscripciones ON estudiantes.id = inscripciones.estudiante_id
        LEFT JOIN cursos ON cursos.id = inscripciones.curso_id;

    Qué hace:
        Muestra todos los estudiantes, incluso si no están inscritos en ningún curso.


RIGHT JOIN (Unir tablas, incluso sin coincidencia)
        SELECT estudiantes.nombre, cursos.nombre
        FROM estudiantes
        RIGHT JOIN inscripciones ON estudiantes.id = inscripciones.estudiante_id
        RIGHT JOIN cursos ON cursos.id = inscripciones.curso_id;

    Qué hace:
        Muestra todos los cursos, incluso si no tienen estudiantes inscritos.

-- Uso del group by y having
-- El GROUP BY agrupa los resultados según un campo específico.
-- Lo que hace el HAVING: filtra los resultados después de agruparlos con GROUP BY.

    SELECT edad, COUNT(*) as cantidad
    FROM estudiantes
    GROUP BY edad
    HAVING COUNT(*) > 1;

-- comandos para la creacion de base de datos por comandos SQL
    CREATE DATABASE nombre_basedatos;
-- para conectarse a la base de datos en sql
    \c nombre_basedatos;
-- agregar un campo nuevo a una tabla
    ALTER TABLE nombre_tabla ADD nombre_campo TIPO_DATO;
-- eliminar un campo de una tabla
    ALTER TABLE nombre_tabla DROP COLUMN nombre_campo;
-- eliminar una tabla
    DROP TABLE nombre_tabla;
-- eliminar una base de datos
    DROP DATABASE nombre_basedatos;
-- crear un indice en una tabla
    CREATE INDEX nombre_indice ON nombre_tabla (nombre_campo);
-- eliminar un indice en una tabla
    DROP INDEX nombre_indice;
-- crear una vista
    CREATE VIEW nombre_vista AS
    SELECT columna1, columna2
    FROM nombre_tabla
    WHERE condicion;
-- eliminar una vista
    DROP VIEW nombre_vista;
