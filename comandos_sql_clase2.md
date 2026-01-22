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


-- practica de tienda

create table ingredientes(
	id_ingrediente serial primary key,
	nombre_ingrediente varchar(50) not null,
	valor float
);

create table productos(
	id_producto serial primary key,
	nombre_producto varchar(50) not null,
	valor float
);

create table clientes(
	id_cliente serial primary key,
	nombre_cliente varchar(60) not null
);

create table pedidos(
	id_pedido serial primary key,
	cliente_id integer,
	foreign key(cliente_id) references clientes (id_cliente)
);

create table pedidos_detalle(
	id_pedido_detalle serial primary key,
	pedido_id integer,
	producto_id integer,
	cantidad integer,
	ingrediente_id integer,
	foreign key (pedido_id) references pedidos(id_pedido),
	foreign key (producto_id) references productos (id_producto),
	foreign key (ingrediente_id) references ingredientes(id_ingrediente)
);


-- registros de la tabla ingredientes
insert into ingredientes (nombre_ingrediente, valor) 
	values
		('palta'  ,500),
		('tomate' ,500),
		('chucrut',500),
		('vianesa',700);

-- registros de la tabla productos
insert into productos(nombre_producto, valor)
	values
		('completo dinamico', 3500),
		('completo', 2500),
		('americano', 2000),
		('chacarrero', 3500),
		('italiano', 3000);

-- registros de la tabla clientes
insert into clientes(nombre_cliente)
	values
		('Joffred'),
		('Oscar'),
		('Franco'),
		('Lorena'),
		('Raul');

-- registros de la tabla pedidos y pedidos_detalle
insert into pedidos(cliente_id) values(1);
insert into pedidos_detalle (pedido_id, producto_id, cantidad, ingrediente_id)
	values
	(1, 1, 1, 1),
	(1, 4, 1, 2),
	(1, 5, 1, 4);

	
	









