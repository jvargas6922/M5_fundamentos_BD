-- registros de usuarios
select * from users u;
-- registros de transacciones
select * from transactions t ;
-- registros de monedas
select * from currencies c ;

-- crear 5 registros en la tabla transacciones < 50
insert into transactions 
	(sender_user_id, receiver_user_id, amount, transaction_date)
values
	(1, 2, 40, now()),
	(1, 2, 30, now()),
	(2, 3, 10, now()),
	(2, 1, 11, now()),
	(3, 1, 15, now());

-- 15% => 0.15
-- prueba de condicion where antes de actualizar
select * from transactions t where t.amount < 50;


update transactions 
	set amount = amount * 1.15
where amount < 50;

--------------------------------
-- crear una base de dato llamada empresa.
-- crear un tabla llamada usuarios
	/*
	  id_usuario
	  nombre
	  apellido
	  rut
	  correo
	 */
-- crear una tabla llamada empleados
	/*
	 * id_empleado
	 * nombre
	 * apellido
	 * salario
	 * fecha_ingreso
	 * departamento => departamento_id
	 * */
	
-- crear una tabla llamada departamentos
/*id_departamento
 * nombre
 * descripcion
 * */

CREATE TABLE usuarios(
	id_usuario SERIAL PRIMARY KEY,
	nombre VARCHAR(60) NOT NULL,
	apellido VARCHAR(60) NOT NULL,
	rut VARCHAR(12) UNIQUE NOT NULL,
	correo VARCHAR(60) UNIQUE NOT NULL
);

CREATE TABLE departamentos(
	id_departamento SERIAL PRIMARY KEY,
	nombre VARCHAR(50) NOT NULL,
	descripcion VARCHAR(60) NOT NULL
);

CREATE TABLE empleados(
	id_empleado SERIAL PRIMARY KEY,
	nombre VARCHAR(60) NOT NULL,
	apellido VARCHAR(60) NOT null,
	salario DECIMAL(10,2),
	departamento_id INTEGER,
	fecha_ingreso TIMESTAMP,
	FOREIGN KEY(departamento_id) REFERENCES departamentos(id_departamento)
);

select * from usuarios u ;
select * from departamentos d ;
select * from empleados e ;

select 
	-- e.*,
	e.nombre,
	e.apellido,
	e.salario,
	d.nombre,
	d.descripcion 
from 
	empleados e
	join departamentos d 
		on e.departamento_id = d.id_departamento 
	; 

-- crear 3 registros para las tablas usuarios, empleados y departamentos
insert into usuarios(nombre, apellido, rut, correo)
	values
		('Joffred', 'Vargas', '1111111-2', 'vargasj@prueba.com'),
		('Natacha', 'Vargas', '1111111-3', 'vargasn@prueba.com'),
		('Jonathan', 'Vargas', '1111111-4', 'vargasjj@prueba.com');

insert into departamentos (nombre, descripcion)
	values
		('TI', 'Gente Buena'),
		('Contabilidad', 'Los Pagan'),
		('RRHH', 'Los Lomo Liso');

insert into empleados
	(nombre, apellido, salario, departamento_id, fecha_ingreso)
	values
		('Ivan','Zamorano', 500000, 3, now()),
		('Oscar','Pezoa', 1200000, 1, now()),
		('Jeff','Bezos', 1500000 , 2, now());

update empleados
 set salario = salario * 2
 where departamento_id = 1;

begin;
delete from usuarios
	where id_usuario = 3;
rollback ;



