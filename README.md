# Taller 2 Bases De Datos

## Creacion Base De Datos

```sql
-- Creacion de la DB principal
CREATE DATABASE gestor_empleados;

-- Ingresar a la DB
USE gestor_empleados;

-- Creacion de Tablas
CREATE TABLE departamento (
	id_departamento INT(10) PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    presupuesto DOUBLE NOT NULL,
    gastos DOUBLE NOT NULL
);

CREATE TABLE empleado (
    id_empleado INT(10) PRIMARY KEY,
    nit VARCHAR(9) NOT NULL,
    nombre VARCHAR(100) NOT NULL,
    apellido1 VARCHAR(100),
    apellido2 VARCHAR(100),
    id_departamento INT(10),
    CONSTRAINT FK_CodigoDepartamento FOREIGN KEY (id_departamento) REFERENCES departamento(id_departamento)
);
```



## Consultas Sobre Una Tabla

**1.** Lista el primer apellido de todos los empleados

```sql
SELECT apellido1
FROM empleado;

+-----------+
| apellido1 |
+-----------+
| Rivero    |
| Salas     |
| Rubio     |
| Loyola    |
| Santana   |
| Ruiz      |
| Gómez     |
| Flores    |
| Herrera   |
| Salas     |
| Sáez      |
+-----------+
```

**2.** Lista el primer apellido de los empleados eliminando los apellidos que estén repetidos.

```sql
SELECT DISTINCT apellido1
FROM empleado;
+-----------+
| apellido1 |
+-----------+
| Rivero    |
| Salas     |
| Rubio     |
| Loyola    |
| Santana   |
| Ruiz      |
| Gómez     |
| Flores    |
| Herrera   |
| Sáez      |
+-----------+
```

**3.** Lista todas las columnas de la tabla empleado.

```sql
SELECT id_empleado, nit, nombre, apellido1, apellido2, id_departamento
FROM empleado;
+-------------+-----------+--------------+-----------+-----------+-----------------+
| id_empleado | nit       | nombre       | apellido1 | apellido2 | id_departamento |
+-------------+-----------+--------------+-----------+-----------+-----------------+
|           1 | 32481596F | Aarón        | Rivero    | Gómez     |               1 |
|           2 | Y5575632D | Adela        | Salas     | Díaz      |               2 |
|           3 | R6970642B | Adolfo       | Rubio     | Flores    |               3 |
|           5 | 17087203C | Marcos       | Loyola    | Méndez    |               5 |
|           6 | 38382980M | María        | Santana   | Moreno    |               1 |
|           8 | 71651431Z | Pepe         | Ruiz      | Santana   |               3 |
|           9 | 56399183D | Juan         | Gómez     | López     |               2 |
|          10 | 46384486H | Diego        | Flores    | Salas     |               5 |
|          11 | 67389283A | Marta        | Herrera   | Gil       |               1 |
|          12 | 41234836R | Irene        | Salas     | Flores    |            NULL |
|          13 | 82635162B | Juan Antonio | Sáez      | Guerrero  |            NULL |
+-------------+-----------+--------------+-----------+-----------+-----------------+
```

**4.** Lista el nombre y los apellidos de todos los empleados.

```sql
SELECT nombre, apellido1, apellido2
FROM empleado;
+--------------+-----------+-----------+
| nombre       | apellido1 | apellido2 |
+--------------+-----------+-----------+
| Aarón        | Rivero    | Gómez     |
| Adela        | Salas     | Díaz      |
| Adolfo       | Rubio     | Flores    |
| Marcos       | Loyola    | Méndez    |
| María        | Santana   | Moreno    |
| Pepe         | Ruiz      | Santana   |
| Juan         | Gómez     | López     |
| Diego        | Flores    | Salas     |
| Marta        | Herrera   | Gil       |
| Irene        | Salas     | Flores    |
| Juan Antonio | Sáez      | Guerrero  |
+--------------+-----------+-----------+
```

**5.** Lista el identificador de los departamentos de los empleados que aparecen en la tabla empleado.

```sql
SELECT id_departamento
FROM empleado;
+-----------------+
| id_departamento |
+-----------------+
|            NULL |
|            NULL |
|               1 |
|               1 |
|               1 |
|               2 |
|               2 |
|               3 |
|               3 |
|               5 |
|               5 |
+-----------------+
```

