Comandos sql utilizados en la  herramienta PostgreSQL


create table estudiantes(
	id_estudiante serial primary key,
	nombre varchar(100),
	email varchar(100) unique,
	edad integer,
	created_at TIMESTAMP default CURRENT_TIMESTAMP
);