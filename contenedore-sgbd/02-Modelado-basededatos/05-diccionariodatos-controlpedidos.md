# Diccionario de Datos de bases de datos control de pedidos

1. Informacion General

| Elemento 1 | Valor |
| :--- | :--- |
| Proyecto | Sistema de Ventas y Pedidos |
| Version | 1.0 |
| Fecha | Junio 2026 |
| Elaboro | Jimena Valdez Delgadillo |
| SGBD | SQLServer |

2. Descripcion del Sistema de Base de Datos

El sistema administra:

- Clientes
- Pedidos
- Productos
- Contenido de los pedidos (Relación de productos y cantidades)

Permite controlar el registro de clientes, el seguimiento de sus pedidos realizados y el inventario o desglose de productos que contiene cada uno.

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

**Tabla:** Cliente

**Descripcion:** _Almacena la información general de los clientes del sistema_

| Campo | Tipo | Longitud | Restricciones | Descripcion |
| :--- | :--- | :--- | :--- | :--- |
| IdCliente | INT | - | PK, NN | Identificador único del cliente |
| nombre | VARCHAR | 30 | NN | Nombre completo o razón social del cliente |

--- 

**Tabla:** Pedido

**Descripcion:** _Almacena las cabeceras de los pedidos realizados_

| Campo | Tipo | Longitud | Restricciones | Descripcion |
| :--- | :--- | :--- | :--- | :--- |
| NumPedido | INT | - | PK, NN | Identificador único del pedido |
| FechaPedido | INT | - | NN | Fecha en la que se generó el pedido (Almacenado como entero/timestamp según diagrama) |
| IdCliente | INT | - | FK, NN | Clave foránea que asocia el pedido al cliente que lo realizó |

---

**Tabla:** Contiene

**Descripcion:** _Tabla intermedia que detalla los productos incluidos en cada pedido y sus cantidades_

| Campo | Tipo | Longitud | Restricciones | Descripcion |
| :--- | :--- | :--- | :--- | :--- |
| NumeroPedido | INT | - | PK, FK, NN | Clave foránea del pedido y parte de la PK compuesta |
| NumProd | INT | - | PK, FK, NN | Clave foránea del producto y parte de la PK compuesta |
| Cantidad | INT | - | NN | Cantidad solicitada del producto en ese pedido |

---

**Tabla:** Producto

**Descripcion:** _Almacena el catálogo de productos disponibles en el sistema_

| Campo | Tipo | Longitud | Restricciones | Descripcion |
| :--- | :--- | :--- | :--- | :--- |
| NumProducto | INT | - | PK, NN | Identificador único del producto |
| NombreProd | VARCHAR | 30 | NN | Nombre comercial o descripción del producto |
| PrecioProd | DECIMAL | 10,2 | NN | Precio unitario del producto con dos posiciones decimales |

---

5. Relaciones

| Relacion | Cardinalidad | Descripcion |
|:----------|:---------:|----------:|
| Cliente -> Pedido     | 1:N     | Un cliente puede realizar muchos pedidos, pero un pedido pertenece a un solo cliente. |
| Pedido -> Contiene    | 1:N     | Un pedido puede contener múltiples líneas de detalles de productos. |
| Producto -> Contiene  | 1:N     | Un producto puede aparecer listado en múltiples registros de contenido de pedidos. |

6. Matriz de Claves Foraneas 

| Tabla  | Campo Fk | Descripcion |
|:----------|:---------:|----------:|
| Pedido    | IdCliente    | Cliente (IdCliente)    |
| Contiene  | NumeroPedido | Pedido (NumPedido)      |
| Contiene  | NumProd      | Producto (NumProducto)  |

7. Integridad Referencial

| Regla  | Descripcion |
| :--- | :--- |
| IR-01 | No se puede registrar un pedido para un cliente inexistente |
| IR-02 | No se puede asociar un producto inexistente al contenido de un pedido |
| IR-03 | No se puede asociar un detalle de producto a un número de pedido inexistente |

8. Reglas del Negocio

| Codigo  | Regla |
| :--- | :--- |
| RN-01 | Un pedido debe estar asociado obligatoriamente a un cliente |
| RN-02 | La cantidad especificada en la tabla Contiene debe ser un valor entero positivo mayor a cero |
| RN-03 | El precio de los productos se debe registrar estrictamente con dos decimales de precisión |


9. Diagrama Relacional

![Solucion](../../img/ER/pedidprod.jpeg)

10. Modelo relacional

![Solucion](../../img/Relacional/clientepedidomr.png)
