# Diccionario de Datos de bases de datos control paciente

1. Informacion General

| Elemento 1 | Valor |
| :--- | :--- |
| Proyecto | Sistema de Expedientes Clínicos |
| Version | 1.0 |
| Fecha | Junio 2026 |
| Elaboro | Jimena Valdez Delgadillo |
| SGBD | SQLServer |

2. Descripcion del Sistema de Base de Datos

El sistema administra:

- Pacientes
- Expedientes Médicos

Permite controlar el registro de datos personales de los pacientes y la apertura de su expediente médico único en la institución de salud.

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

**Tabla:** Paciente

**Descripcion:** _Almacena los datos personales e identificativos de los pacientes_

| Campo | Tipo | Longitud | Restricciones | Descripcion |
| :--- | :--- | :--- | :--- | :--- |
| NumPaciente | INT | - | PK, NN | Identificador único del paciente |
| Nombre | VARCHAR | 30 | NN | Nombre(s) del paciente |
| Apellido1 | VARCHAR | 20 | NN | Primer apellido del paciente |
| Apellido2 | VARCHAR | 20 | NULL | Segundo apellido del paciente |
| FechaNaci | DATE | - | NN | Fecha de nacimiento del paciente |

--- 

**Tabla:** Expediente

**Descripcion:** _Almacena la información de control clínico y apertura del expediente del paciente_

| Campo | Tipo | Longitud | Restricciones | Descripcion |
| :--- | :--- | :--- | :--- | :--- |
| NumExp | INT | - | PK, NN | Identificador único del expediente médico |
| FechaApertura | DATE | - | NN | Fecha en la que se dio de alta el expediente |
| TipodeSangre | CHAR | 3 | NN | Grupo sanguíneo y factor Rh del paciente (ej. 'O+', 'AB-') |
| NumPaciente | INT | - | FK, UQ, NN | Clave foránea única que vincula el expediente con un solo paciente |

---

5. Relaciones

| Relacion | Cardinalidad | Descripcion |
|:----------|:---------:|----------:|
| Paciente -> Expediente | 1:1 | Un paciente posee un único expediente clínico, y cada expediente pertenece exclusivamente a un paciente. |

6. Matriz de Claves Foraneas 

| Tabla  | Campo Fk | Descripcion |
|:----------|:---------:|----------:|
| Expediente | NumPaciente | Paciente (NumPaciente) |

7. Integridad Referencial

| Regla  | Descripcion |
| :--- | :--- |
| IR-01 | No se puede crear un expediente clínico para un paciente que no se encuentre registrado previamente en el sistema |

8. Reglas del Negocio

| Codigo  | Regla |
| :--- | :--- |
| RN-01 | Cada paciente tiene derecho a un único expediente clínico dentro de la institución (Relación 1 a 1 impuesta por la restricción UNIQUE) |
| RN-02 | El tipo de sangre debe ser registrado de forma obligatoria siguiendo la nomenclatura clínica estándar |


9. Diagrama Relacional

![Solucion](../../img/ER/pacienteExpedieenteEr.jpeg)

10. Modelo relacional

![Solucion](../../img/Relacional/PacienteExpediente.png)
