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

select * from libros l;
select * from categorias c ;
select * from autores a ;

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

insert into categorias (nombre_categoria)
	values
		('Poesia');

-- normalizando los regitros de la tabla libros para el campo categoria_id
-- campo categoria_id
UPDATE libros
        SET categoria_id = 8
	where categoria_id is null;

-- campo precio
UPDATE libros
        SET precio = 10000
	where id_libro IN(1,2,3,4);

-- regitros a los que les vamos a poblar el campo precio
select * from libros l where l.id_libro IN(1,2,3,4);

-- consulta para los registros con el campo categoria_id = null
select * from libros l where l.categoria_id is null;

-- consulta para los registros con el campo categoria_id != null
select * from libros l where l.categoria_id is not null;


-- nuevos registros de la tabla autores
insert into autores(nombre, apellido, fecha_nacimiento, nacionalidad)
	values('Gabriel','Garcia Marquez','1927-03-06','Colombiano');

-- nuevo registro en la tabla libros
insert into libros(titulo, autor_id, disponible, precio, categoria_id)
	values
		('100 años de soledad', 3, true, 20000, 4);

-- query para evidenciar el error de nulidad en el campo titulo
insert into libros(autor_id, disponible, precio, categoria_id)
	values
		(3, true, 1000, 4);