**6.** Lista el identificador de los departamentos de los empleados que aparecen en la tabla empleado, eliminando los identificadores que aparecen repetidos.

```sql
SELECT DISTINCT id_departamento
FROM empleado;
+-----------------+
| id_departamento |
+-----------------+
|            NULL |
|               1 |
|               2 |
|               3 |
|               5 |
+-----------------+
```

**7.** Lista el nombre y apellidos de los empleados en una única columna.

```sql
SELECT CONCAT(nombre,' ', apellido1,' ', apellido2)
FROM empleado;
+----------------------------------------------+
| CONCAT(nombre,' ', apellido1,' ', apellido2) |
+----------------------------------------------+
| Aarón Rivero Gómez                           |
| Adela Salas Díaz                             |
| Adolfo Rubio Flores                          |
| Marcos Loyola Méndez                         |
| María Santana Moreno                         |
| Pepe Ruiz Santana                            |
| Juan Gómez López                             |
| Diego Flores Salas                           |
| Marta Herrera Gil                            |
| Irene Salas Flores                           |
| Juan Antonio Sáez Guerrero                   |
+----------------------------------------------+
```

**8.** Lista el nombre y apellidos de los empleados en una única columna, convirtiendo todos los caracteres en mayúscula.

```sql
SELECT UPPER(CONCAT(nombre,' ', apellido1,' ', apellido2))
FROM empleado;
+-----------------------------------------------------+
| UPPER(CONCAT(nombre,' ', apellido1,' ', apellido2)) |
+-----------------------------------------------------+
| AARÓN RIVERO GÓMEZ                                  |
| ADELA SALAS DÍAZ                                    |
| ADOLFO RUBIO FLORES                                 |
| MARCOS LOYOLA MÉNDEZ                                |
| MARÍA SANTANA MORENO                                |
| PEPE RUIZ SANTANA                                   |
| JUAN GÓMEZ LÓPEZ                                    |
| DIEGO FLORES SALAS                                  |
| MARTA HERRERA GIL                                   |
| IRENE SALAS FLORES                                  |
| JUAN ANTONIO SÁEZ GUERRERO                          |
+-----------------------------------------------------+
```

**9.** Lista el nombre y apellidos de los empleados en una única columna, convirtiendo todos los caracteres en minúscula.



```sql
SELECT LOWER(CONCAT(nombre,' ', apellido1,' ', apellido2))
FROM empleado;
+-----------------------------------------------------+
| LOWER(CONCAT(nombre,' ', apellido1,' ', apellido2)) |
+-----------------------------------------------------+
| aarón rivero gómez                                  |
| adela salas díaz                                    |
| adolfo rubio flores                                 |
| marcos loyola méndez                                |
| maría santana moreno                                |
| pepe ruiz santana                                   |
| juan gómez lópez                                    |
| diego flores salas                                  |
| marta herrera gil                                   |
| irene salas flores                                  |
| juan antonio sáez guerrero                          |
+-----------------------------------------------------+

```

**10.** Lista el identificador de los empleados junto al nit, pero el nit deberá aparecer en dos columnas, una mostrará únicamente los dígitos del nit y la otra la letra.

```sql
SELECT id_empleado, LEFT(nit, 8) AS nit_digitos, SUBSTRI	NG(nit, -1) AS nit_letra
FROM empleados;
+-------------+-------------+-----------+
| id_empleado | nit_digitos | nit_letra |
+-------------+-------------+-----------+
|           1 | 32481596    | F         |
|           2 | Y5575632    | D         |
|           3 | R6970642    | B         |
|           5 | 17087203    | C         |
|           6 | 38382980    | M         |
|           8 | 71651431    | Z         |
|           9 | 56399183    | D         |
|          10 | 46384486    | H         |
|          11 | 67389283    | A         |
|          12 | 41234836    | R         |
|          13 | 82635162    | B         |
+-------------+-------------+-----------+
```

**11.** Lista el nombre de cada departamento y el valor del presupuesto actual del que dispone. Para calcular este dato tendrá que restar al valor del presupuesto inicial (columna presupuesto) los gastos que se han generado (columna gastos). Tenga en cuenta que en algunos casos pueden existir valores negativos. Utilice un alias apropiado para la nueva columna columna que está calculando.

