-- obtener el registro del cliente con id = 2
select 
	*  
from 
	clientes c 
where 
	c.id_cliente = 2;

-- obtener los pedidos donde el cliente sea el id = 2
select 
	* 
from 
	pedidos p 
where 
	p.cliente_id = 2;

-- obtener todos los registros de clientes
select * from clientes c ;
-- obtener todos los registros de pedidos_detalle
select * from pedidos_detalle pd ;
-- obtener todos los registros de productos
select * from productos p ;
-- obtener todos los registros de ingredientes
select * from ingredientes i ;
-- obtener todos los registros de pedidos
select * from pedidos p;


-- insert clientes
insert into clientes(nombre_cliente) values('Alejandro');
insert into clientes(nombre_cliente) values('Cristobal');

-- insert pedidos
insert into pedidos(cliente_id) values(6);
insert into pedidos(cliente_id) values(3);
insert into pedidos(cliente_id) values(4);
insert into pedidos(cliente_id) values(7);

-- insert pedidos_detalle
insert into pedidos_detalle(pedido_id, producto_id, cantidad, ingrediente_id)
	values
		(3, 5, 2, 1),
		(3, 1, 2, 2);

insert into pedidos_detalle (pedido_id,producto_id, cantidad, ingrediente_id)
	values
		(4, 6, 1, 5);

insert into pedidos_detalle (pedido_id, producto_id, cantidad, ingrediente_id)
	values
		(5, 4, 1, 1),
		(5, 6, 1, 5);

insert into pedidos_detalle (pedido_id, producto_id, cantidad, ingrediente_id)
	values
		(6, 7, 1, 1),
		(6, 5, 1, 1),
		(6, 6, 1, 5);
		

-- insert producto
insert into productos(nombre_producto, valor) values('cocacola',1000);
insert into productos(nombre_producto, valor) values('papas fritas', 1500);

-- insert ingredientes
insert into ingredientes (nombre_ingrediente, valor) values('Agrandar', 200);



			




