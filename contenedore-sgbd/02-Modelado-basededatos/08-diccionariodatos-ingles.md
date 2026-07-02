# Diccionario de Datos de bases de datos empleados y departamentos(ingles)

1. Informacion General

| Elemento 1 | Valor |
| :--- | :--- |
| Proyecto | Sistema de Gestión de Empleados y Departamentos |
| Version | 1.0 |
| Fecha | Junio 2026 |
| Elaboro | Jimena Valdez Delgadillo |
| SGBD | SQLServer |

2. Descripcion del Sistema de Base de Datos

El sistema administra:

- Empleados (Employee)
- Departamentos (Department)
- Ubicaciones de los Departamentos (Locations)
- Dependientes de los Empleados (Dependent)
- Proyectos (Projects)
- Participación de Empleados en Proyectos (Works_On)

Permite controlar la estructura interna de una organización, asignando empleados a departamentos, registrando jefes directos, gestionando los proyectos asignados y manteniendo el control de los dependientes o familiares de cada trabajador.

3. Catalogo de Restricciones 

| Codigo  | Significado |
| :--- | :--- |
| PK | Primary key |
| FK | Foreign key |
| NN | Not Null |
| UQ | Unique |
| AI | Auto increment |
| CK | Check |
| DF | Default |

4. Diccionario de Datos

**Tabla:** Employee

**Descripcion:** _Almacena los datos personales, de nómina y laborales de los empleados_

| Campo | Tipo | Longitud | Restricciones | Descripcion |
| :--- | :--- | :--- | :--- | :--- |
| Ssn | INT | - | PK, NN | Número de seguridad social (Identificador único del empleado) |
| FirstName | VARCHAR | 30 | NN | Primer nombre del empleado |
| LastName | VARCHAR | 30 | NN | Apellido del empleado |
| Address | VARCHAR | 100 | NULL | Dirección de residencia |
| Bdate | DATE | - | NULL | Fecha de nacimiento |
| Salary | DECIMAL | 10,2 | NULL | Salario asignado |
| Sex | CHAR | 1 | NULL | Género del empleado |
| Jef_fk | INT | - | FK, NULL | Clave foránea reflexiva que referencia al Ssn del jefe directo |
| NumberDep | INT | - | FK, NN | Número del departamento al que pertenece |
| NameDep_fk | VARCHAR | 50 | FK, NN | Nombre del departamento al que pertenece |

--- 

**Tabla:** Department

**Descripcion:** _Almacena la información operativa de los departamentos de la empresa_

| Campo | Tipo | Longitud | Restricciones | Descripcion |
| :--- | :--- | :--- | :--- | :--- |
| Number | INT | - | PK, NN | Número identificador del departamento |
| Name | VARCHAR | 50 | UQ, NN | Nombre único del departamento |
| Manager_fk | INT | - | FK, UQ, NN | Clave foránea del Ssn del empleado que administra el departamento |
| StartDate | DATE | - | NULL | Fecha en la que el manager tomó el cargo |

---

**Tabla:** Locations

**Descripcion:** _Registra las diferentes locaciones físicas o sedes que posee un departamento_

| Campo | Tipo | Longitud | Restricciones | Descripcion |
| :--- | :--- | :--- | :--- | :--- |
| NumLocation | INT | - | PK, NN | Identificador de la ubicación (Parte de la PK compuesta) |
| NumberDep | INT | - | PK, FK, NN | Número del departamento asociado |
| NameDep_fk | VARCHAR | 50 | PK, FK, NN | Nombre del departamento asociado |
| Location | VARCHAR | 50 | NN | Dirección o zona geográfica de la locación |

---

**Tabla:** Dependent

**Descripcion:** _Almacena los datos de los familiares o dependientes de los empleados para beneficios_

| Campo | Tipo | Longitud | Restricciones | Descripcion |
| :--- | :--- | :--- | :--- | :--- |
| Name | VARCHAR | 50 | PK, NN | Nombre del dependiente (Parte de la PK compuesta) |
| Ssn_fk | INT | - | PK, FK, NN | Clave foránea del Ssn del empleado asociado |
| Sex | CHAR | 1 | NULL | Género del dependiente |
| RelationShip | VARCHAR | 30 | NULL | Parentesco con el empleado (ej. Hijo, Esposa, etc.) |