```sql
SELECT nombre, (presupuesto - gastos) AS presupuesto_actual
FROM departamento;
+------------------+--------------------+
| nombre           | presupuesto_actual |
+------------------+--------------------+
| Desarrollo       |             114000 |
| Sistemas         |             129000 |
| Recursos Humanos |             255000 |
| Contabilidad     |             107000 |
| I+D              |              -5000 |
| Proyectos        |                  0 |
+------------------+--------------------+
```

**12.** Lista el nombre de los departamentos y el valor del presupuesto actual ordenado de forma ascendente.

```sql
SELECT nombre, (presupuesto - gastos) AS presupuesto_actual
FROM presupuesto_actual
ORDER BY departamento ASC;
+------------------+--------------------+
| nombre           | presupuesto_actual |
+------------------+--------------------+
| I+D              |              -5000 |
| Proyectos        |                  0 |
| Contabilidad     |             107000 |
| Desarrollo       |             114000 |
| Sistemas         |             129000 |
| Recursos Humanos |             255000 |
+------------------+--------------------+
```

**13. **Lista el nombre de todos los departamentos ordenados de forma ascendente.

```sql
SELECT nombre
FROM departamento
ORDER BY nombre ASC;
+------------------+
| nombre           |
+------------------+
| Contabilidad     |
| Desarrollo       |
| I+D              |
| Proyectos        |
| Recursos Humanos |
| Sistemas         |
+------------------+
```

**14. **Lista el nombre de todos los departamentos ordenados de forma descendente.

```sql
SELECT nombre
FROM departamento
ORDER BY nombre DESC;
+------------------+
| nombre           |
+------------------+
| Sistemas         |
| Recursos Humanos |
| Proyectos        |
| I+D              |
| Desarrollo       |
| Contabilidad     |
+------------------+
```

**15.** Lista los apellidos y el nombre de todos los empleados, ordenados de forma alfabética tendiendo en cuenta en primer lugar sus apellidos y luego su nombre.

```sql
SELECT CONCAT(nombre,' ', apellido1, ' ', apellido2) AS nombre_completo
FROM empleados
ORDER BY nombre_completo;
+-----------------------------+
| nombre_completo             |
+-----------------------------+
| Aarón Rivero Gómez          |
| Adela Salas Díaz            |
| Adolfo Rubio Flores         |
| Diego Flores Salas          |
| Irene Salas Flores          |
| Juan Antonio Sáez Guerrero  |
| Juan Gómez López            |
| Marcos Loyola Méndez        |
| María Santana Moreno        |
| Marta Herrera Gil           |
| Pepe Ruiz Santana           |
+-----------------------------+
```

**16.** Devuelve una lista con el nombre y el presupuesto, de los 3 departamentos que tienen mayor presupuesto.

```sql
SELECT nombre,presupuesto FROM departamento
ORDER BY presupuesto DESC LIMIT 3;
+------------------+-------------+
| nombre           | presupuesto |
+------------------+-------------+
| I+D              |      375000 |
| Recursos Humanos |      280000 |
| Sistemas         |      150000 |
+------------------+-------------+
```

**17. ** Devuelve una lista con el nombre y el presupuesto, de los 3 departamentos que tienen menor presupuesto.

```sql
SELECT nombre,presupuesto
FROM departamento
ORDER BY presupuesto ASC LIMIT 3;
+--------------+-------------+
| nombre       | presupuesto |
+--------------+-------------+
| Proyectos    |           0 |
| Publicidad   |           0 |
| Contabilidad |      110000 |
+--------------+-------------+
```

**18.** Devuelve una lista con el nombre y el gasto, de los 2 departamentos que tienen mayor gasto.

```sql
SELECT nombre, gastos
FROM departamento
ORDER BY gastos DESC LIMIT 2;
+------------------+--------+
| nombre           | gastos |
+------------------+--------+
| I+D              | 380000 |
| Recursos Humanos |  25000 |
+------------------+--------+
```

**19.** Devuelve una lista con el nombre y el gasto, de los 2 departamentos que tienen menor gasto.

