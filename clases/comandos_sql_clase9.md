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

select * from usuarios u ;
select * from autores a ;
select * from libros l;
select * from prestamos p ;

-- creacion de regitros.

insert into usuarios(nombre_completo, rut, telefono, correo)
	values
		('Oscar Pezoa', '12345678-9','123456789', 'oscar@prueba.com'),
		('Juan Perez', '12345678-8', '123456789', 'juan@prueba.com');

insert into autores(nombre_completo, nacionalidad)
	values
		('Stephen King', 'EEUU'),
		('Isaac Asimob', 'Rusia');

insert into libros(autor_id, ISBN ,nombre,anio)
	values
		(1,'12345678', 'IT', 1986),
		(1, '23456789', 'El resplandor', 1977),
		(2, '34567890', 'Yo Robot', 1950),
		(2, '45678901', 'Fundación', 1951);

insert into prestamos(usuario_id, libro_id, fecha)
	values
		(1, 4, now());

-- quiero ver los datos de la persona y el libro en el prestamo
select 
	p.id_prestamo, 
	u.nombre_completo,
	l.nombre,
	p.fecha
from 
	prestamos p 
	join usuarios u on p.usuario_id = u.id_usuario
	join libros l on p.libro_id = l.id_libro;
