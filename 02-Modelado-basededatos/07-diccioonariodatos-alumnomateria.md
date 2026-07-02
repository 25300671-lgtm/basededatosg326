# Diccionario de Datos de bases de datos control escolar

1. Informacion General

| Elemento 1 | Valor |
| :--- | :--- |
| Proyecto | Sistema de Inscripción de Materias |
| Version | 1.0 |
| Fecha | Junio 2026 |
| Elaboro | Jimena Valdez Delgadillo |
| SGBD | SQLServer |

2. Descripcion del Sistema de Base de Datos

El sistema administra:

- Alumnos
- Materias
- Inscripciones (Relación histórica de calificaciones y fechas)

Permite controlar la oferta de materias vigentes, el registro académico de los estudiantes y el desglose de sus inscripciones con sus respectivas calificaciones finales.

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

**Tabla:** Alumno

**Descripcion:** _Almacena la información escolar y personal de los estudiantes_

| Campo | Tipo | Longitud | Restricciones | Descripcion |
| :--- | :--- | :--- | :--- | :--- |
| IdAlumno | INT | - | PK, NN | Identificador único del alumno |
| Matricula | VARCHAR | 10 | UQ, NN | Matrícula única institucional |
| Nombre | VARCHAR | 30 | NN | Nombre(s) del estudiante |
| Apellido1 | VARCHAR | 20 | NN | Primer apellido del alumno |
| Apellido2 | VARCHAR | 20 | NULL | Segundo apellido del alumno |
| Semestre | INT | - | NN, CK | Número de semestre asignado (Debe cumplir restricción Check) |

--- 

**Tabla:** Materia

**Descripcion:** _Almacena el catálogo de materias disponibles en el plan de estudios_

| Campo | Tipo | Longitud | Restricciones | Descripcion |
| :--- | :--- | :--- | :--- | :--- |
| IdMateria | INT | - | PK, NN | Identificador único de la materia |
| NombreMat | VARCHAR | 20 | UQ, NN | Nombre único de la materia |
| Creditos | INT | - | NN, CK | Cantidad de créditos asignados (Debe cumplir restricción Check) |

---

**Tabla:** Inscribe

**Descripcion:** _Tabla intermedia que registra las materias inscritas por cada alumno_

| Campo | Tipo | Longitud | Restricciones | Descripcion |
| :--- | :--- | :--- | :--- | :--- |
| IdMateria | INT | - | PK, FK, NN | Clave foránea de la materia y parte de la PK compuesta |
| IdAlumno | INT | - | PK, FK, NN | Clave foránea del alumno y parte de la PK compuesta |
| FechaInscripcion | DATE | - | NN | Fecha en la que se dio de alta la materia |
| CalFinal | DECIMAL | 4,2 | NN | Calificación definitiva obtenida en la materia |

---

5. Relaciones

| Relacion | Cardinalidad | Descripcion |
|:----------|:---------:|----------:|
| Alumno -> Inscribe   | 1:N     | Un alumno puede inscribir una o muchas materias. |
| Materia -> Inscribe  | 1:N     | Una materia puede ser inscrita por múltiples estudiantes. |

6. Matriz de Claves Foraneas 

| Tabla  | Campo Fk | Descripcion |
|:----------|:---------:|----------:|
| Inscribe  | Id


9. Diagrama Relacional

![Solucion](../../img/ER/alummat.jpeg)

10. Modelo relacional

![Solucion](../../img/Relacional/alumnomateria.png)
