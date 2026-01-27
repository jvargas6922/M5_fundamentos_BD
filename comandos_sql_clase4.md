-- PPT3

-- obtener todos los registros de clientes
select * from clientes c ;
select * from clientes c order by c.id_cliente asc;
-- obtener todos los registros de pedidos_detalle
select * from pedidos_detalle pd ;
-- obtener todos los registros de productos
select * from productos p ;
-- obtener todos los registros de ingredientes
select * from ingredientes i ;
-- obtener todos los registros de pedidos
select * from pedidos p;

-- insert a una tabla
insert into clientes (nombre_cliente) values('Natacha');
insert into clientes (nombre_cliente) values('PPPPPPPPPP');

-- update a un registro
update clientes
	set nombre_cliente = 'joffred'
	where id_cliente = 1;

-- delete a un registro
delete from clientes where id_cliente = 10 ;



-- Formas de utilizar el where

-- igual simple
select * from productos p where p.id_producto = 5;

-- comparación
select * from productos p where p.valor < 2000;

-- comparacion de fechas se va a ocupar los regitros del dataset (dataset)
select * from data;

-- timestamp => año-mes-dia 00:00:00

-- uso del between para comprar rangos de fechas
select * from data d where d.invoicedate between '12/2/2010 00:00' and '12/3/2010 00:00'; 

-- and / or (1 o muchas condiciones)
select 
	* 
from 
	data d 
where 
	d.invoicedate 
	between 
		'12/2/2010 00:00' and '12/3/2010 00:00'
and 
	d.unitprice = 4.25
and
	d.quantity = 24
and 
	d.stockcode = '79321';

-- uso del like
select * from data d where d.description like '%WHITE METAL%';

-- uso del select en las consultas
select * from ingredientes i;

-- select seleccionando los campos de mi tabla
select 
	i.nombre_ingrediente,
	i.valor 
from 
	ingredientes i;

-- select seleccionado los campos con alias
select 
	i.nombre_ingrediente as ingrediente,
	i.valor as precio
from 
	ingredientes i;

-- select con join
select 
	p.id_pedido,
	c.nombre_cliente as cliente,
	p2.nombre_producto as completo,
	p2.valor as precio 
from 
	pedidos p
	join pedidos_detalle pd 
		on p.id_pedido = pd.pedido_id
	join productos p2 
		on pd.producto_id = p2.id_producto
	join clientes c 
		on p.cliente_id = c.id_cliente;  

-- consultas con la base de datos pokemon
select * from pokemon;

select * from pokemon p where p.nombre like '%Zubat%'; 

select * from pokemon p where p.nombre like '%Pidgey%'; -- 16

select * from pokemon p where p.nombre like '%Caperpie%'; -- 10

select * from pokemon p where p.numero_pokedex >= 10 and p.numero_pokedex <= 16;

-- ultimo registro de la tabla
select 
	* 
from 
	pokemon p 
order by 
	p.numero_pokedex desc limit 1;
