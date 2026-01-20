Consigna: ✍
Armaremos grupos para avanzar de forma colaborativa en este ejercicio.
Cada grupo deberá crear una tabla de inventario en Google Sheets con 10 artículos que puede
haber en una casa (pueden ser productos de cualquier categoría: tecnología, utensilios de cocina,
libros, etc.).
Luego, deberán identificar y etiquetar los atributos (columnas) de su tabla, como el nombre del
artículo, categoría, precio, cantidad, etc., y reflexionar sobre cuál podría ser la clave primaria de
su tabla. Además, deberán pensar y discutir qué elementos de esa tabla podrían nutrir a una
tabla hija en una base de datos relacional.

leche
pan
galletas
avena
arroz
huevo
azucar
maizena
porotos
lentejas

estructura:
articulos
    id_articulo (Clave primaria[PK])
    nombre_articulo (Cadena de texto)
    valor   (decimal)

tipo_productos
    id_tipo_producto (Clave primaria[PK])
    nombre_tipo_producto (Cadena de texto)

productos
    id_producto (Clave primaria[PK])
    nombre_producto (Cadena de texto)
    tipo_producto_id (Clave foranea[FK])
    descripción (Cadena de texto)


simulación de tabla()
    id_articulo | nombre_articulo | valor
        1           leche         | 1200
        2           pan           | 1000
        3           galletas      | 1000
        4           avena         | 1100
        5           arroz         | 2000
        6           huevo         | 
        7           azucar        | 700
        8           maizena       | 900
        9           porotos       | 800
        10          lenteja       | 1000






