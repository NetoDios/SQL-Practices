# Practice 5


- Contraints
    - Primary Key
    - Foreing key
    - Unique Key
    - Not Null


## Constraint
> Es una propiedad que se le puede agregar a cualquier campo o conjunto de campos para al momento de insertar o actualizar un registro que este mantenga dicha propiedad.

Es posible tener multiples condiciones para un solo campo, o que varios campos compongan un mismo constraint
```sql
CREATE TABLE tableName (
    salary int,
    ...
    CONSTRAINT valid_salary CHECK (salary >= 0)
);
```


## Primary key
> Se refiere a un campo en la tabla que es unico y no nullo para todos los registros de dicha tabla.

Es recomendable que al crear la tabla se especifique que este campo sea numerico y que se auto genere, comunemnte se utiliza un autoincremento.

Es posible asignar a un dato especifico esta propiedad, o a multiples en conjunto con ayuda de un `constraint`
```sql
CREATE TABLE tableName (
    id bigserial,
    ...
    CONSTRAINT id_key PRIMARY KEY (id)
);
```


## Foreing key
> Es un campo en una tabla que sirve para asociar con un registro de una tabla distinta. Requiere que el valor exista en la tabla solicitada.
```sql
CREATE TABLE tableName (
    city_id text REFERENCES city(city_id),
    ...
);
```


## Unique key
> Se trata de un campo en la tabla que no puede ser compartido por ningun otro registro.
```sql
CREATE TABLE tableName (
    email text,
    ...
    CONSTRAINT unique_mail UNIQUE (email)
);
```


## Not Null
> Especifica que un campo de la tabla no puede ser nullo, o que siempre debe tener algun valor.

```sql
CREATE TABLE tableName (
    name text NOT NULL,
    ...
);
```