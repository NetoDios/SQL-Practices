# Practice 10

## Extensions
> Existen más utilidades y funciones que no son estandar para SQL, pero es posible incorporarlas gracias a que podemos importar extensiones que nos permiten analizar informacion de maneras nuevas.

Primero debemos instalar la extension de la siguiente manera
```sql
CREATE EXTENSION IF NOT EXISTS crosstab;
```

Esto nos permite ahora utilizar la extension con tan solo llamarla utilizando `extension()` y haciendo uso del lenguaje definido por la extension dentro de los parentecis

## Challenge
```sql
SELECT *
    FROM crosstab(
        'SELECT flavor, office, count(*)
            FROM ice_cream_survey
                GROUP BY flavor, office
                ORDER BY flavor',
        'SELECT office
            FROM ice_cream_survey
                GROUP BY office
                ORDER BY office')
    AS (office text,
        Downtown bigint,
        Midtown bigint,
        Uptown bigint);
```