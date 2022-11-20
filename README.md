# TP BBDD I

## General
```
            Modelar, llenar y consultar una base de datos del tipo SQL usando las diferentes herramientas, comandos y principalmente conceptos adquiridos en el curso de la materia.
```
---
## Puntos necesarios
```
1. Diagrama de entidad relación DER de la base de datos mostrando la información básica como son: entidades y sus atributos (indicando tipo e información especial como Pk o Fk) y líneas de uniones con los símbolos correspondientes. Dicho diagrama debe tener un mínimo de 8 entidades y variedad de cardinalidades (uno a muchos, muchos a muchos y en lo posible alguna relación uno a uno).

2. Mostrar todos los comandos necesarios para la creación de las tablas del punto anterior.

3. Llenar las tablas con datos, coherentes y relevantes para el negocio.

4.Realizar y mostrar tres consultas complejas usando joins anidados y sus resultados, los cuales deben ser reveladores para el proposito de la base de datos.
```
---
## Herramientas utilizadas:
  - [SQLite](https://www.sqlite.org/index.html)
  - [GitHub](https://github.com/DIOLINK/TP-BBDD-I)
  - [Mockaroo](https://www.mockaroo.com/)

---
# E-COMMERCE 

## 1. Diagrama de entidad relación.

---
## 2. Los comandos necesarios para la creación de las tablas.

- USUARIO
```
CREATE TABLE
    usuario (
        usuario_id INTEGER PRIMARY KEY NOT NULL,
        direcciones_id INTEGER NOT NULL REFERENCES direccion (direccion_id),
        nombre VARCHAR (40),
        CUIT_CUIL VARCHAR (11),
        proveedor BOOLEAN
    );
```
- DIRECCIÓN
```
CREATE TABLE
    direccion (
        direccion_id INTEGER PRIMARY KEY NOT NULL,
        name_calle VARCHAR (40),
        localidad VARCHAR (20),
        provincia VARCHAR (20),
        altura INTEGER,
        codigo_postal VARCHAR (8)
    );
```
- SUCURSAL
```
CREATE TABLE
    sucursal (
        sucursal_id INTEGER PRIMARY KEY NOT NULL,
        name_director VARCHAR (40),
        gender_director CHAR,
        place_birth_director VARCHAR (20),
        country_director VARCHAR (20),
        direcciones_id INTEGER NOT NULL REFERENCES direccion (direccion_id)
    );
```
- PRODUCTO
```
CREATE TABLE
    producto (
        producto_id INTEGER PRIMARY KEY NOT NULL,
        name VARCHAR (40),
        url_image VARCHAR (256),
        description VARCHAR (256),
        precio FLOAT
    );
```
- MEDIO DE PAGO
```
CREATE TABLE
    medio_pago (
        medio_pago_id INTEGER PRIMARY KEY NOT NULL,
        tipo_pago BOOLEAN,
        description VARCHAR (256)
    );
```
- FACTURAS
```
CREATE TABLE
    facturas (
        factura_id INTEGER PRIMARY KEY NOT NULL,
        usuario_proveedor_id INTEGER REFERENCES usuario (usuario_id),
        usuario_cliente_id INTEGER REFERENCES usuario (usuario_id),
        tipo_pago_id INTEGER REFERENCES MedioPago (medio_pago_id),
        producto_id INTEGER REFERENCES producto (producto_id),
        sucursal_id INTEGER REFERENCES sucursal (sucursal_id),
        cantidad INTEGER,
        descripcion VARCHAR (256),
        condicion_IVA CHAR
    );
```
- AYUDA
```
CREATE TABLE
    ayuda (
        ayuda_id INTEGER PRIMARY KEY NOT NULL,
        usuario_id INTEGER REFERENCES usuario (usuario_id),
        factura_id INTEGER REFERENCES facturas (factura_id),
        description VARCHAR (256),
        tipo VARCHAR (40)
    );
```

---
