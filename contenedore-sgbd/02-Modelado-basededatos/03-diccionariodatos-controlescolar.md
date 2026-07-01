# Diccionario de Datos de bases de datos control escolar

1. Informacion General

| Elemento 1 | Valor |
| :--- | :--- |
| Proyecto | Sistema de Control Escolar |
| Version | 1.0 |
| Fecha | Junio 2026 |
| Elaboro | Jimena Valdez Delgadillo |
| SGBD | SQLServer |

2. Descripcion del Sistema de Base de Datos

El sistema administra:

- Carreras
- Alumnos
- Profesores
- Materias
- Grupos
- Inscripciones

Permite controlar la oferta educativa y la inscripcion de los estudiantes

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

**Tabla:** Carrera

**Descripcion:** _Almacena las carreras ofertadas por la Universidad_

| Campo | Tipo | Longitud | Restricciones | Descripcion |
| :--- | :--- | :--- | :--- | :--- |
| id_carrera | INT | - | PK, AI, NN | Identificador unico de la carrera |
| nombre | VARCHAR | 100 | UQ, NN | Nombre de la carrera |
| duracion_cuatrimestre | INT | - | NN,CK(>0) | Duracion del cuatrimestre |

--- 



**Tabla:** Alumno

**Descripcion:** _Almacena la informacion de los estudiantes_

| Campo | Tipo | Longitud | Restricciones | Descripcion |
| :--- | :--- | :--- | :--- | :--- |
| id_alumno | INT | - | PK, AI, NN | Identificador unico del alumno |
| id_matricula | VARCHAR | 10 | UQ, NN | Matricula Institucional |
| nombre | VARCHAR | 50 | NN | Nombre del estudiante |
| apellido_paterno | VARCHAR | 50 | NN | Apellido Paterno |
| apellido_materno | VARCHAR | 50 | NULL | Apellido Materno |
| correo | VARCHAR | 100 | UQ, NN | Correo Institucional |
| fecha_nacimiento | DATE | - | NN | Fecha de Nacimiento |
| id_carrera | INT | - | FK, NN | Carrera a la que Pertenece |

---


5. Relaciones

| Relacion | Cardinalidad | Descripcion |
|:----------|:---------:|----------:|
| Carera -> Alumno    | 1:N    | Una carrera tiene muchos alumnos   |
| Carrera -> Materia   | 1:N    | Una carrera tiene muchas materias    |
| Profesor -> Grupo    | 1:N    | Un profesor puede impartir a varios grupos     |
| Materia -> Grupo    | 1:N    | Una materia puede abrirse en varios grupos   |
| Alumno -> Inscripcion    | 1:N    | Un alumno puede tener varias inscripciones    |
| Grupo -> Inscripcion    | 1:N    | Un grupo puede tener muchos alumnos     |


6. Matriz de Claves Foraneas 

| Tabla  | Campo Fk | Descripcion |
|:----------|:---------:|----------:|
| Alumno    | id_carrera    | Carrera (id_carrera)    |
| Materia   | id_carrera    | Carrera (id_carrera)    |
| Grupo    | id_profesor    | Profesor (id_profesor)   |
| Grupo    | id_materia    | Materia (id_profesor)   |
| Inscripcion | id_alumno | Alumno (id_alumno)   |
| Inscripcion | id_grupo   | Grupo (id_Grupo)   |

7. Integridad Referencial

| Regla  | Descripcion |
| :--- | :--- |
| IR-01 | No se puede registrar un alumno con una carrera inexistente |
| IR-02 | No se puede crear un grupo para una materia inexistente |
| IR-03 | No se puede crear un grupo con un profesor inexistente |

8. Reglas del Negocio

| Codigo  | Regla |
| :--- | :--- |
| RN-01 | Un alumno pertenece solo a sola carrera |
| RN-02 | Una carrera puede tener muchos alumnos |
| RN-03 | Una carrera puede tener muchas materias |



9. Diagrama Relacional


![Solucion Ejercicio 1](../img/ER/diagrama.png)
