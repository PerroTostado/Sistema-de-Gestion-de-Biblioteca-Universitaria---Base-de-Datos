# Informe de Aplicación y Pasos de Normalización

> **Proyecto:** Modelo Relacional – Sistema de Gestión de Biblioteca
>
> **Estado del Proyecto:** `Normalizado hasta 5FN` | `6FN Omitida por Diseño (OLTP)`

## Resumen de Normalización

| Forma Normal | Estado | Estrategia / Acción Aplicada | 
| ----- | ----- | ----- | 
| **1FN (Primera Forma Normal)** | Cumplida | Atributos atómicos y claves primarias escalares simples. | 
| **2FN (Segunda Forma Normal)** | Cumplida | Ausencia de dependencias parciales en llaves compuestas. | 
| **3FN (Tercera Forma Normal)** | Cumplida | Depuración de redundancias (llaves foráneas repetidas) y eliminación de ciclos transitivos. | 
| **FNBC (Boyce-Codd)** | Cumplida | Validación de la llave artificial mediante la regla de negocio de coordenadas relativas. | 
| **4FN (Cuarta Forma Normal)** | Cumplida | Aislamiento de relaciones $N:M$ para evitar productos cartesianos. | 
| **5FN (Quinta Forma Normal)** | Cumplida | Preservación de la integridad transaccional sin pérdidas. | 
| **6FN (Sexta Forma Normal)** | Omitida | Desestimada conscientemente para optimizar el rendimiento en OLTP. | 

## 1. Primera Forma Normal (1FN)

> **Regla:** Todo atributo debe ser atómico, sin grupos de valores repetidos, y cada tabla debe contar con una Llave Primaria (PK).

* **Estado original:** El modelo cumplía con la 1FN de manera nativa.

* **Justificación:**

  Todas las tablas principales fueron creadas con identificadores únicos escalares (`ID_libro`, `ID_usuario`, etc.). Los atributos se restringieron a tipos de datos base. Por ejemplo, en las tablas `USUARIO` y `FISICA`, el campo `Telefono` se definió como un `INT` de valor único, bloqueando estructuralmente la posibilidad de insertar múltiples números separados por comas y garantizando la atomicidad.

## 2. Segunda Forma Normal (2FN)

> **Regla:** Cumplir la 1FN y garantizar que todos los atributos no clave dependan de la totalidad de la Llave Primaria compuesta, no solo de una parte de ella.

* **Estado original:** El modelo se encontraba en 2FN.

* **Justificación:**

  Las tablas con llaves primarias de una sola columna cumplen esta norma por defecto. Las únicas tablas con llaves compuestas en el diseño son las intermedias que resuelven relaciones $N:M$ (`ESCRIBE`, `CLASIFICA` y `PUBLICA`). Como estas se diseñaron como tablas de unión puras (solo contienen las llaves foráneas que las componen y carecen de atributos descriptivos adicionales), es matemáticamente imposible que existan dependencias parciales.

## 3. Tercera Forma Normal (3FN)

> **Regla:** Cumplir la 2FN y eliminar dependencias transitivas (ningún atributo no clave debe depender de otro atributo no clave).

### Decisiones y Cambios Aplicados

En esta etapa se realizaron tres intervenciones estructurales críticas sobre el diseño base:

1. **Depuración de Ejemplares (Redundancia de Sede):**

   * *Problema:* La tabla `EJEMPLARES` tenía asignada la llave `fk_BIBLIOTECA`. Sin embargo, el ejemplar ya contaba con `fk_Ubicación`, y dicha ubicación ya determinaba la biblioteca correspondiente.

   * *Solución:* Se eliminó la llave foránea `fk_BIBLIOTECA` de la tabla de ejemplares junto con las columnas manuales repetidas. La ubicación define implícitamente la sede.

