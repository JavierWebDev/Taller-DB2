# Taller 2 Bases De Datos

## Creacion Base De Datos

```sql
-- Creacion de la DB principal
CREATE DATABASE gestor_empleados;

-- Ingresar a la DB
USE gestor_empleados;

-- Creacion de Tablas
CREATE TABLE departamento (
	codigo INT(10) PRIMARY KEY,
    nombre VARCHAR(100),
    presupuesto DOUBLE
);

CREATE TABLE empleado (
    codigo INT(10),
    nit VARCHAR(9),
    nombre VARCHAR(100),
    apellido1 VARCHAR(100),
    apellido2 VARCHAR(100),
    codigo_departamento INT(10)
    CONSTRAINT FK_CodigoDepartamento FOREIGN KEY (codigo_departamento) REFERENCES departamento(codigo)
)
```



## Consultas Sobre Una Tabla

**1.** Lista el primer apellido de todos los empleados

```sql
SELECT apellido1
FROM empleado;
```

**2.** Lista el primer apellido de los empleados eliminando los apellidos que estén repetidos.

```sql
SELECT DISTINCT apellido1
FROM empleado;
```

**3.** Lista todas las columnas de la tabla empleado.

```sql
SELECT codigo, nit, nombre, apellido, apellido1, apellido2, codigo_departamento
FROM empleado;
```

**4.** Lista el nombre y los apellidos de todos los empleados.

```sql
SELECT nombre, apellido, apellido1, apellido2
FROM empleado;
```

**5.** Lista el identificador de los departamentos de los empleados que aparecen en la tabla empleado.

```sql
SELECT codigo_departamento
FROM empleado
```

**6.**