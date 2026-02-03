Se crea un modelo entidad relacion con respecto a la problematica planteada

en los recursos tiene el modelo entidad relacion en formato PDF.



creacion de las tablas

create table usuarios(
	id_usuario serial primary key,
	nombre_completo varchar(80) not null,
	rut varchar(12) unique not null,
	telefono varchar(30) not null,
	correo varchar(60) unique not null,
	created_at timestamp default current_timestamp,
	updated_at timestamp,
	deleted_at timestamp
);


create table autores(
	id_autor serial primary key,
	nombre_completo varchar(80) not null,
	nacionalidad varchar(30),
	created_at timestamp default current_timestamp,
	updated_at timestamp,
	deleted_at timestamp
);


create table libros(
	id_libro serial primary key,
	autor_id integer,
	ISBN varchar(13) unique not null,
	nombre varchar(50) not null,
	anio date,
	created_at timestamp default current_timestamp,
	updated_at timestamp,
	deleted_at timestamp,
	foreign key(autor_id) references autores(id_autor)
);


create table prestamos(
	id_prestamo serial primary key,
	usuario_id integer,
	libro_id integer,
	fecha date,
	created_at timestamp default current_timestamp,
	updated_at timestamp,
	deleted_at timestamp,
	foreign key (usuario_id) references usuarios(id_usuario),
	foreign key (libro_id) references libros(id_libro)
);