2. **Ruptura del Ciclo en Préstamos:**

   * *Problema:* Se detectó un bucle transitivo generado automáticamente (`USUARIO` apuntaba a `EJEMPLARES`, `EJEMPLARES` a `RESERVA`, y `RESERVA` a `USUARIO`).

   * *Solución:* Se centralizó la transacción en la entidad `RESERVA`. Se eliminaron las llaves foráneas en los extremos y se integró `fk_EJEMPLARES` dentro de `RESERVA`. De esta manera, la reserva actúa como el puente transaccional puro que une **Quién**, **Cuándo** y **Qué ejemplar específico**.

3. **Historial de Sanciones:**

   * *Solución:* Para evitar la sobrescritura de datos, se descartó la opción de incrustar las infracciones directamente en `USUARIO`. Se creó la tabla independiente `SANCIONA` (con atributos propios como fechas y motivo), vinculada únicamente con `fk_USUARIO`. La biblioteca no se vinculó a la sanción, ya que el usuario, por regla de negocio, pertenece a una única sede.

## 4. Forma Normal de Boyce-Codd (FNBC / 3.5FN)

> **Regla:** Todo determinante debe ser una clave candidata (superclave).

* **Estado original:** El modelo cumple con la FNBC de manera nativa gracias a la regla de negocio espacial definida para la biblioteca.

### Justificación Técnica (Criterio de Coordenadas Relativas)

Se evaluó la tabla `Ubicación` (que contiene `Estanteria`, `Piso` y `Sección`) para identificar si alguno de sus campos era un determinante anómalo. 

Para este sistema, se hace énfasis en la disposición física de la biblioteca: **la numeración de las estanterías es relativa y se reinicia en cada nivel**. Es decir, las estanterías siempre empiezan por la 1, 2, 3, 4... sin importar en qué piso se encuentren. 

Bajo esta regla de negocio, el atributo `Estanteria` **no** funciona como un "súper atributo" determinante, ya que por sí solo no puede deducir en qué piso o sección se encuentra el ejemplar. Para identificar un punto físico real, se requiere obligatoriamente la combinación de todas las coordenadas. Esto elimina cualquier dependencia transitiva interna y confirma que el uso de la clave primaria artificial `Id_Ubicacion` es la decisión de diseño correcta para agrupar estas coordenadas, cumpliendo la 3.5FN a la perfección.

## 5. Cuarta (4FN) y Quinta Forma Normal (5FN)

> **Reglas:**
>
> * **4FN:** Eliminar dependencias multivaluadas independientes.
>
> * **5FN:** Eliminar dependencias de reunión cíclicas (*Join Dependencies*).

* **Estado:** Cumplidas de manera natural.

* **Justificación:**

  * **4FN:** Se garantizó al aislar todas las relaciones de granularidad Muchos a Muchos (`ESCRIBE`, `CLASIFICA`, `PUBLICA`) en sus propias tablas independientes, evitando la creación de productos cartesianos (por ejemplo, combinar múltiples autores con múltiples categorías en una sola fila).

  * **5FN:** Se alcanzó dado que transacciones como `RESERVA` operan sobre eventos temporales estrictos que no pueden descomponerse en subtablas (ej. separar *Usuario-Fecha* de *Ejemplar-Fecha*) sin generar registros espurios o pérdida del contexto histórico al ejecutar un `JOIN`.

## 6. Sexta Forma Normal (6FN)

> **Regla:** Descomponer las tablas hasta que cada relación conste únicamente de la Llave Primaria y, como máximo, un solo atributo no clave.
 
> ### Justificación Técnica

La **6FN** representa un nivel de descomposición extremo utilizado principalmente en bodegas de datos temporales (*Data Warehouses*). Aplicarla a un sistema transaccional en tiempo real (**OLTP**) como el de una biblioteca impactaría negativamente el rendimiento.

De haberse aplicado la 6FN, una entidad como `USUARIO` habría requerido ser fragmentada en múltiples tablas independientes:

* `USUARIO_NOMBRE` (`ID_usuario`, `Nombre`)

* `USUARIO_TELEFONO` (`ID_usuario`, `Telefono`)

* `USUARIO_DIRECCION` (`ID_usuario`, `Direccion`)

