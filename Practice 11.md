# Practice 11


## Case Formatting
Hay ocaciones en las que podriamos tener algun dato guardado en un formato pero necesitamos trabajar en otro, para ello es necesario utilizar las siguientes funciones

- `UPPER('')` Convierte todo a mayusculas
- `LOWER('')` Convierte todo a minusculas
- `INITCAP('')` Todas las palabras tienen mayuscula al inicio
```sql
SELECT UPPER('some text here');
```

## Character Data
Se presentan situaciones donde nos es importatne que un dato sea de cierto tamaño, o que este estructurado correctamente, para saber esto usamos fuciones como
- `LENGHT('')` Retorna el tamaño total de la cadena
- `POSITION('' in '')` Retorna la primer instancia buscada
```sql
SELECT LENGTH('some text here');
```

## Handle Data
Ahora hablaremos de como tomar un dato y seleccionar solo una porcion de el, ya sea quitar otras porciones, cambiarlas, refactorizar y mas usamos estas funciones
- `TRIM('')` Retorna el valor ingresado sin espacios al inicio y final. Puede asignarse el caracter a eliminar.
- `LTRIM('')` Retorna el valor ingresado sin espacios al inicio
- `RTRIM('')` Retorna el valor ingresado sin espacios al final
- `LEFT('', #)` Retorna los primeros `#` caracteres
- `RIGHT('', #)` Retorna los ultimos `#` caracteres
- `REPLACE('','','')` Retorna el primer valor sustituyendo el segundo con el tercero
```sql
SELECT TRIM('   some text here  ');
SELECT LEFT('some text here', 4);
SELECT REPLACE('some text here', 'me', 'ME');
```

## Regular Expresions
Se pueden utilizar expresiones regulares para verificar que un dato se encuentre formateado correctamente, o simplemente reconocer algun patron entre los datos
[Practice RegEx](https://regex101.com/)

Las expresiones regulares se pueden utilizar en varias partes de la querry, como `WHERE` o dentro de funciones predefinidas
```sql
SELECT *
    FROM table_name
    WHERE column_name ~ '\\bworld\\b';
```