```sql
SELECT nombre, gastos
FROM departamento
ORDER BY gastos ASC LIMIT 2;
+------------+--------+
| nombre     | gastos |
+------------+--------+
| Proyectos  |      0 |
| Publicidad |   1000 |
+------------+--------+
```

**20.** Devuelve una lista con 5 filas a partir de la tercera fila de la tabla empleado. La tercera fila se debe incluir en la respuesta. La respuesta debe incluir todas las columnas de la tabla empleado.

```sql
SELECT id_empleado,nit,nombre,apellido1,apellido2, id_departamento
FROM empleado
LIMIT 5 OFFSET 2;
+-------------+-----------+--------+-----------+-----------+-----------------+
| id_empleado | nit       | nombre | apellido1 | apellido2 | id_departamento |
+-------------+-----------+--------+-----------+-----------+-----------------+
|           3 | R6970642B | Adolfo | Rubio     | Flores    |               3 |
|           5 | 17087203C | Marcos | Loyola    | Méndez    |               5 |
|           6 | 38382980M | María  | Santana   | Moreno    |               1 |
|           8 | 71651431Z | Pepe   | Ruiz      | Santana   |               3 |
|           9 | 56399183D | Juan   | Gómez     | López     |               2 |
+-------------+-----------+--------+-----------+-----------+-----------------+
```

**21.** Devuelve una lista con el nombre de los departamentos y el presupuesto, de aquellos que tienen un presupuesto mayor o igual a 150000 euros.

```sql
SELECT nombre, presupuesto
FROM departamento
WHERE presupuesto >= 150000;
+------------------+-------------+
| nombre           | presupuesto |
+------------------+-------------+
| Sistemas         |      150000 |
| Recursos Humanos |      280000 |
| I+D              |      375000 |
+------------------+-------------+
```

**22.** 22. Devuelve una lista con el nombre de los departamentos y el gasto, de aquellos que tienen menos de 5000 euros de gastos.

```sql
SELECT nombre, gastos
FROM departamento
WHERE gastos <= 5000;
+--------------+--------+
| nombre       | gastos |
+--------------+--------+
| Contabilidad |   3000 |
| Proyectos    |      0 |
| Publicidad   |   1000 |
+--------------+--------+
```

**23.** Devuelve una lista con el nombre de los departamentos y el presupuesto, de aquellos que tienen un presupuesto entre 100000 y 200000 euros. Sin utilizar el operador BETWEEN.

```sql
SELECT nombre, presupuesto
FROM departamento
WHERE presupuesto >= 100000 AND presupuesto <= 200000;
+--------------+-------------+
| nombre       | presupuesto |
+--------------+-------------+
| Desarrollo   |      120000 |
| Sistemas     |      150000 |
| Contabilidad |      110000 |
+--------------+-------------+
```

**24.** Devuelve una lista con el nombre de los departamentos que no tienen un presupuesto entre 100000 y 200000 euros. Sin utilizar el operador BETWEEN.

```sql
SELECT nombre, presupuesto
FROM departamento
WHERE NOT (presupuesto >= 100000 AND presupuesto <= 200000);
+------------------+-------------+
| nombre           | presupuesto |
+------------------+-------------+
| Recursos Humanos |      280000 |
| I+D              |      375000 |
| Proyectos        |           0 |
| Publicidad       |           0 |
+------------------+-------------+
```

**25.** Devuelve una lista con el nombre de los departamentos que tienen un presupuesto entre 100000 y 200000 euros. Utilizando el operador BETWEEN.

```sql
SELECT nombre, presupuesto 
FROM departamento 
WHERE presupuesto BETWEEN 100000 AND 200000;
+--------------+-------------+
| nombre       | presupuesto |
+--------------+-------------+
| Desarrollo   |      120000 |
| Sistemas     |      150000 |
| Contabilidad |      110000 |
+--------------+-------------+
```

**26.** Devuelve una lista con el nombre de los departamentos que no tienen un presupuesto entre 100000 y 200000 euros. Utilizando el operador BETWEEN.

```sql
SELECT nombre, presupuesto  
FROM departamento  
WHERE NOT (presupuesto BETWEEN 100000 AND 200000);
+------------------+-------------+
| nombre           | presupuesto |
+------------------+-------------+
| Recursos Humanos |      280000 |
| I+D              |      375000 |
| Proyectos        |           0 |
| Publicidad       |           0 |
+------------------+-------------+
```

