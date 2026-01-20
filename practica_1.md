¿En qué consistirá la Demo?
Esta demostración en vivo es solo un primer vistazo a lo que es una base de datos real. Hoy no vamos a
profundizar en cómo construirla ni en los detalles técnicos. Lo que veremos es cómo se organiza la
información y qué elementos componen una base de datos relacional.
En las próximas clases, iremos adentrándonos más en la construcción y gestión de bases de datos, pero
por ahora, lo que buscamos es familiarizarnos con su estructura básica.
¿Alguna vez pensaron en ordenar su lista de contactos incluyendo diferentes datos para identificar
quién es la persona? Por ejemplo, ¿quién es el dueño de ese correo? ¿Cuál es su número de teléfono?
¿En qué grupo lo incluirían? Estos datos nos ayudarán a organizar nuestra información de manera más
eficiente.

Con respecto al enunciado construiremos las tablas.

Esquema:

personas:
    id_persona  (clave primaria) PK
    nombre      (cadena de string)
    apellido    (cadena de string)
    fecha_nac   (fecha)

mediosContacto
    id_medio       (clave primaria) PK
    persona_id     (clave foranea) FK
    tipo_medio_id  (clave foranea) FK
    valor          (cadena de string)

tipoMedios
    id_tipo_medio     (clave primaria) PK
    tipo_medio_nombre (cadena de string)

grupos
    id_grupo        (clave primaria) PK
    nombre_grupo    (cadena de string)

personasGrupos
    id_grupo_persona (clave primaria)
    persona_id       (clave foranea)
    grupo_id         (clave foranea)


Valores o simulación
mediosContacto
    id_medio | persona_id   |   tipo    |    valor
        1           1           email
        2           2           móvil
        3           3           Email
        4           4           Movil
        N           N           EMAIL
                                MOVIL
                                correo
                                
