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
    - Nombre completo
    - Especialidad o área de conocimiento
    - Un profesor puede dictar uno o varios cursos

📚 Cursos
- Cada curso debe tener un identificador único
    Se debe registrar:
    - Nombre del curso
    - Fecha de inicio
    - Fecha de término
    - Cada curso es dictado por un solo profesor

📝 Inscripciones
Los alumnos pueden inscribirse en uno o varios cursos
- Un curso puede tener muchos alumnos inscritos
    Se debe registrar:
    - Fecha de inscripción
    - Un alumno no puede inscribirse más de una vez al mismo curso

📌 Reglas importantes del negocio
- Un alumno puede estar inscrito en varios cursos.
- Un curso puede tener varios alumnos inscritos.
- Un profesor puede dictar varios cursos.
- Cada curso tiene un solo profesor asignado.
- No se permiten inscripciones duplicadas.
- No deben existir cursos sin profesor asignado.

🛠️ Actividades a realizar por los estudiantes
- Identificar las entidades del sistema.
- Definir los atributos de cada entidad.
- Determinar las relaciones entre las entidades.
- Identificar las claves primarias y claves foráneas.
- Diseñar el modelo relacional.
- Crear las tablas SQL con sus respectivos campos y restricciones.
- Insertar datos de prueba.
- Realizar consultas que permitan:
- Ver alumnos inscritos en cursos
- Ver cursos con su profesor
- Listar alumnos de un curso específico

🧩 Preguntas:

¿Qué entidades detectas en el problema?
¿Existe alguna relación muchos a muchos? ¿Cómo la resolverías?
¿Qué campos deberían ser únicos?
¿Qué reglas del negocio deben reflejarse en la base de datos?
¿Qué pasaría si no existiera una tabla de inscripciones?

Desarrollo de ejercicio propuesto

-- crear base de datos para trabajar instituto

-- creacion de tablas.
/*
 	students 	=> estudiantes
 	teachers 	=> profesores
 	courses 	=> cursos
 	enrollments => inscripciones
 */

create table students(
 	id_student serial primary key,
 	full_name varchar(100) not null,
 	email varchar(60) not null unique,
 	birth_date date,
 	created_at timestamp default current_timestamp
);

create table teachers(
	id_teacher serial primary key,
	full_name varchar(100) not null,
	specialty varchar(100) not null,
	created_at timestamp default current_timestamp
);

create table courses(
	id_course serial primary key,
	course_name varchar(100) not null,
	teacher_id integer,
	star_date date,
	end_date date,
	created_at timestamp default current_timestamp,
	foreign key (teacher_id) references teachers(id_teacher)
);

create table enrollments(
	id_enrollment serial primary key,
	studen_id integer,
	course_id integer,
	enrollment_date date default current_date,
	create_at timestamp default current_timestamp,
	foreign key (studen_id) references students(id_student),
	foreign key (course_id) references courses(id_course),
	unique(studen_id, course_id),
	created_at timestamp default current_timestamp
);

-- insert students
	insert into students (full_name, email, birth_date)
		values
			('Ana Torres', 'ana.torres@mail.com', '2000-05-14'),
			('Carlos Pérez', 'carlos.perez@mail.com', '1999-09-22'),
			('María López', 'maria.lopez@mail.com', '2001-02-10');

-- insert teachers
	insert into teachers (full_name, specialty)
		values
			('Juan González', 'Base de Datos'),
			('Laura Martínez', 'Programación');

-- insert courses
	insert into courses (course_name, teacher_id, star_date, end_date)
		values
			('Introducción a SQL', 1, '2026-03-01', '2026-06-30'),
			('Programación en Python', 2, '2026-03-01', '2026-06-30');

-- insert enrollments
	insert into enrollments(studen_id, course_id)
		values
			(1, 1),
			(1, 2),
			(2, 1),
			(3, 2);

-- Alumnos inscritos en cursos.
select 
	s.full_name,
	c.course_name 
from 
	enrollments e
	join students s on e.studen_id = s.id_student
	join courses c  on e.course_id = c.id_course; 

-- Cursos con su profesor
select 
	c.course_name,
	t.full_name
from 
	courses c
	join teachers t on c.teacher_id = t.id_teacher;

-- alumnos en un curso en especifico
select 
	s.full_name
from 
	enrollments e
	join students s on e.studen_id = s.id_student
where
	e.course_id = 1;