**27.** Devuelve una lista con el nombre de los departamentos, gastos y presupuesto, de aquellos departamentos donde los gastos sean mayores que el presupuesto del que disponen.

```sql
SELECT nombre,gasto,presupuesto 
FROM departamento
WHERE gasto > presupuesto;
+------------+--------+-------------+
| nombre     | gasto  | presupuesto |
+------------+--------+-------------+
| I+D        | 380000 |      375000 |
| Publicidad |   1000 |           0 |
+------------+--------+-------------+
```

**28.** Devuelve una lista con el nombre de los departamentos, gastos y presupuesto, de aquellos departamentos donde los gastos sean menores que el presupuesto del que disponen.

```sql
SELECT nombre,gasto,presupuesto 
FROM departamento 
WHERE gasto < presupuesto;
+------------------+-------+-------------+
| nombre           | gasto | presupuesto |
+------------------+-------+-------------+
| Desarrollo       |  6000 |      120000 |
| Sistemas         | 21000 |      150000 |
| Recursos Humanos | 25000 |      280000 |
| Contabilidad     |  3000 |      110000 |
+------------------+-------+-------------+
```

**29.** Devuelve una lista con el nombre de los departamentos, gastos y presupuesto, de aquellos departamentos donde los gastos sean iguales al presupuesto del que disponen.

```sql
SELECT nombre,gasto,presupuesto 
FROM departamento 
WHERE gasto = presupuesto;
+-----------+-------+-------------+
| nombre    | gasto | presupuesto |
+-----------+-------+-------------+
| Proyectos |     0 |           0 |
+-----------+-------+-------------+
```

**30.** Lista todos los datos de los empleados cuyo segundo apellido sea NULL.

```sql
SELECT id_empleado, nit, nombre, apellido1, apellido2, id_departamento 
FROM empleado 
WHERE apellido2 IS NULL;
+-------------+-----------+---------+-----------+-----------+-----------------+
| id_empleado | nit       | nombre  | apellido1 | apellido2 | id_departamento |
+-------------+-----------+---------+-----------+-----------+-----------------+
|           4 | 77705545E | Adrián  | Suárez    | NULL      |               4 |
|           7 | 80576669X | Pilar   | Ruiz      | NULL      |               2 |
+-------------+-----------+---------+-----------+-----------+-----------------+

```

**31.** Lista todos los datos de los empleados cuyo segundo apellido no sea NULL.

```sql
SELECT id_empleado, nit, nombre, apellido1, apellido2, id_departamento 
FROM empleado 
WHERE apellido2 IS NOT NULL;
+-------------+-----------+--------------+-----------+-----------+-----------------+
| id_empleado | nit       | nombre       | apellido1 | apellido2 | id_departamento |
+-------------+-----------+--------------+-----------+-----------+-----------------+
|           1 | 32481596F | Aarón        | Rivero    | Gómez     |               1 |
|           2 | Y5575632D | Adela        | Salas     | Díaz      |               2 |
|           3 | R6970642B | Adolfo       | Rubio     | Flores    |               3 |
|           5 | 17087203C | Marcos       | Loyola    | Méndez    |               5 |
|           6 | 38382980M | María        | Santana   | Moreno    |               1 |
|           8 | 71651431Z | Pepe         | Ruiz      | Santana   |               3 |
|           9 | 56399183D | Juan         | Gómez     | López     |               2 |
|          10 | 46384486H | Diego        | Flores    | Salas     |               5 |
|          11 | 67389283A | Marta        | Herrera   | Gil       |               1 |
|          12 | 41234836R | Irene        | Salas     | Flores    |            NULL |
|          13 | 82635162B | Juan Antonio | Sáez      | Guerrero  |            NULL |
+-------------+-----------+--------------+-----------+-----------+-----------------+
```

**32.** Lista todos los datos de los empleados cuyo segundo apellido sea López.

