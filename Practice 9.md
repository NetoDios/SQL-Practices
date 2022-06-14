# Practice 9

- Subquery
    - WHERE
    - FROM
    - JOIN
    - IN
    - EXIST
    - CTE

## Subquery
Se trata de una busqueda en la que se hace una busqueda internamente, y esta es una funcionalidad que puede ser accesada desde multiples partes de la busqueda, y potencialmente anidada multiples veces.

## Subquery en un `WHERE`
```sql
SELECT salary
    FROM employee
    WHERE salary >= (
        SELECT avg_salary
            FROM companies
            ORDER BY avg_salary ASC
            LIMIT 1
        )
```

## Subquery en un `FROM`
```sql
SELECT
    outcome.avg_age, outcome.top_age
        FROM (
            SELECT avg(age) AS avg_age, max(age) AS top_age
                FROM students
        ) AS outcome;
```


## Subquery en un `JOIN`
```sql
SELECT 
    student.name, student.gpa, national_schools.avg_gpa, national_schools.year_date,
        FROM students
        JOIN (
            SELECT avg_gpa, year_date, state_code
                FROM schools
            ) AS national_schools
        ON student.state = national_schools.state_code
        ORDER BY student.gpa DESC;
```

## Subquery con `IN`
```sql
SELECT full_name
    FROM employees
    WHERE emp_id IN 
        (SELECT id
            FROM manager)
    ORDER BY emp_id;
```

## Subquery con `EXISTS`
Tambien se puede agregar `NOT` para el caso contrario
```sql
SELECT full_name
    FROM employees
    WHERE EXISTS (
        SELECT id
        FROM manager
        WHERE id = employees.emp_id);
```

## Subquery con `Commin Table Expressions`
Tambien se puede agregar `NOT` para el caso contrario
```sql
WITH temp_table (column1, column2)
    AS (
        SELECT column1, column2
            FROM table1
            WHERE condition1)
    SELECT column1, column2
    FROM temp_table
    WHERE condition2;
```