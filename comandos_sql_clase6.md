-- registros de ususrios
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
practica clase 6
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