```sql
SELECT id_empleado, nit, nombre, apellido1, apellido2, id_departamento 
FROM empleado 
WHERE apellido2 = 'López';
+-------------+-----------+--------+-----------+-----------+-----------------+
| id_empleado | nit       | nombre | apellido1 | apellido2 | id_departamento |
+-------------+-----------+--------+-----------+-----------+-----------------+
|           9 | 56399183D | Juan   | Gómez     | López     |               2 |
+-------------+-----------+--------+-----------+-----------+-----------------+
```

**33.** Lista todos los datos de los empleados cuyo segundo apellido sea Díaz o Moreno. Sin utilizar el operador IN.

```sql
SELECT id_empleado, nit, nombre, apellido1, apellido2, id_departamento 
FROM empleado 
WHERE apellido2 = 'Díaz' OR apellido2 = 'Moreno';
+-------------+-----------+--------+-----------+-----------+-----------------+
| id_empleado | nit       | nombre | apellido1 | apellido2 | id_departamento |
+-------------+-----------+--------+-----------+-----------+-----------------+
|           2 | Y5575632D | Adela  | Salas     | Díaz      |               2 |
|           6 | 38382980M | María  | Santana   | Moreno    |               1 |
+-------------+-----------+--------+-----------+-----------+-----------------+
```

**34.** Lista todos los datos de los empleados cuyo segundo apellido sea Díaz o Moreno. Utilizando el operador IN.

```sql
SELECT id_empleado, nit, nombre, apellido1, apellido2, id_departamento 
FROM empleado 
WHERE apellido2 IN ('Díaz', 'Moreno');
+-------------+-----------+--------+-----------+-----------+-----------------+
| id_empleado | nit       | nombre | apellido1 | apellido2 | id_departamento |
+-------------+-----------+--------+-----------+-----------+-----------------+
|           2 | Y5575632D | Adela  | Salas     | Díaz      |               2 |
|           6 | 38382980M | María  | Santana   | Moreno    |               1 |
+-------------+-----------+--------+-----------+-----------+-----------------+
```

**35.** Lista los nombres, apellidos y nit de los empleados que trabajan en el departamento 3.

```sql
SELECT nombre, apellido1, apellido2, nit, id_departamento
FROM empleado
WHERE id_departamento = 3;
+--------+-----------+-----------+-----------+-----------------+
| nombre | apellido1 | apellido2 | nit       | id_departamento |
+--------+-----------+-----------+-----------+-----------------+
| Adolfo | Rubio     | Flores    | R6970642B |               3 |
| Pepe   | Ruiz      | Santana   | 71651431Z |               3 |
+--------+-----------+-----------+-----------+-----------------+
```

**36.** Lista los nombres, apellidos y nit de los empleados que trabajan en los departamentos 2, 4 o 5.

```sql
SELECT nombre, apellido1, apellido2, nit, id_departamento
FROM empleado
WHERE id_departamento IN (2,4,5);
+---------+-----------+-----------+-----------+-----------------+
| nombre  | apellido1 | apellido2 | nit       | id_departamento |
+---------+-----------+-----------+-----------+-----------------+
| Adela   | Salas     | Díaz      | Y5575632D |               2 |
| Pilar   | Ruiz      | NULL      | 80576669X |               2 |
| Juan    | Gómez     | López     | 56399183D |               2 |
| Adrián  | Suárez    | NULL      | 77705545E |               4 |
| Marcos  | Loyola    | Méndez    | 17087203C |               5 |
| Diego   | Flores    | Salas     | 46384486H |               5 |
+---------+-----------+-----------+-----------+-----------------+

```

---

## Consultas Multitabla

**1.** Devuelve un listado con los empleados y los datos de los departamentos donde trabaja cada uno.

