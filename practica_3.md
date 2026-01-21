[Practica_3]
Con los ejercicios planteados anteriormente llevemos a otro nivel poder indentificar las estructuras de una tabla o esquema para poder solventar negocios o requerimientos.
El siguiente ejercicio tu tarea es poder abordar y guardar los datos de un negocio de venta de completos.
En el cual te permita poder registar las ventas de un producto(Venta) con el flujo completo a un cliente y poder identificar que clientes te compraron productos y la cantidad.

estrutura 
    ingredientes
        id_ingrediente
        nombre_ingrediente
        valor

    productos
        id_producto
        nombre_producto
        valor

    clientes
        id_cliente
        nombre_cliente

    pedidos
        id_pedido
        id_producto
        id_cliente




simulacion


 ingredientes
        id_ingrediente  |   nombre_ingrediente  | valor |
            1           |       palta           |  500  |
            2           |       tomate          |  500  |
            3           |       chucrut         |  500  |
            4           |       vianesa         |   700 |

    productos
        id_producto  |   nombre_producto     |  valor_producto   | 
            1        |   completo dinamico   |      3500         |
            2        |   completo            |      2500         |
            3        |   americano           |      2000         |
            4        |   chacarrero          |      3500         |
            5        |    Italiano           |      3000         | 

    pedidos (Cabecera)
        id_pedido (PK) |  id_producto      |  id_cliente
            1          |        1          |      1
            2          |        5          |      1
            3          |        2          |      1
            4          |        3          |      1

     pedidos (Cabecera)
        id_pedido (PK)  |   id_cliente
            1           |        1
                        |        
                        |        
                        |        
    
    
    Pedidos_detalle
        id_pedido_detalle   | id_pedido FK  | id_producto FK   | cantidad  | ingrediente +    
            1               |   1           |     1            |     1
            2               |   1           |     5            |     3
            3               |   1           |     2            |     2
            4               |   1           |     3            |     4
            5               |   1           |     3            |     1