# PROYECTO-BASES1
## Carga de Datos a tabla temporal
```
OPTIONS (SKIP=1)
LOAD DATA INFILE 'C:\Users\jared\documents\BlockbusterData.csv'
INTO TABLE PROYECTO.temporal FIELDS TERMINATED BY ';' 
OPTIONALLY ENCLOSED BY '"'
(
    NOMBRE_CLIENTE, CORREO_CLIENTE, CLIENTE_ACTIVO, FECHA_CREACION, TIENDA_PREFERIDA, 
    DIRECCION_CLIENTE, CODIGO_POSTAL_CLIENTE, CIUDAD_CLIENTE, PAIS_CLIENTE,
    FECHA_RENTA, FECHA_RETORNO, MONTO_A_PAGAR, FECHA_PAGO, NOMBRE_EMPLEADO,
    CORREO_EMPLEADO, EMPLEADO_ACTIVO, TIENDA_EMPLEADO, USUARIO_EMPLEADO, CONTRASENIA_EMPLEADO,
    DIRECCION_EMPLEADO, CODIGO_POSTAL_EMPLEADO, CIUDAD_EMPLEADO, PAIS_EMPLEADO, NOMBRE_TIENDA,
    ENCARGADO_TIENDA, DIRECCION_TIENDA, CODIGO_POSTAL_TIENDA, CIUDAD_TIENDA, PAIS_TIENDA, TIENDA_PELICULA, NOMBRE_PELICULA,
    DESCRIPCION_PELICULA, ANIO_LANZAMIENTO, DIAS_RENTA, COSTO_RENTA, DURACION,
    COSTO_POR_DANIO, CLASIFICACION, LENGUAJE_PELICULA, CATEGORIA_PELICULA, ACTOR_PELICULA
)
```
## Creacion de Tablas
```
CREATE TABLE Temporal(
    NOMBRE_CLIENTE VARCHAR2(256),
    CORREO_CLIENTE VARCHAR2(256),
    CLIENTE_ACTIVO VARCHAR2(256),
    FECHA_CREACION VARCHAR2(256),
    TIENDA_PREFERIDA VARCHAR2(256),
    DIRECCION_CLIENTE VARCHAR2(256),
    CODIGO_POSTAL_CLIENTE VARCHAR2(256),
    CIUDAD_CLIENTE VARCHAR2(256),
    PAIS_CLIENTE VARCHAR2(256),
    FECHA_RENTA VARCHAR2(256),
    FECHA_RETORNO VARCHAR2(256),
    MONTO_A_PAGAR VARCHAR2(256),
    FECHA_PAGO VARCHAR2(256),
    NOMBRE_EMPLEADO VARCHAR2(256),
    CORREO_EMPLEADO VARCHAR2(256),
    EMPLEADO_ACTIVO VARCHAR2(256),
    TIENDA_EMPLEADO VARCHAR2(256),
    USUARIO_EMPLEADO VARCHAR2(256),
    CONTRASENIA_EMPLEADO VARCHAR2(256),
    DIRECCION_EMPLEADO VARCHAR2(256),
    CODIGO_POSTAL_EMPLEADO VARCHAR2(256),
    CIUDAD_EMPLEADO VARCHAR2(256),
    PAIS_EMPLEADO VARCHAR2(256),
    NOMBRE_TIENDA VARCHAR2(256),
    ENCARGADO_TIENDA VARCHAR2(256),
    DIRECCION_TIENDA VARCHAR2(256),
    CODIGO_POSTAL_TIENDA VARCHAR2(256),
    CIUDAD_TIENDA VARCHAR2(256),
    PAIS_TIENDA VARCHAR2(256),
    TIENDA_PELICULA VARCHAR2(256),
    NOMBRE_PELICULA VARCHAR2(256),
    DESCRIPCION_PELICULA VARCHAR2(256),
    ANIO_LANZAMIENTO VARCHAR2(256),
    DIAS_RENTA VARCHAR2(256),
    COSTO_RENTA VARCHAR2(256),
    DURACION VARCHAR2(256),
    COSTO_POR_DANIO VARCHAR2(256),
    CLASIFICACION VARCHAR2(256),
    LENGUAJE_PELICULA VARCHAR2(256),
    CATEGORIA_PELICULA VARCHAR2(256),
    ACTOR_PELICULA VARCHAR2(256)
);

CREATE TABLE Pais(
    id NUMBER GENERATED ALWAYS AS IDENTITY(START WITH 1 INCREMENT BY 1),
    NOMBRE VARCHAR2(256),
    PRIMARY KEY(id)
);
CREATE TABLE Duracion(
    id NUMBER GENERATED ALWAYS AS IDENTITY(START WITH 1 INCREMENT BY 1),
    DURACION VARCHAR2(256) NOT NULL,
    PRIMARY KEY(id)
);
CREATE TABLE Costo(
    id NUMBER GENERATED ALWAYS AS IDENTITY(START WITH 1 INCREMENT BY 1),
    COSTO VARCHAR2(256) NOT NULL,
    PRIMARY KEY(id)
);
CREATE TABLE Actor(
    id NUMBER GENERATED ALWAYS AS IDENTITY(START WITH 1 INCREMENT BY 1),
    NOMBRE VARCHAR2(256) NOT NULL,
    APELLIDO VARCHAR2(256) NOT NULL,
    PRIMARY KEY(id)
);
CREATE TABLE Categoria(
    id NUMBER GENERATED ALWAYS AS IDENTITY(START WITH 1 INCREMENT BY 1),
    CATEGORIA VARCHAR2(256) NOT NULL,
    PRIMARY KEY(id)
);
CREATE TABLE Lenguaje(
    id NUMBER GENERATED ALWAYS AS IDENTITY(START WITH 1 INCREMENT BY 1),
    LENGUAJE VARCHAR2(256) NOT NULL,
    PRIMARY KEY(id)
);
CREATE TABLE Clasificacion(
    id NUMBER GENERATED ALWAYS AS IDENTITY(START WITH 1 INCREMENT BY 1),
    CLASIFICACION VARCHAR2(256) NOT NULL,
    PRIMARY KEY(id)
);
CREATE TABLE CodigoPostal(
    id NUMBER GENERATED ALWAYS AS IDENTITY(START WITH 1 INCREMENT BY 1),
    CODIGO_POSTAL VARCHAR2(256) NOT NULL,
    PRIMARY KEY(id)
);
CREATE TABLE Ciudad(
    id NUMBER GENERATED ALWAYS AS IDENTITY(START WITH 1 INCREMENT BY 1),
    CIUDAD VARCHAR2(256) NOT NULL,
    PAIS INT NOT NULL,
    PRIMARY KEY(id),
    CONSTRAINT fk_ciudad_pais FOREIGN KEY (PAIS) REFERENCES Pais(id)
);
CREATE TABLE Fecha(
    id NUMBER GENERATED ALWAYS AS IDENTITY(START WITH 1 INCREMENT BY 1),
    FECHA VARCHAR2(256),
    PRIMARY KEY(id)
);
CREATE TABLE Lanzamiento(
    id NUMBER GENERATED ALWAYS AS IDENTITY(START WITH 1 INCREMENT BY 1),
    LANZAMIENTO VARCHAR2(256),
    PRIMARY KEY(id)
);
CREATE TABLE Tienda(
    id NUMBER GENERATED ALWAYS AS IDENTITY(START WITH 1 INCREMENT BY 1),
    NOMBRE_TIENDA VARCHAR2(256),
    DIRECCION_TIENDA VARCHAR2(256),
    CODIGO_POSTAL_TIENDA INT NOT NULL,
    CIUDAD_TIENDA INT NOT NULL,
    PAIS_TIENDA INT NOT NULL,
    PRIMARY KEY(id),
    CONSTRAINT fk_codigo_tienda FOREIGN KEY (CODIGO_POSTAL_TIENDA) REFERENCES CodigoPostal(id),
    CONSTRAINT fk_ciudad_tienda FOREIGN KEY (CIUDAD_TIENDA) REFERENCES Ciudad(id),
    CONSTRAINT fk_pais_tienda FOREIGN KEY (PAIS_TIENDA) REFERENCES Pais(id)
);
CREATE TABLE Pelicula(
    id NUMBER GENERATED ALWAYS AS IDENTITY(START WITH 1 INCREMENT BY 1),
    NOMBRE_PELICULA VARCHAR2(256),
    DESCRIPCION_PELICULA VARCHAR2(256),
    ANIO_LANZAMIENTO INT NOT NULL,
    CLASIFICACION INT NOT NULL,
    LENGUAJE INT NOT NULL,
    CATEGORIA INT NOT NULL,
    DURACION INT NOT NULL,
    COSTO_RENTA VARCHAR2(256),
    COSTO_POR_DANIO VARCHAR2(256),
    PRIMARY KEY(id),
    CONSTRAINT fk_anio_detallepelicula FOREIGN KEY (ANIO_LANZAMIENTO) REFERENCES Lanzamiento(id),
    CONSTRAINT fk_clasificacion_detallepelicula FOREIGN KEY (CLASIFICACION) REFERENCES Clasificacion(id),
    CONSTRAINT fk_lenguaje_detallepelicula FOREIGN KEY (LENGUAJE) REFERENCES Lenguaje(id),
    CONSTRAINT fk_categoria_detallepelicula FOREIGN KEY (CATEGORIA) REFERENCES Categoria(id),
    CONSTRAINT fk_duracion_detallepelicula FOREIGN KEY (DURACION) REFERENCES Duracion(id)
);
CREATE TABLE Inventario(
    id NUMBER GENERATED ALWAYS AS IDENTITY(START WITH 1 INCREMENT BY 1),
    CODIGO_TIENDA INT NOT NULL,
    CODIGO_PELICULA INT NOT NULL,
    PRIMARY KEY(id),
    CONSTRAINT fk_tienda_inventario FOREIGN KEY (CODIGO_TIENDA) REFERENCES Tienda(id),
    CONSTRAINT fk_pelicula_inventario FOREIGN KEY (CODIGO_PELICULA) REFERENCES Pelicula(id)
);
CREATE TABLE DetallePelicula(
    id NUMBER GENERATED ALWAYS AS IDENTITY(START WITH 1 INCREMENT BY 1),
    CODIGO_PELICULA INT NOT NULL,
    ACTOR INT NOT NULL,
    PRIMARY KEY(id),
    CONSTRAINT fk_pelicula_detallepelicula FOREIGN KEY (CODIGO_PELICULA) REFERENCES Pelicula(id),
    CONSTRAINT fk_actor_detallepelicula FOREIGN KEY (ACTOR) REFERENCES Actor(id)
);
CREATE TABLE Cliente(
    id NUMBER GENERATED ALWAYS AS IDENTITY(START WITH 1 INCREMENT BY 1),
    NOMBRE VARCHAR2(256),
    APELLIDO VARCHAR(256),
    CORREO_CLIENTE VARCHAR2(256),
    CLIENTE_ACTIVO VARCHAR(256),
    DIRECCION_CLIENTE VARCHAR2(256),
    FECHA_CREACION INT NOT NULL,
    CODIGO_POSTAL_CLIENTE INT NOT NULL,
    CIUDAD_CLIENTE INT NOT NULL,
    PRIMARY KEY(id),
    CONSTRAINT fk_fecha_cliente FOREIGN KEY (FECHA_CREACION) REFERENCES Fecha(id),
    CONSTRAINT fk_codigo_cliente FOREIGN KEY (CODIGO_POSTAL_CLIENTE) REFERENCES CodigoPostal(id),
    CONSTRAINT fk_ciudad_cliente FOREIGN KEY (CIUDAD_CLIENTE) REFERENCES Ciudad(id)
);
CREATE TABLE ClientePais(
    id NUMBER GENERATED ALWAYS AS IDENTITY(START WITH 1 INCREMENT BY 1),
    CLIENTE INT NOT NULL,
    PAIS INT NOT NULL,
    PRIMARY KEY(id),
    CONSTRAINT fk_cliente FOREIGN KEY (CLIENTE) REFERENCES Cliente(id),
    CONSTRAINT fk_pais FOREIGN KEY (PAIS) REFERENCES Pais(id)
);
CREATE TABLE Empleado(
    id NUMBER GENERATED ALWAYS AS IDENTITY(START WITH 1 INCREMENT BY 1),
    NOMBRE_EMPLEADO VARCHAR2(256),
    CORREO_EMPLEADO VARCHAR2(256),
    EMPLEADO_ACTIVO VARCHAR2(256),
    TIENDA_EMPLEADO INT NOT NULL,
    USUARIO_EMPLEADO VARCHAR2(256),
    CONTRASENIA_EMPLEADO VARCHAR(256),
    CODIGO_POSTAL_EMPLEADO INT NOT NULL,
    DIRECCION_EMPLEADO VARCHAR(256),
    PRIMARY KEY(id),
    CONSTRAINT fk_tienda_empleado FOREIGN KEY (TIENDA_EMPLEADO) REFERENCES Tienda(id),
    CONSTRAINT fk_codigo_empleado FOREIGN KEY (CODIGO_POSTAL_EMPLEADO) REFERENCES CodigoPostal(id)
);
CREATE TABLE Renta(
    id NUMBER GENERATED ALWAYS AS IDENTITY(START WITH 1 INCREMENT BY 1),
    FECHA_RENTA INT NOT NULL,
    FECHA_RETORNO INT NOT NULL,
    MONTO_A_PAGAR VARCHAR2(256),
    FECHA_PAGO INT NOT NULL,
    DIAS_RENTA INT,
    PELICULA INT NOT NULL,
    TIENDA INT NOT NULL,
    EMPLEADO INT NOT NULL,
    CLIENTE INT NOT NULL,
    PRIMARY KEY(id),
    CONSTRAINT fk_fechaRenta_renta FOREIGN KEY (FECHA_RENTA) REFERENCES Fecha(id),
    CONSTRAINT fk_fechaRetorno_renta FOREIGN KEY (FECHA_RETORNO) REFERENCES Fecha(id),
    CONSTRAINT fk_fechaPago_renta FOREIGN KEY (FECHA_PAGO) REFERENCES Fecha(id),
    CONSTRAINT fk_pelicula_renta FOREIGN KEY (PELICULA) REFERENCES Pelicula(id),
    CONSTRAINT fk_tienda_renta FOREIGN KEY (TIENDA) REFERENCES Tienda(id),
    CONSTRAINT fk_empleado_renta FOREIGN KEY (EMPLEADO) REFERENCES Empleado(id),
    CONSTRAINT fk_cliente_renta FOREIGN KEY (CLIENTE) REFERENCES Cliente(id)
);
```
## Carga de Datos al modelo
```
INSERT INTO Pais(nombre) SELECT DISTINCT PAIS_CLIENTE FROM Temporal;

INSERT INTO Duracion(DURACION) SELECT DISTINCT DURACION FROM Temporal;

INSERT INTO Costo(COSTO) (SELECT DISTINCT COSTO_RENTA FROM Temporal UNION SELECT DISTINCT COSTO_POR_DANIO FROM Temporal);

INSERT INTO ACTOR(nombre, apellido)
    SELECT DISTINCT REGEXP_SUBSTR(cadena, '[^ ]+'), SUBSTR(REGEXP_SUBSTR(cadena, '(? ).*'), 0, LENGTH(REGEXP_SUBSTR(cadena, '(? ).*')) - 1) FROM 
                (
                    SELECT Temporal.ACTOR_PELICULA AS cadena FROM Temporal WHERE ACTOR_PELICULA != '-'
                )
    WHERE REGEXP_SUBSTR(cadena, '[^ ]+') != '-,'
    ;

INSERT INTO Categoria(CATEGORIA) SELECT DISTINCT CATEGORIA_PELICULA FROM Temporal;

INSERT INTO Lenguaje(LENGUAJE) SELECT DISTINCT LENGUAJE_PELICULA FROM Temporal;

INSERT INTO Clasificacion(CLASIFICACION) SELECT DISTINCT CLASIFICACION FROM Temporal;

INSERT INTO CodigoPostal(CODIGO_POSTAL) SELECT DISTINCT CODIGO_POSTAL_TIENDA FROM Temporal
    UNION SELECT DISTINCT CODIGO_POSTAL_CLIENTE FROM Temporal
    UNION SELECT DISTINCT CODIGO_POSTAL_EMPLEADO FROM Temporal;

INSERT INTO Ciudad(CIUDAD, PAIS)
    (SELECT DISTINCT Temporal.CIUDAD_CLIENTE, Pais.id FROM Temporal
        INNER JOIN Pais ON Temporal.PAIS_CLIENTE = Pais.NOMBRE)
    UNION
    (SELECT DISTINCT Temporal.CIUDAD_TIENDA, Pais.id FROM Temporal
        INNER JOIN Pais ON Temporal.PAIS_TIENDA = Pais.NOMBRE)
    UNION
    (SELECT DISTINCT Temporal.CIUDAD_EMPLEADO, Pais.id FROM Temporal
        INNER JOIN Pais ON Temporal.PAIS_EMPLEADO = Pais.NOMBRE);

INSERT INTO Fecha(FECHA) SELECT DISTINCT FECHA_PAGO FROM Temporal
    UNION SELECT DISTINCT FECHA_RETORNO FROM Temporal
    UNION SELECT DISTINCT FECHA_CREACION FROM Temporal
    UNION SELECT DISTINCT FECHA_RENTA FROM Temporal;

INSERT INTO Lanzamiento(LANZAMIENTO) SELECT DISTINCT ANIO_LANZAMIENTO FROM Temporal;

INSERT INTO Tienda(NOMBRE_TIENDA, DIRECCION_TIENDA, CODIGO_POSTAL_TIENDA, CIUDAD_TIENDA, PAIS_TIENDA)
    SELECT DISTINCT Temporal.NOMBRE_TIENDA, Temporal.DIRECCION_TIENDA, CodigoPostal.id, Ciudad.id, Pais.id
    FROM Temporal
    INNER JOIN CodigoPostal ON Temporal.CODIGO_POSTAL_TIENDA = CodigoPostal.CODIGO_POSTAL
    INNER JOIN Ciudad ON Temporal.CIUDAD_TIENDA = Ciudad.CIUDAD
    INNER JOIN Pais ON Temporal.PAIS_TIENDA = Pais.NOMBRE;

INSERT INTO Pelicula(NOMBRE_PELICULA, DESCRIPCION_PELICULA, ANIO_LANZAMIENTO, CLASIFICACION, LENGUAJE,
    CATEGORIA, DURACION, COSTO_RENTA, COSTO_POR_DANIO)
    SELECT DISTINCT Temporal.NOMBRE_PELICULA, Temporal.DESCRIPCION_PELICULA, Lanzamiento.id,
    Clasificacion.id, Lenguaje.id, Categoria.id, Duracion.id,
    Temporal.COSTO_RENTA, Temporal.COSTO_POR_DANIO FROM Temporal
    INNER JOIN Lanzamiento ON Temporal.ANIO_LANZAMIENTO = Lanzamiento.lanzamiento
    INNER JOIN Clasificacion ON Temporal.CLASIFICACION = Clasificacion.clasificacion
    INNER JOIN Lenguaje ON Temporal.LENGUAJE_PELICULA = Lenguaje.lenguaje
    INNER JOIN Categoria ON Temporal.CATEGORIA_PELICULA = Categoria.categoria
    INNER JOIN Duracion ON Temporal.DURACION = Duracion.duracion;

INSERT INTO Inventario(CODIGO_TIENDA, CODIGO_PELICULA)
    SELECT DISTINCT Tienda.id, Pelicula.id
    FROM Temporal
    INNER JOIN Tienda ON Temporal.NOMBRE_TIENDA = Tienda.NOMBRE_TIENDA
    INNER JOIN Pelicula ON Temporal.NOMBRE_PELICULA = Pelicula.NOMBRE_PELICULA;

INSERT INTO DetallePelicula(CODIGO_PELICULA, ACTOR)
    SELECT DISTINCT Pelicula.id, Actor.id
    FROM Temporal 
    INNER JOIN Pelicula ON Temporal.NOMBRE_PELICULA = Pelicula.nombre_pelicula
    INNER JOIN Actor ON Temporal.ACTOR_PELICULA = CONCAT(Actor.nombre, Actor.apellido)
    OR Temporal.ACTOR_PELICULA = CONCAT(CONCAT(Actor.nombre, Actor.apellido), ',');

INSERT INTO Cliente(NOMBRE, APELLIDO, CORREO_CLIENTE, CLIENTE_ACTIVO, DIRECCION_CLIENTE, FECHA_CREACION, CODIGO_POSTAL_CLIENTE, CIUDAD_CLIENTE)
    SELECT DISTINCT REGEXP_SUBSTR(Temporal.NOMBRE_CLIENTE, '[^ ]+'), REGEXP_SUBSTR(Temporal.NOMBRE_CLIENTE, '(? ).*'),
    Temporal.CORREO_CLIENTE, Temporal.CLIENTE_ACTIVO,
    Temporal.DIRECCION_CLIENTE, Fecha.id, CodigoPostal.id, Ciudad.id
    FROM Temporal
    INNER JOIN Fecha ON Temporal.FECHA_CREACION = Fecha.FECHA
    INNER JOIN CodigoPostal ON Temporal.CODIGO_POSTAL_CLIENTE = CodigoPostal.CODIGO_POSTAL
    INNER JOIN Ciudad ON Temporal.CIUDAD_CLIENTE = Ciudad.CIUDAD;

INSERT INTO ClientePais(CLIENTE, PAIS)
    SELECT DISTINCT Cliente.id, Pais.id FROM Temporal, Cliente, Pais 
    WHERE Temporal.NOMBRE_CLIENTE = CONCAT(Cliente.NOMBRE, Cliente.APELLIDO) AND Temporal.PAIS_CLIENTE = Pais.NOMBRE;

INSERT INTO Empleado(NOMBRE_EMPLEADO, CORREO_EMPLEADO, EMPLEADO_ACTIVO, TIENDA_EMPLEADO, USUARIO_EMPLEADO,
    CONTRASENIA_EMPLEADO, CODIGO_POSTAL_EMPLEADO, DIRECCION_EMPLEADO)
    SELECT DISTINCT Temporal.NOMBRE_EMPLEADO, Temporal.CORREO_EMPLEADO, Temporal.EMPLEADO_ACTIVO, Tienda.id, Temporal.USUARIO_EMPLEADO,
    Temporal.CONTRASENIA_EMPLEADO, CodigoPostal.id, Temporal.DIRECCION_EMPLEADO
    FROM Temporal
    INNER JOIN Tienda ON Temporal.NOMBRE_TIENDA = Tienda.NOMBRE_TIENDA
    INNER JOIN CodigoPostal ON Temporal.CODIGO_POSTAL_EMPLEADO = CodigoPostal.CODIGO_POSTAL
    WHERE NOMBRE_EMPLEADO != '-';

INSERT INTO Empleado(NOMBRE_EMPLEADO, CORREO_EMPLEADO, EMPLEADO_ACTIVO, TIENDA_EMPLEADO,
    USUARIO_EMPLEADO, CONTRASENIA_EMPLEADO, CODIGO_POSTAL_EMPLEADO, DIRECCION_EMPLEADO)
    VALUES('-', '-', '-', 177, '-', '-', 1, '-');

INSERT INTO Renta(FECHA_RENTA, FECHA_RETORNO, MONTO_A_PAGAR, FECHA_PAGO, DIAS_RENTA, PELICULA, TIENDA, EMPLEADO, CLIENTE)
    SELECT Fecha.id, Fecha.id, Temporal.MONTO_A_PAGAR, Fecha.id, Temporal.DIAS_RENTA, Pelicula.id, Tienda.id, Empleado.id, Cliente.id
    FROM Temporal
    INNER JOIN Fecha ON Temporal.FECHA_RENTA = Fecha.FECHA
    INNER JOIN Fecha ON Temporal.FECHA_RETORNO = Fecha.FECHA
    INNER JOIN Fecha ON Temporal.FECHA_PAGO = Fecha.FECHA
    INNER JOIN Pelicula ON Temporal.NOMBRE_PELICULA = Pelicula.NOMBRE_PELICULA
    INNER JOIN Tienda ON Temporal.NOMBRE_TIENDA = Tienda.NOMBRE_TIENDA
    INNER JOIN Empleado ON Temporal.NOMBRE_EMPLEADO = Empleado.NOMBRE_EMPLEADO
    INNER JOIN Cliente ON Temporal.NOMBRE_CLIENTE = CONCAT(Cliente.NOMBRE, Cliente.APELLIDO)
    WHERE Temporal.NOMBRE_CLIENTE != '-' AND Temporal.NOMBRE_TIENDA != '-';
```
## Consultas
```
-- Consulta 1
    SELECT Pelicula.NOMBRE_PELICULA AS Pelicula,
        Tienda.NOMBRE_TIENDA AS Tienda,
        COUNT(Tienda.NOMBRE_TIENDA) AS Cantidad
        FROM Pelicula, Tienda WHERE Pelicula.NOMBRE_PELICULA = 'SUGAR WONKA' AND Pelicula.TIENDA = Tienda.id
        GROUP BY Tienda.NOMBRE_TIENDA, Pelicula.NOMBRE_PELICULA;

-- Consulta 2
    SELECT CONCAT(Cliente.NOMBRE, Cliente.APELLIDO) AS Cliente, SUM(Renta.MONTO_A_PAGAR), COUNT(Renta.CLIENTE)
        FROM Cliente, Renta
        WHERE Renta.CLIENTE = Cliente.id
        GROUP BY CONCAT(Cliente.NOMBRE, Cliente.APELLIDO)
        HAVING COUNT(Renta.CLIENTE) >= 40
        ORDER BY COUNT(Renta.CLIENTE) ASC

-- Consulta 4
    SELECT Actor.NOMBRE, Actor.APELLIDO FROM Actor 
        WHERE LOWER(Actor.APELLIDO) LIKE '%son%' ORDER BY Actor.NOMBRE

-- Consulta 5
    SELECT Actor.APELLIDO, COUNT(Actor.APELLIDO) AS Cantidad FROM Actor 
        GROUP BY Actor.APELLIDO
        HAVING COUNT(Actor.APELLIDO) >= 2

-- Consulta 6
    SELECT Pelicula.NOMBRE_PELICULA, Actor.NOMBRE, Actor.APELLIDO, Lanzamiento.LANZAMIENTO FROM Pelicula, DetallePelicula, Lanzamiento, Actor
        WHERE (LOWER(DESCRIPCION_PELICULA) LIKE '%shark%' OR LOWER(DESCRIPCION_PELICULA) LIKE '%crocodile%')
        AND Pelicula.id = DetallePelicula.CODIGO_PELICULA AND DetallePelicula.ACTOR = Actor.id
        AND DetallePelicula.ANIO_LANZAMIENTO = Lanzamiento.id
        GROUP BY Pelicula.NOMBRE_PELICULA, Actor.NOMBRE, Actor.APELLIDO, Lanzamiento.LANZAMIENTO ORDER BY Actor.APELLIDO ASC;

-- Consulta 7
    SELECT Categoria.CATEGORIA, COUNT(Pelicula.CATEGORIA) AS Cantidad FROM Categoria, Pelicula
        WHERE Categoria.id = Pelicula.CATEGORIA
        GROUP BY Pelicula.CATEGORIA, Categoria.CATEGORIA
        HAVING COUNT(Pelicula.CATEGORIA) < 65 AND COUNT(Pelicula.CATEGORIA) > 55

-- Consulta 8
    SELECT Categoria.CATEGORIA, AVG(Pelicula.COSTO_POR_DANIO - Pelicula.COSTO_RENTA) AS PROMEDIO
        FROM Categoria, Pelicula
        WHERE Categoria.id = Pelicula.CATEGORIA
        GROUP BY Categoria.CATEGORIA

-- Consulta 9
    SELECT Pelicula.NOMBRE_PELICULA, CONCAT(Actor.NOMBRE, Actor.APELLIDO) FROM Pelicula, Actor, DetallePelicula
        WHERE Actor.id = DetallePelicula.ACTOR AND Pelicula.id = DetallePelicula.CODIGO_PELICULA
        GROUP BY CONCAT(Actor.NOMBRE, Actor.APELLIDO), Pelicula.NOMBRE_PELICULA

-- Consulta 10
    SELECT CONCAT(Actor.NOMBRE, Actor.APELLIDO) FROM Actor 
        WHERE Actor.NOMBRE = 'Matthew'
        UNION
        SELECT CONCAT(Cliente.NOMBRE, Cliente.APELLIDO) FROM Cliente
        WHERE Cliente.NOMBRE = 'Matthew'

-- Consulta 11
    SELECT CONCAT(Cliente.NOMBRE, Cliente.APELLIDO) AS Cliente
        FROM Cliente, Renta
        WHERE Renta.CLIENTE = Cliente.id
        GROUP BY CONCAT(Cliente.NOMBRE, Cliente.APELLIDO)
        ORDER BY COUNT(Cliente.id) DESC;

-- Consulta 12
-- Fue eliminada

-- Consulta 18
-- No se puede hacer

-- Consulta 20
-- Si voy a ir a congreso
```
## Modelo Conceptual
![ModeloConceptual](https://drive.google.com/uc?export=view&id=1n_9qKjHX-oY6mLXl6j3sCAtY6xyM9PtB)

## Explicacion
### Pais
Se utiliza para almacenar los paises
### Duracion
Sirve para almacenar la duracion de las peliculas
### Actor
Sirve para almacenar la informacion de los actores
### Categoria
Sirve para almacenar las categorias de las peliculas
### Lenguaje
Sirve para almacenar los lenguajes que tienen las peliculas
### Clasificacion
Almacena la clasificacion de las peliculas
### CodigoPostal
Almacena el codigo postal de una ciudad
### Ciudad
Almacena las ciudades
### Fecha
Almacena las fechas
### Lanzamiento
Almacena el año de lanzamiento de una pelicula
### Tienda
Almacena la informacion de una tienda
### Pelicula
Almacena toda la informacion de las peliculas, costos, etc
### Inventario
Almacena las peliculas que pertenecen a una tienda
### DetallePelicula
Guarda los detalles de una pelicula, que actor aparecio
### Cliente
Maneja la informacion de los clientes
### ClientePais
Maneja la informacion del pais
### Empleado
Maneja la informacion del empleado
### Renta
Maneja la informacion de una renta
## Eliminacion de datos
```
DROP TABLE Renta;
DROP TABLE Empleado;
DROP TABLE ClientePais;
DROP TABLE Cliente;
DROP TABLE DetallePelicula;
DROP TABLE Inventario;
DROP TABLE Pelicula;
DROP TABLE Tienda;
DROP TABLE Lanzamiento;
DROP TABLE Fecha;
DROP TABLE Ciudad;
DROP TABLE CodigoPostal;
DROP TABLE Clasificacion;
DROP TABLE Lenguaje;
DROP TABLE Categoria;
DROP TABLE Actor;
DROP TABLE Costo;
DROP TABLE Duracion;
DROP TABLE Pais;
DROP TABLE Temporal;
```
## Modelo Logico
| Pais        |    |           |
| ----------- | -- | --------- |
| Columna     | id | nombre    |
| Restriccion | PK |           |
|             | 1  | Argentina |
|             | 2  | Guatemala |

| Duracion    |    |          |
| ----------- | -- | -------- |
| Columna     | id | Duracion |
| Restriccion | PK |          |
|             | 1  | 154      |
|             | 2  | 150      |

| Actor       |    |          |            |
| ----------- | -- | -------- | ---------- |
| Columna     | id | Nombre   | Apellido   |
| Restriccion | PK |          |            |
|             | 1  | Nombre 1 | Apellido 1 |
|             | 2  | Nombre 2 | Apellido 2 |

| Categoria   |    |           |
| ----------- | -- | --------- |
| Columna     | id | Categoria |
| Restriccion | PK |           |
|             | 1  | Family    |
|             | 2  | Sci-Fi    |

| Lenguaje    |    |          |
| ----------- | -- | -------- |
| Columna     | id | Lenguaje |
| Restriccion | PK |          |
|             | 1  | Ingles   |
|             | 2  | Ruso     |

| Clasificacion |    |               |
| ------------- | -- | ------------- |
| Columna       | id | Clasificacion |
| Restriccion   | PK |               |
|               | 1  | A             |
|               | 2  | R             |

| Fecha       |    |            |
| ----------- | -- | ---------- |
| Columna     | id | Fecha      |
| Restriccion | PK |            |
|             | 1  | 25/06/1993 |
|             | 2  | 25/08/2002 |

| Lanzamiento |    |
| ----------- | -- |
| Columna     | id | Lanzamiento |
| Restriccion | PK |  |
|             | 1  | 2003 |
|             | 2  | 2006 |

| Tienda      |    |          |           |        |        |      |
| ----------- | -- | -------- | --------- | ------ | ------ | ---- |
| Columna     | ID | NOMBRE   | DIRECCION | CODIGO | CIUDAD | PAIS |
| Restriccion | PK |          |           | PK     | PK     | PK   |
|             |    | Tienda 1 | Dir 1     |        |        |      |
|             |    | Tienda 2 | Dir 2     |        |        |      |

| Inventario  |    |        |      |
| ----------- | -- | ------ | ---- |
| Columna     | ID | TIENDA | PAIS |
| Restriccion | PK | FK     | FK   |
|             | 1  | 1      | 2    |
|             | 2  | 1      | 2    |

| DetallePelicula |    |          |
| --------------- | -- | -------- |
| Columna         | ID | PELICULA | ACTOR |
| Restriccion     | PK | FK       | FK |
|                 | 1  | 1        | 2 |
|                 | 2  | 1        | 2 |

| Cliente     |    |            |                                               |        |           |          |        |        |
| ----------- | -- | ---------- | --------------------------------------------- | ------ | --------- | -------- | ------ | ------ |
| Columna     | ID | NOMBRE     | CORREO                                        | ACTIVO | DIRECCION | FECHA    | CODIGO | CIUDAD |
| Restriccion | PK |            |                                               |        |           | FK       | FK     | FK     |
|             |    |            |                                               |        |           |          |        |        |
|             | 1  | Juan Pedro | [correo1@gmail.com](mailto:correo1@gmail.com) | SI     | Di2       | 2/5/2007 | 2      | 1      |
|             | 2  | Maria Inez | [correo2@gmail.com](mailto:correo2@gmail.com) | SI     | Di3       | 5/8/2010 | 12     | 3      |
