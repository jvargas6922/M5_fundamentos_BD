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

