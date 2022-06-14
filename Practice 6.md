# Practice 6

> La manera comun en la que las bases de datos buscan informcaion es iterando por todos los registros y verificando si dicho registro cumple con las condiciones.


## Indexes
> Los indices son una estretegia utilizada para agilizar y optimizar el proceso de busquedas en una base de datos.
Preprosesan la informacion y generan una estructura de datos facil de indexar y de hacer busquedas sobre ella. Estructuras tale scomo arboles o tablas de hasheo.

Primeramente debemos generar la estructura, lo cual se hace con una estructura como la siguiente
```sql
CREATE INDEX students_index on students(
    full_name
);
```
Ahora al hacer una busqueda como la siguiente los tiempos de ejecucion seran más veloces
```sql
SELECT * FROM students
    WHERE full_name = 'Neto Alvarez';
```
