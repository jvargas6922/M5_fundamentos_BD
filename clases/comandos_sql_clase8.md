/*
Utilizaremos la base de datos que tenemos de libreria:

1. Crear una tabla llamada "Categorias" con 2 columnas: id_categoria (PK)y nombre_categoria.
2. Agregar a nuestra tabla libros los campos precio, id_categoria (FK).
3. Insertar algunos datos de ejemplo para probar las relaciones.
*/

-- creamos la tabla categorias
create table categorias(
	id_categoria serial primary key,
	nombre_categoria varchar(60),
	created_at timestamp default current_timestamp
);

select * from libros l ;

-- agregamos un nuevo llamado precio campo a nuestra tabla libros.
--ALTER TABLE libros ADD precio decimal(10,2);

-- agregar un nuevo campo llamado categoria_id integer fk

-- primero agregamos el campo con su tipo de dato
ALTER TABLE libros ADD categoria_id integer;


-- Luego agregamos la relacion entre las tablas
ALTER TABLE libros
    ADD constraint categoria_id 
    FOREIGN KEY (categoria_id)
    REFERENCES categorias(id_categoria);

-- agregar regitros a tabla categoria
insert into categorias (nombre_categoria)
	values
		('Romanticas'),
		('Terror'),
		('Suspenso'),
		('Ficción'),
		('Programación'),
		('Historico'),
		('Infantil');



