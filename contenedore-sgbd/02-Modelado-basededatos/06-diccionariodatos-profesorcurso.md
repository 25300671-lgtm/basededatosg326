# Diccionario de Datos de bases de datos profesor-curso

1. Informacion General

| Elemento 1 | Valor |
| :--- | :--- |
| Proyecto | Sistema de Control Escolar (Profesores) |
| Version | 1.0 |
| Fecha | Junio 2026 |
| Elaboro | Jimena Valdez Delgadillo |
| SGBD | SQLServer |

2. Descripcion del Sistema de Base de Datos

El sistema administra:

- Profesores
- Cursos
- Especialidades

Permite controlar la asignación de los cursos académicos a los profesores correspondientes y el registro de las especialidades profesionales de cada docente.

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

**Tabla:** Profesor

**Descripcion:** _Almacena la informacion de los profesores de la institucion_

| Campo | Tipo | Longitud | Restricciones | Descripcion |
| :--- | :--- | :--- | :--- | :--- |
| NumProf | INT | - | PK, NN | Identificador unico del profesor |
| Nombre | VARCHAR | 50 | NN | Nombre del profesor |
| Apellido1 | VARCHAR | 20 | NN | Primer apellido del profesor |
| Apellido2 | VARCHAR | 20 | NULL | Segundo apellido del profesor _(Nota: Corregido de Apellido1 repetido en el diagrama)_ |

--- 

**Tabla:** Curso

**Descripcion:** _Almacena la informacion de los cursos ofertados_

| Campo | Tipo | Longitud | Restricciones | Descripcion |
| :--- | :--- | :--- | :--- | :--- |
| NumCurso | INT | - | PK, NN | Identificador unico del curso |
| NombreCurso | VARCHAR | 20 | UQ, NN | Nombre unico del curso |
| Creditos | INT | - | NN | Creditos academicos del curso |
| NumProf | INT | - | FK, NN | Profesor que imparte el curso |

---

**Tabla:** Especialidad

**Descripcion:** _Almacena las especialidades asociadas a los profesores_

| Campo | Tipo | Longitud | Restricciones | Descripcion |
| :--- | :--- | :--- | :--- | :--- |
| NumEsp | INT | - | PK, NN | Identificador de la especialidad |
| NumProf | INT | - | PK, FK, NN | Clave foranea del profesor |
| Nombre | VARCHAR | 30 | NN | Nombre de la especialidad |

---

5. Relaciones

| Relacion | Cardinalidad | Descripcion |
|:----------|:---------:|----------:|
| Profesor -> Curso      | 1:N     | Un profesor puede impartir varios cursos   |
| Profesor -> Especialidad | 1:N     | Un profesor puede tener varias especialidades |

6. Matriz de Claves Foraneas 

| Tabla  | Campo Fk | Descripcion |
|:----------|:---------:|----------:|
| Curso      | NumProf   | Profesor (NumProf)   |
| Especialidad | NumProf   | Profesor (NumProf)   |

7. Integridad Referencial

| Regla  | Descripcion |
| :--- | :--- |
| IR-01 | No se puede asignar un curso a un profesor inexistente |
| IR-02 | No se puede registrar una especialidad para un profesor inexistente |

8. Reglas del Negocio

| Codigo  | Regla |
| :--- | :--- |
| RN-01 | Un profesor puede impartir múltiples cursos académicos |
| RN-02 | Un curso sólo puede ser impartido por un único profesor |
| RN-03 | Una especialidad se asocia obligatoriamente a un profesor registrado |

9. Diagrama Relacional

![Solucion](../../img/ER/profcur.jpeg)

10. Modelo relacional

![Solucion](../../img/Relacional/profcurso.jpeg)