---

**Tabla:** Projects

**Descripcion:** _Almacena los proyectos desarrollados o coordinados por la empresa_

| Campo | Tipo | Longitud | Restricciones | Descripcion |
| :--- | :--- | :--- | :--- | :--- |
| Name | VARCHAR | 50 | UQ, NN | Nombre único del proyecto |
| Number | INT | - | PK, NN | Identificador único del proyecto |
| Location | VARCHAR | 50 | NULL | Ubicación geográfica donde se ejecuta el proyecto |

---

**Tabla:** Works_On

**Descripcion:** _Tabla intermedia que registra las horas de trabajo y asignación de empleados a proyectos_

| Campo | Tipo | Longitud | Restricciones | Descripcion |
| :--- | :--- | :--- | :--- | :--- |
| Ssn_fk | INT | - | PK, FK, NN | Clave foránea del Ssn del empleado |
| NameProj_fk | VARCHAR | 50 | PK, FK, NN | Clave foránea del nombre del proyecto |
| NumberProj_fk | INT | - | PK, FK, NN | Clave foránea del número del proyecto |

---

5. Relaciones

| Relacion | Cardinalidad | Descripcion |
|:----------|:---------:|----------:|
| Department -> Employee   | 1:N     | Un departamento tiene muchos empleados inscritos. |
| Employee -> Department   | 1:1     | Un empleado puede dirigir (ser Manager) de un único departamento. |
| Employee -> Employee     | 1:N     | Un empleado (Jefe) puede supervisar a varios empleados subordinados. |
| Department -> Locations  | 1:N     | Un departamento puede estar distribuido en múltiples locaciones. |
| Employee -> Dependent    | 1:N     | Un empleado puede tener registrados múltiples dependientes. |
| Employee -> Works_On     | 1:N     | Un empleado puede trabajar en muchos proyectos. |
| Projects -> Works_On     | 1:N     | Un proyecto cuenta con la participación de muchos empleados. |

6. Matriz de Claves Foraneas 

| Tabla  | Campo Fk | Descripcion |
|:----------|:---------:|----------:|
| Employee  | Jef_fk       | Employee (Ssn) |
| Employee  | NumberDep, NameDep_fk | Department (Number, Name) |
| Department| Manager_fk   | Employee (Ssn) |
| Locations | NumberDep, NameDep_fk | Department (Number, Name) |
| Dependent | Ssn_fk       | Employee (Ssn) |
| Works_On  | Ssn_fk       | Employee (Ssn) |
| Works_On  | NameProj_fk, NumberProj_fk | Projects (Name, Number) |

7. Integridad Referencial

| Regla  | Descripcion |
| :--- | :--- |
| IR-01 | No se puede asignar un empleado a un departamento que no exista |
| IR-02 | No se puede registrar un jefe directo (Jef_fk) que no esté dado de alta como empleado |
| IR-03 | No se puede asignar un manager a un departamento si el empleado no existe |
| IR-04 | Las ubicaciones de los departamentos deben ligarse obligatoriamente a registros vigentes de Department |
| IR-05 | No se puede registrar un dependiente si no está vinculado a un Ssn de empleado válido |
| IR-06 | Los registros de la tabla Works_On requieren que tanto el empleado como el proyecto existan previamente |

8. Reglas del Negocio

| Codigo  | Regla |
| :--- | :--- |
| RN-01 | El campo Manager_fk es de tipo UNIQUE, garantizando que un empleado solo pueda dirigir un departamento a la vez |
| RN-02 | El nombre de cada departamento (Name) y el nombre de cada proyecto (Name) son únicos e irrepetibles en toda la base de datos |
| RN-03 | La clave primaria de las entidades débiles (Locations, Dependent y Works_On) se conforma de manera compuesta en combinación con la clave de su entidad padre |


9. Diagrama Relacional

![Solucion](../../img/ER/ingl.jpeg)

10. Modelo relacional

![Solucion](../../img/Relacional/ingleselaboradomr.png)