```sql
SELECT e.nombre, e.apellido1, e.apellido2, d.id_departamento, d.nombre, d.presupuesto, d.gastos
FROM empleado AS e, departamento AS d
WHERE e.id_departamento = d.id_departamento;
+---------+-----------+-----------+-----------------+------------------+-------------+--------+
| nombre  | apellido1 | apellido2 | id_departamento | nombre           | presupuesto | gastos |
+---------+-----------+-----------+-----------------+------------------+-------------+--------+
| Aarón   | Rivero    | Gómez     |               1 | Desarrollo       |      120000 |   6000 |
| María   | Santana   | Moreno    |               1 | Desarrollo       |      120000 |   6000 |
| Marta   | Herrera   | Gil       |               1 | Desarrollo       |      120000 |   6000 |
| Adela   | Salas     | Díaz      |               2 | Sistemas         |      150000 |  21000 |
| Pilar   | Ruiz      | NULL      |               2 | Sistemas         |      150000 |  21000 |
| Juan    | Gómez     | López     |               2 | Sistemas         |      150000 |  21000 |
| Adolfo  | Rubio     | Flores    |               3 | Recursos Humanos |      280000 |  25000 |
| Pepe    | Ruiz      | Santana   |               3 | Recursos Humanos |      280000 |  25000 |
| Adrián  | Suárez    | NULL      |               4 | Contabilidad     |      110000 |   3000 |
| Marcos  | Loyola    | Méndez    |               5 | I+D              |      375000 | 380000 |
| Diego   | Flores    | Salas     |               5 | I+D              |      375000 | 380000 |
+---------+-----------+-----------+-----------------+------------------+-------------+--------+
```

**2.** Devuelve un listado con los empleados y los datos de los departamentos donde trabaja cada uno. Ordena el resultado, en primer lugar por el nombre del departamento (en orden alfabético) y en segundo lugar por los apellidos y el nombre de los empleados.

```sql
SELECT e.nombre, e.apellido1, e.apellido2, d.id_departamento, d.nombre, d.presupuesto, d.gastos
FROM empleado AS e, departamento AS d
WHERE e.id_departamento = d.id_departamento
ORDER BY d.nombre, e.apellido1, e.apellido2, e.nombre;
+---------+-----------+-----------+-----------------+------------------+-------------+--------+
| nombre  | apellido1 | apellido2 | id_departamento | nombre           | presupuesto | gastos |
+---------+-----------+-----------+-----------------+------------------+-------------+--------+
| Adrián  | Suárez    | NULL      |               4 | Contabilidad     |      110000 |   3000 |
| Marta   | Herrera   | Gil       |               1 | Desarrollo       |      120000 |   6000 |
| Aarón   | Rivero    | Gómez     |               1 | Desarrollo       |      120000 |   6000 |
| María   | Santana   | Moreno    |               1 | Desarrollo       |      120000 |   6000 |
| Diego   | Flores    | Salas     |               5 | I+D              |      375000 | 380000 |
| Marcos  | Loyola    | Méndez    |               5 | I+D              |      375000 | 380000 |
| Adolfo  | Rubio     | Flores    |               3 | Recursos Humanos |      280000 |  25000 |
| Pepe    | Ruiz      | Santana   |               3 | Recursos Humanos |      280000 |  25000 |
| Juan    | Gómez     | López     |               2 | Sistemas         |      150000 |  21000 |
| Pilar   | Ruiz      | NULL      |               2 | Sistemas         |      150000 |  21000 |
| Adela   | Salas     | Díaz      |               2 | Sistemas         |      150000 |  21000 |
+---------+-----------+-----------+-----------------+------------------+-------------+--------+

```

**3.** Devuelve un listado con el identificador y el nombre del departamento, solamente de aquellos departamentos que tienen empleados.

```sql
SELECT DISTINCT d.id_departamento, d.nombre
FROM empleado AS e, departamento AS d
WHERE e.id_departamento = d.id_departamento;
+-----------------+------------------+
| id_departamento | nombre           |
+-----------------+------------------+
|               1 | Desarrollo       |
|               2 | Sistemas         |
|               3 | Recursos Humanos |
|               4 | Contabilidad     |
|               5 | I+D              |
+-----------------+------------------+
```

**4.** Devuelve un listado con el identificador, el nombre del departamento y el valor del presupuesto actual del que dispone, solamente de aquellos departamentos que tienen empleados. El valor del presupuesto actual lo puede calcular restando al valor del presupuesto inicial (columna presupuesto) el valor de los gastos que ha generado (columna gastos).

```sql
SELECT DISTINCT d.id_departamento, d.nombre, (d.presupuesto-gastos) AS presupuesto_actual
FROM empleado AS e, departamento AS d
WHERE e.id_departamento = d.id_departamento;
+-----------------+------------------+--------------------+
| id_departamento | nombre           | presupuesto_actual |
+-----------------+------------------+--------------------+
|               1 | Desarrollo       |             114000 |
|               2 | Sistemas         |             129000 |
|               3 | Recursos Humanos |             255000 |
|               4 | Contabilidad     |             107000 |
|               5 | I+D              |              -5000 |
+-----------------+------------------+--------------------+
```

