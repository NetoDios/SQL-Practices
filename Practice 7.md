# Practice 7

- Cleanup data
    - Finding Duplicates
    - Find Missing Data
    - Constraints
    - Fixing The Data


## Cleanup Data
> Muchas veces la estructura de una tabla se encuentra comprometida, ya sea que contiene redundancia, o como lo atacamos hoy, los datos que contiene se encuentran comprometidos, ya sea porque tenemos datos duplicados o faltantes.


## Finding Duplicates
Lo primero que debemos hacer para encontrar datos duplicados es entender que siginifica a nivel de base de datos que se encuentren duplicados, y pues esto es sencillo, que todos sus datos sean iguales.

Para buscar todos los registros que se encuentran duplicados basta con agrupar todos los datos (importantes al contexto) y compararlos asi. Al final solo escogemos aquellos que tengan más de una instancia.
```sql
SELECT company,
       street,
       count(*) AS address_count
FROM company_address
GROUP BY company, street
HAVING count(*) > 1
ORDER BY company, street;
```


## Finding Missing Data
Similarmente para encontrar datos faltantes basta con hacer una busqueda simple donde preguntemos si el campo importante (puede ser un conjunto de campos) es vacio o no.

```sql
SELECT * FROM company_address
    WHERE street IS NULL;
```


## Constraints
Ahora, vamos a buscar que los datos cumplan con condiciones y que no se encuentren incosistentes.

Para esto la manera de abordarlo es especifica al campo y lo que se quiera comprobar, podemos buscar inconsistencias en la forma de escribir digase una empresa de la siguiente forma
```sql
SELECT company, count(*) AS company_count
    FROM clients
        GROUP BY company
        ORDER BY company ASC;
```
O si un numero telefonico podria ser valido de esta manera
```sql
SELECT length(phone_number),
       count(*) AS length_count
FROM contacts
GROUP BY length(phone_number)
ORDER BY length(phone_number) ASC;
```


## Fixing The Data
De muy poco nos sirve simplemente buscar los datos corrompidos en una base de datos, pero es un paso necesario antes de corregir estos errores.

Que para arreglar esto seguimos simples pasos
1. Creamos una tabla de respaldo (por seguridad)
```sql
CREATE TABLE table_backup AS
    SELECT * FROM original_table;
```
2. Agregamos una columna con el dato que debemos corregir
```sql
ALTER TABLE original_table
    ADD COLUMN temp_city text;
```
3. Llenamos la nueva columna con el dato pertinente
```sql
UPDATE original_table
    SET temp_city = city;
```
4. Actualizamos el dato original con el valor deseado
```sql
UPDATE original_table
    SET city = 'GDL'
        WHERE zip_code = '45000';
```
Cuando cometemos algun error simplemente recurrimos a reiniciar el proceso con la columna temporal, o el respaldo de la tambla.
```sql
UPDATE riginal_table original
    SET city = backup.city
        FROM table_backup backup
        WHERE original.id = backup.id;
```

## Chalange
Tenemos que agregar una columna con valor `boolean` que sera cierto si la empresa tiene entre sus actividades `Meat Processing` y caso contrario es falso.
```sql
ALTER TABLE meat_poultry_egg_establishments
    ADD COLUMN meat_processing boolean NOT NULL DEFAULT false;

UPDATE meat_poultry_egg_establishments 
    SET meat_processing = true
        WHERE activities LIKE '%Meat Processing%';
```