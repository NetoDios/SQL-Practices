# Practice 8

- Data Types
    - Date
    - Time
    - Interval

`'2022-12-01 18:37:12 EST'::timestamptz` de aqui podemos extraer
- Año
- Mes
- Día
- Hora
- Minuto
- Segundo
- Zona horaria
- Semana
- Cuarto
- Epoch

Podemos crear estos tipos de datos de la siguiente manera
```sql
SELECT make_date(2022, 2, 22);
SELECT make_time(18, 4, 30.3);
SELECT make_timestamptz(2022, 2, 22, 18, 4, 30.3, 'Europe/Lisbon');
```
Podemos acceder a estas fuciones que nos regresan tiempos
```sql
SELECT
    current_timestamp,
    localtimestamp,
    current_date,
    current_time,
    localtime,
    now();
```


## Challenge
Calculate the lenght of each ride. Sort the lenght from longest to shortest.
```sql
SELECT trip_id, tpep_dropoff_datetime - tpep_pickup_datetime AS duration_time
    FROM nyc_yellow_taxi_trips
      ORDER BY duration_time DESC
```