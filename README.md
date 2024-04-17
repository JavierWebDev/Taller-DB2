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
    presupuesto DOUBLE NOT NULL
);

CREATE TABLE empleado (
    id_empleado INT(10) PRIMARY KEY,
    nit VARCHAR(9) NOT NULL,
    nombre VARCHAR(100) NOT NULL,
    apellido1 VARCHAR(100) NOT NULL,
    apellido2 VARCHAR(100) NOT NULL,
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
SELECT id_empleado, LEFT(nit, 8) AS nit_digitos, SUBSTRING(nit, -1) AS nit_letra
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
ORDER BY nombre_completo
```

