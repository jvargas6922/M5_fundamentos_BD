-- soy un comentario de una linea en SQL

/*
 Soy un comentario en bloque que 
 me permite hacer varias ejecuciones
 */

-- crear tabla estudiantes
CREATE TABLE estudiantes(
	id_estudiante SERIAL PRIMARY KEY,
	nombre varchar(100),
	email varchar(100) UNIQUE,
	edad integer,
	created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);


-- consultar registros a nuestra tabla estudiantes 
-- esta query me trae todos los regitros de la tabla estudiantes.
SELECT * FROM estudiantes;

-- esta query me trae solo los nombres de la tabla estudiante.
SELECT nombre FROM estudiantes;


-- insercion de 1 registro
-- INSERT INTO estudiantes (nombre, email, edad) VALUES ('Juan Pérez', 'juan@mail.com', 25);

-- insercion de más de 1 registro
/*
INSERT INTO estudiantes (nombre, email, edad) VALUES
        ('Ana Díaz', 'ana@mail.com', 22),
        ('Pedro Soto', 'pedro@mail.com', 30);
*/


-- consulta de un registro con un filtro estatico o igual a una cantidad
SELECT 
	* 
FROM 
	estudiantes e 
WHERE 
	e.edad = 30;


-- consulta de un registro con un filtro estatico o igual a un valor
SELECT 
	* 
FROM 
	estudiantes e 
WHERE 
	e.edad > 18;

-- ordenar registros de forma ascendente
SELECT * FROM estudiantes ORDER BY edad;


-- ordenar registros de forma ascendente
SELECT * FROM estudiantes ORDER BY edad DESC;

-- uso de limit 
SELECT 
	* 
FROM 
	estudiantes 
ORDER BY 
	edad 
DESC 
LIMIT 1;

-- uso del count
SELECT count(*) FROM estudiantes e ;



