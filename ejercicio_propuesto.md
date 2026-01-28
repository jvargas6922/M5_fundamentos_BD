Modelado de Base de Datos Relacional – Caso Vida Real
🏫 Contexto general

Un instituto educativo necesita desarrollar un sistema para gestionar la información académica de sus alumnos.
El sistema debe permitir registrar personas, cursos y el proceso de inscripción de los alumnos a dichos cursos.

Actualmente, toda la información se maneja en planillas Excel, lo que provoca errores, datos duplicados y dificultad para obtener reportes.

🎯 Objetivo del ejercicio

Diseñar un modelo de datos relacional y crear las tablas necesarias en una base de datos, considerando:

- Integridad de los datos
- Relaciones entre entidades
- Reglas del negocio
- Posibilidad de realizar consultas reales

🧠 Descripción del problema

El instituto necesita almacenar la siguiente información:

👩‍🎓 Alumnos

- Cada alumno debe tener un identificador único
Se debe registrar:
- Nombre completo
- Correo electrónico
- Fecha de nacimiento
- Los alumnos no pueden compartir el mismo correo electrónico

👨‍🏫 Profesores

- Cada profesor debe tener un identificador único

Se debe registrar:

Nombre completo

Especialidad o área de conocimiento

Un profesor puede dictar uno o varios cursos

📚 Cursos

Cada curso debe tener un identificador único

Se debe registrar:

Nombre del curso

Fecha de inicio

Fecha de término

Cada curso es dictado por un solo profesor

📝 Inscripciones

Los alumnos pueden inscribirse en uno o varios cursos

Un curso puede tener muchos alumnos inscritos

Se debe registrar:

Fecha de inscripción

Un alumno no puede inscribirse más de una vez al mismo curso

📌 Reglas importantes del negocio

Un alumno puede estar inscrito en varios cursos.

Un curso puede tener varios alumnos inscritos.

Un profesor puede dictar varios cursos.

Cada curso tiene un solo profesor asignado.

No se permiten inscripciones duplicadas.

No deben existir cursos sin profesor asignado.

🛠️ Actividades a realizar por los estudiantes

Identificar las entidades del sistema.

Definir los atributos de cada entidad.

Determinar las relaciones entre las entidades.

Identificar las claves primarias y claves foráneas.

Diseñar el modelo relacional.

Crear las tablas SQL con sus respectivos campos y restricciones.

Insertar datos de prueba.

Realizar consultas que permitan:

Ver alumnos inscritos en cursos

Ver cursos con su profesor

Listar alumnos de un curso específico

🧩 Preguntas guía (para discusión en clase)

¿Qué entidades detectas en el problema?

¿Existe alguna relación muchos a muchos? ¿Cómo la resolverías?

¿Qué campos deberían ser únicos?

¿Qué reglas del negocio deben reflejarse en la base de datos?

¿Qué pasaría si no existiera una tabla de inscripciones?