**5.** Devuelve el nombre del departamento donde trabaja el empleado que tiene el nit 38382980M.

```sql
SELECT d.nombre
FROM empleado AS e, departamento AS d
WHERE e.id_departamento = d.id_departamento AND e.nit = '38382980M' ;
+------------+
| nombre     |
+------------+
| Desarrollo |
+------------+
```

**6.** Devuelve el nombre del departamento donde trabaja el empleado Pepe Ruiz Santana.

```sql
SELECT d.nombre
FROM empleado AS e, departamento AS d
WHERE e.id_departamento = d.id_departamento AND e.nombre = 'Pepe' AND e.apellido1 = 'Ruiz' AND e.apellido2 = 'Santana';
+------------------+
| nombre           |
+------------------+
| Recursos Humanos |
+------------------+
```

**7.** Devuelve un listado con los datos de los empleados que trabajan en el departamento de I+D. Ordena el resultado alfabéticamente.

```sql
SELECT e.nombre, e.apellido1, e.apellido2, e.nit, e.id_departamento
FROM empleado AS e, departamento AS d
WHERE e.id_departamento = d.id_departamento AND e.id_departamento = 5
ORDER BY e.nombre ASC;
+--------+-----------+-----------+-----------+-----------------+
| nombre | apellido1 | apellido2 | nit       | id_departamento |
+--------+-----------+-----------+-----------+-----------------+
| Diego  | Flores    | Salas     | 46384486H |               5 |
| Marcos | Loyola    | Méndez    | 17087203C |               5 |
+--------+-----------+-----------+-----------+-----------------+
```

**8.** Devuelve un listado con los datos de los empleados que trabajan en el departamento de Sistemas, Contabilidad o I+D. Ordena el resultado alfabéticamente.

```sql
SELECT DISTINCT e.nombre, e.apellido1, e.apellido2, e.nit, e.id_departamento
FROM empleado AS e, departamento AS d
WHERE e.id_departamento = d.id_departamento AND e.id_departamento = 5 OR e.id_departamento = 2 OR e.id_departamento = 4
ORDER BY e.nombre ASC;
+---------+-----------+-----------+-----------+-----------------+
| nombre  | apellido1 | apellido2 | nit       | id_departamento |
+---------+-----------+-----------+-----------+-----------------+
| Adela   | Salas     | Díaz      | Y5575632D |               2 |
| Adrián  | Suárez    | NULL      | 77705545E |               4 |
| Diego   | Flores    | Salas     | 46384486H |               5 |
| Juan    | Gómez     | López     | 56399183D |               2 |
| Marcos  | Loyola    | Méndez    | 17087203C |               5 |
| Pilar   | Ruiz      | NULL      | 80576669X |               2 |
+---------+-----------+-----------+-----------+-----------------+
```

**9.** Devuelve una lista con el nombre de los empleados que tienen los departamentos que no tienen un presupuesto entre 100000 y 200000 euros.

```sql
SELECT e.nombre, e.apellido1, e.apellido2
FROM empleado AS e, departamento AS d
WHERE e.id_departamento = d.id_departamento AND d.presupuesto NOT BETWEEN 100000 AND 200000;
+--------+-----------+-----------+
| nombre | apellido1 | apellido2 |
+--------+-----------+-----------+
| Adolfo | Rubio     | Flores    |
| Pepe   | Ruiz      | Santana   |
| Marcos | Loyola    | Méndez    |
| Diego  | Flores    | Salas     |
+--------+-----------+-----------+
```

**10.** Devuelve un listado con el nombre de los departamentos donde existe algún empleado cuyo segundo apellido sea NULL. Tenga en cuenta que no debe mostrar nombres de departamentos que estén repetidos.

```sql
SELECT DISTINCT d.nombre
FROM empleado AS e, departamento AS d
WHERE e.id_departamento = d.id_departamento AND e.apellido2 IS NULL;
+--------------+
| nombre       |
+--------------+
| Contabilidad |
| Sistemas     |
+--------------+
```

