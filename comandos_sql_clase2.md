-- Clase 2

select * from estudiantes e ;

-- crear una segunda tabla que me permite hacer una relacion
/*
 * Relaciones que pueden tener las tablas 
 * 	1)  1 - 1
 * 	2)  1 - N
 * 	3 	N - N 
 */


/*
CREATE TABLE cursos (
     id_curso  SERIAL PRIMARY KEY,
     nombre VARCHAR(100)
);
*/


/*
CREATE TABLE inscripciones (
   id_inscripcion SERIAL PRIMARY KEY,
   estudiante_id INTEGER,
   curso_id INTEGER,
   FOREIGN KEY (estudiante_id) REFERENCES estudiantes(id_estudiante),
   FOREIGN KEY (curso_id) REFERENCES cursos(id_curso)
);
*/


-- Consultas de registros
select * from estudiantes e ;
select * from cursos c ;
select * from inscripciones i ;

-- insercion de registros en la tabla curso 
insert into cursos(nombre) values('Python');
insert into cursos(nombre) values('Javascript');
insert into cursos(nombre) values('Base de datos');


-- insercion a la tabla incripciones
insert into inscripciones (estudiante_id, curso_id) values(2,1);


-- consulta de tablas relacionales
select 
	i.id_inscripcion,
	c.nombre as nombre_curso,
	e.nombre as nombre_estudiante,
	e.edad,
	e.email
from 
	inscripciones i
	join estudiantes e 
		on i.estudiante_id = e.id_estudiante
	join cursos c 
		on i.curso_id = c.id_curso; 
	
	









