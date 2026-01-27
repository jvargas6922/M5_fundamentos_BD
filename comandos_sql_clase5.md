Agregar nuevos usuarios utilizando INSERT:
En este espacio vamos a mostrar cómo agregar nuevos usuarios en una una tabla llamada "Usuarios".
No obstante antes de comenzar, debemos crear una conexión a una base de datos llamada “Alke Wallet”.

1)Crear 3 tablas llamadas
    - Usuarios
    - Transacciones
    - Monedas

2)Estructura de la tabla Usuarios:
    id_user (clave primaria)
    nombre
    correo electrónico
    contraseña
    saldo.
    fecha de creación

3)Estructura de la tabla Transacciones:
    id_transaction (Primary Key)
    sender_user_id (Foreign Key referenciando a User)
    receiver_user_id (Foreign Key referenciando a User)
    valor
    transaction_date.

4)Estructura de la tabla Monedas:
    id_currency (Primary Key)
    currency_name
    currency_symbol

5)Forma correcta que deberia tener las tablas:
- OPCIONAL
    Users (Tabla Usuarios)
        id_user
        name
        email
        password
        balance
        created_at
    
    Transactions (Tabla Transacciones)
        id_transaction
        sender_user_id
        receiver_user_id
        amount
        transaction_date

    Currencies (Tabla Monedas)
        id_currency
        currency_name
        currency_symbol

6)SQL para la creacion de las tablas:
Nota la base de datos se debe llamar Alke Wallet
Sentencias SQL para la creacion de las tablas

create table User(
    id_user serial primary key,
    name varchar(100),
    email varchar(100),
    password varchar(100),
    balance decimal(10,2),
    created_at datetime
);

create table Transactions(
    id_transaction serial primary key,
    sender_user_id int references User(id_user),
    receiver_user_id int references User(id_user),
    amount decimal(10,2),
    transaction_date datetime
);

create table Currencies(
    id_currency serial primary key,
    currency_name varchar(100),
    currency_symbol varchar(10)
);

7)Insertar al menos 3 usuarios y 3 transacciones.
8)Consultar usuarios creados

-- comandos utilizados en Dbeaver
-- creacion de la base de datos Alke Wallet

-- creacion de las tablas Users, Transaction, Currencies

/*
create table Users(
    id_user serial primary key,
    name varchar(100) not null,
    email varchar(100) unique not null ,
    password varchar(100)not null,
    balance decimal(10,2),
    created_at timestamp
);
*/

/*
create table Transactions(
    id_transaction serial primary key,
    sender_user_id int,
    receiver_user_id int ,
    amount decimal(10,2),
    transaction_date timestamp,
    foreign key(sender_user_id) references Users(id_user),
    foreign key (receiver_user_id) references Users (id_user)
);
*/

/*
create table Currencies(
    id_currency serial primary key,
    currency_name varchar(100) not null,
    currency_symbol varchar(10) not null
);
*/

-- consultas de usuarios
select * from users;

-- consultas de transacciones
select * from transactions t;

-- consulta de monedas
select * from currencies c;

-- insertar a lo menos 3 usuarios y 3 transacciones

-- insert users
insert into users(name, email, password, balance, created_at)
	values
		('Joffred', 'vargas@prueba.com', '123456789', '0', now()),
		('Natacha', 'vargasN@prueba.com', '12345678', '500', now()),
		('Jonathan', 'vargasj@prueba.com', '123456777', '5000', now());

-- insert transaction
insert into transactions (sender_user_id, receiver_user_id, amount, transaction_date)
	values
		(2, 1, 100, now()),
		(3, 1, 200, now()),
		(1, 2, 50, now());

-- insert currencies
insert into currencies(currency_name,currency_symbol)
	values
		('Rial', '**R'),
		('Dolar', '$'),
		('Peso Chileno', 'CLP');

