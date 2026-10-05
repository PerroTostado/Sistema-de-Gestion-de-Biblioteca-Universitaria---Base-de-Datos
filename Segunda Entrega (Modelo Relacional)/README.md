# Sistema de Gestión de Biblioteca Universitaria — Modelo relacional normalizado

**Entrega 2 — Base de Datos I**
Universidad Industrial de Santander · Facultad de Ingenierías Fisicomecánicas · Grupo G3[cite: 4]

A partir del modelo E-R de la primera entrega, construimos el modelo relacional del Sistema de Gestión de Biblioteca Universitaria: 20 tablas con su llave primaria, sus llaves foráneas y el tipo de dato de cada columna, normalizado hasta la quinta forma normal (5FN).

## Integrantes del grupo[cite: 4]

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
| Modelo relacional (Imagen) | Proyecto_Biblioteca_Relacional_Normalizado_5FN.jpg | Diagrama visual de las 20 tablas con sus relaciones, llaves primarias y foráneas. |
| Diccionario de Datos | README (4).md | Detalle completo de las tablas, tipos de datos (INT, CHAR, DATE, etc.) y descripciones de cada columna. |
| Informe de normalización | informe_de_normalizacion.md | Informe de aplicación y justificación de los pasos de normalización desde la 1FN hasta la decisión de omitir la 6FN. |

## Contenido

1. Paso del modelo E-R al modelo relacional
2. Modelo relacional
3. Normalización

### 1. Paso del modelo E-R al modelo relacional

Antes de normalizar, transformamos el diagrama E-R en tablas aplicando las siguientes reglas de mapeo:

| Elemento del E-R | Cómo lo pasamos a tablas | Ejemplo del proyecto |
| :--- | :--- | :--- |
| Entidad | Una tabla con su llave primaria (PK). | LIBRO, USUARIO, BIBLIOTECA |
| Relación 1:N | La llave foránea (FK) va en la tabla del lado con cardinalidad N. | EJEMPLARES recibe la llave de Ubicación, RESERVA recibe la llave de USUARIO |
| Relación N:M | Una tabla intermedia cuya PK está compuesta por las FK de las dos entidades. | CLASIFICA (une LIBRO y CATEGORIA), ESCRIBE (une LIBRO y AUTOR), PUBLICA (une EDITORIAL y LIBRO) |
| Especialización | Una tabla por subtipo, cuya PK es a la vez FK hacia el supertipo. | FISICO y VIRTUAL (para EJEMPLARES y BIBLIOTECA), ESTUDIANTE y DOCENTE (para USUARIO) |

### 2. Modelo relacional

El modelo completo de 20 tablas con el tipo de dato de cada columna se detalla en el diccionario de datos. Aquí lo resumimos en notación de esquema: la PK va en **negrita** y las FK van en *cursiva*.

#### 2.1 Libros, Autores y Editoriales
* **LIBRO**(**ID_libro**, Titulo, Idioma, Nro_paginas)
* **CATEGORIA**(**ID_categoria**, Nombre, Descripcion)
* **AUTOR**(**ID_autor**, Nombre, Fecha_nacimiento, Fecha_fallecido)
* **EDITORIAL**(**NIT**, Nombre, Pais)
* **CLASIFICA**(**fk_LIBRO**, **fk_CATEGORIA**)
* **ESCRIBE**(**fk_LIBRO**, **fk_AUTOR**)
* **PUBLICA**(**fk_EDITORIAL**, **fk_LIBRO**)

#### 2.2 Ejemplares y Ubicación Física
* **Ubicación**(**Id_Ubicacion**, Estanteria, Piso, Sección, *fk_BIBLIOTECA*)
* **EJEMPLARES**(**ID_ejemplar**, *fk_LIBRO*, *fk_Ubicación*)
* **FISICO (Ejemplar)**(**fk_EJEMPLARES**, Cod_barras, Estado, Cantidad)
* **VIRTUAL (Ejemplar)**(**fk_EJEMPLARES**, URL, Licencia)

#### 2.3 Usuarios y Bibliotecas (Sedes)
* **BIBLIOTECA**(**ID_sede**, Nombre)
* **FISICA (Sede)**(**fk_BIBLIOTECA**, Direccion, Telefono
