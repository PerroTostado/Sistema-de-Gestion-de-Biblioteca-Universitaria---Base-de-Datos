# Sistema de Gestión de Biblioteca Universitaria — Modelo relacional normalizado

**Entrega 2 — Base de Datos I**
Universidad Industrial de Santander · Facultad de Ingenierías Fisicomecánicas · Grupo G3[cite: 4]

A partir del modelo E-R de la primera entrega, construimos el modelo relacional del Sistema de Gestión de Biblioteca Universitaria: 20 tablas con su llave primaria, sus llaves foráneas y el tipo de dato de cada columna, normalizado hasta la quinta forma normal (5FN).

## Integrantes del grupo

| # | Nombre completo | Código |
| :--- | :--- | :--- |
| 1 | Juan Camilo Hernández Parra | 2250174 |
| 2 | Bramdon Julián González Velandia | 2250196 |
| 3 | Jhulian Stewar Prieto Zuluaga | 2251751 |
| 4 | Nicolas Soto Sánchez | 2250145 |
| 5 | Nicolas David Sanguino Ortiz | 2250157 |

## Archivos

| Archivo | Ruta / Nombre | Descripción |
| :--- | :--- | :--- |
| Imagen del Modelo relacional | [Proyecto_Biblioteca_Relacional_Normalizado_5FN](https://github.com/PerroTostado/Sistema-de-Gestion-de-Biblioteca-Universitaria---Base-de-Datos/blob/8ce7e7448f5e3f0b659cfdaacafbdec3f8a2d2f5/Segunda%20Entrega%20(Modelo%20Relacional)/Modelo%20Relacional%20Normalizado/Proyecto_Biblioteca_Relacional_Normalizado_5FN.png) | Diagrama visual con: 20 tablas, relaciones, PK's y FK's. |
| Diccionario de Datos | [diccionario_de_datos.md](https://github.com/PerroTostado/Sistema-de-Gestion-de-Biblioteca-Universitaria---Base-de-Datos/blob/8ce7e7448f5e3f0b659cfdaacafbdec3f8a2d2f5/Segunda%20Entrega%20(Modelo%20Relacional)/Modelo%20Relacional%20Normalizado/diccionario_de_datos.md)| Detalle completo de las tablas, tipos de datos (INT, CHAR, DATE, etc.) y descripciones de cada columna. |
| Informe de normalización | [informe_de_normalizacion](https://github.com/PerroTostado/Sistema-de-Gestion-de-Biblioteca-Universitaria---Base-de-Datos/blob/8ce7e7448f5e3f0b659cfdaacafbdec3f8a2d2f5/Segunda%20Entrega%20(Modelo%20Relacional)/Informe%20de%20Aplicaci%C3%B3n%20de%20los%20Pasos%20de%20Normalizaci%C3%B3n/informe_de_normalizacion.md) | Informe de aplicación y justificación de los pasos de normalización desde la 1FN hasta la decisión de omitir la 6FN. |

## Contenido

1. [Modelo relacional](#1-Modelo_relacional)
2. [Normalización](#-Normalización)

--- 
### 1. Modelo relacional

El modelo completo de 20 tablas con el tipo de dato de cada columna se detalla en el diccionario de datos. Aquí lo resumimos en notación de esquema: la PK va en **negrita** y las FK van en *cursiva*.

#### 1.1 Libros, Autores y Editoriales
* **LIBRO**(**ID_libro**, Titulo, Idioma, Nro_paginas)
* **CATEGORIA**(**ID_categoria**, Nombre, Descripcion)
* **AUTOR**(**ID_autor**, Nombre, Fecha_nacimiento, Fecha_fallecido)
* **EDITORIAL**(**NIT**, Nombre, Pais)
* **CLASIFICA**(**fk_LIBRO**, **fk_CATEGORIA**)
* **ESCRIBE**(**fk_LIBRO**, **fk_AUTOR**)
* **PUBLICA**(**fk_EDITORIAL**, **fk_LIBRO**)

#### 1.2 Ejemplares y Ubicación Física
* **Ubicación**(**Id_Ubicacion**, Estanteria, Piso, Sección, *fk_BIBLIOTECA*)
* **EJEMPLARES**(**ID_ejemplar**, *fk_LIBRO*, *fk_Ubicación*)
* **FISICO (Ejemplar)**(**fk_EJEMPLARES**, Cod_barras, Estado, Cantidad)
* **VIRTUAL (Ejemplar)**(**fk_EJEMPLARES**, URL, Licencia)

#### 1.3 Usuarios y Bibliotecas (Sedes)
* **BIBLIOTECA**(**ID_sede**, Nombre)
* **FISICA (Sede)**(**fk_BIBLIOTECA**, Direccion, Telefono)
* **VIRTUAL (Sede)**(**fk_BIBLIOTECA**, Ubicacion_web)
* **USUARIO**(**ID_usuario**, Nombre, Telefono, Dirección, *fk_BIBLIOTECA*)
* **ESTUDIANTE**(**fk_USUARIO**)
* **DOCENTE**(**fk_USUARIO**)

#### 1.4 Préstamos, Renovaciones y Sanciones
* **RESERVA**(**ID_reserva**, Fecha_prestamo, Fecha_devolucion, *fk_USUARIO*, *fk_EJEMPLARES*)
* **RENOVARSE**(**ID_renovacion**, Fecha_solicitud, Fecha_vencimiento, *fk_RESERVA*)
* **Sanciona**(**ID_Sancion**, Fecha_inicio, Fecha_fin, Motivo, *fk_USUARIO*)

### 2. Normalización

El modelo fue sometido a evaluación y refactorización transaccional (OLTP). Este es el resumen de la aplicación de las formas normales:

| Forma Normal | Implementación | Utilidad sobre el proyecto |
| :--- | :--- | :--- |
| **1FN** | Implementado | Garantizamos atributos atómicos (ej. el Teléfono en USUARIO es un único valor INT) y aseguramos que cada tabla cuente con una Llave Primaria escalar simple. |
| **2FN** | Implementado | Revisamos las tablas con llave compuesta (ESCRIBE, CLASIFICA, PUBLICA) y confirmamos la ausencia de dependencias parciales, ya que son tablas de unión puras sin atributos descriptivos. |
| **3FN** | Implementado | Refactorizamos dependencias transitivas: eliminamos `fk_BIBLIOTECA` de EJEMPLARES (ya determinada por la Ubicación), rompimos el bucle transitivo centralizando la operación en RESERVA, y separamos el historial en la tabla independiente SANCIONA. |
| **FNBC** | Implementado | Evaluamos los determinantes de espacio físico en Ubicación para garantizar que la clave elegida (Id_Ubicacion vs ID_Estanteria) fuera un determinante válido y único para las coordenadas físicas. |
| **4FN** | Implementado | Aislamos las relaciones de granularidad N:M en sus propias tablas independientes para evitar la generación de productos cartesianos (combinaciones falsas repetidas). |
| **5FN** | Implementado | Preservamos la integridad transaccional asegurando que eventos temporales dependientes (como RESERVA) no se descompongan en subtablas con pérdida de contexto histórico. |
| **6FN** | Rechazado | Decidimos omitirla intencionalmente. Fragmentar USUARIO en múltiples tablas (nombre, teléfono, dirección) impactaría negativamente el rendimiento mediante exceso de consultas JOIN, siendo inviable para nuestra arquitectura OLTP. |

Conclusión: nuestro modelo relacional final consta de 20 tablas estructuradas e interconectadas, cumpliendo rigurosamente hasta la quinta forma normal (5FN), el nivel óptimo para garantizar la integridad y el rendimiento del Sistema de Gestión de Biblioteca.
