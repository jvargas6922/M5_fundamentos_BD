-- creamos la base de datos llamada prueba.
create database prueba;
-- creamos la tabla empleados
create table empleados(
	id_empleado serial primary key,
	nombre varchar(100) not null,
	salario decimal(10,2)
);

-- agregar un campo nuevo a mi tabla(fecha_ingreso)
alter table empleados add fecha_ingreso date;

-- eliminar una tabla de mi base de datos.
drop table if exists Empleados_backup;

-- crear un indixe
create index idx_salario on empleados (salario)

-- crear un vista 
create view VW_EmpleadosAltosSalarios as 
SELECT nombre, salario
FROM Empleados
WHERE salario > 50000;

-- como consulto la vista
select * from vw_empleadosaltossalarios ve ; 

-- crear la tabla moneda (currencies)
create table currencies(
	id_currency serial primary key,
	currency_name varchar(30) not null,
	currency_symbol char(3),
	created_at timestamp default current_timestamp
);

-- default current_timestamp
insert into currencies (currency_name, currency_symbol)
	values('Dolar', '$');

-- sin default current_timestamp
insert into currencies (currency_name,currency_symbol, created_at)
	values('Dolar', '$', now())
	
-- crear la base de datos liberia
	create database libreria;

-- crear la tabla autores.
create table autores(
	id_autor serial primary key,
	nombre varchar(60) not null,
	apellido varchar(60) not null,
	fecha_nacimiento date,
	nacionalidad varchar(30) not null
);

-- crear 2 registros
insert into autores(nombre, apellido, fecha_nacimiento, nacionalidad)
values
	('Pablo','Neruda', '1904-07-12','Chilena'),
	('Gabriela', 'Mistral','1889-04-07','Chilena');

-- consultar los registros creados
select * from autores a ;

-- crear una tabla llamada libros
create table libros(
	id_libro serial primary key,
	titulo varchar(60) not null,
	autor_id integer,
	ano_publicacion integer,
	disponible boolean default false,
	foreign key (autor_id) references autores(id_autor)
);

-- crear 3 registros para la tabla libros
insert into libros (titulo, autor_id, ano_publicacion, disponible)
	values
		('Canto General', 1, 1950, true),
		('Desolación', 2, 1922, false),
		('Tala', 2, 1938, true);

insert into libros(titulo, autor_id, ano_publicacion, disponible)
	values('Los Versos del Capitan', 1, '1952', true);

-- modificar los atributos de un campo de mi tabla
ALTER TABLE libros 
	ALTER COLUMN ano_publicacion TYPE char(4);


-- revisar si estan los registros creados
select * from libros l;
		


