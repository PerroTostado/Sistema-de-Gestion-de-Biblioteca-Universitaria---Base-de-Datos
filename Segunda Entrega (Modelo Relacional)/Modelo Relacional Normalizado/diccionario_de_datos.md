# Diccionario de Datos del Esquema Relacional

> **Proyecto:** Sistema de Gestión de Biblioteca (proyecto_sanguino)

---

## Índice de Tablas

1. [LIBRO](#1-libro)
2. [CLASIFICA](#2-clasifica)
3. [CATEGORIA](#3-categoria)
4. [ESCRIBE](#4-escribe)
5. [AUTOR](#5-autor)
6. [PUBLICA](#6-publica)
7. [EDITORIAL](#7-editorial)
8. [EJEMPLARES](#8-ejemplares)
9. [FISICO](#9-fisico)
10. [VIRTUAL (Ejemplares)](#10-virtual-ejemplares)
11. [USUARIO](#11-usuario)
12. [RESERVA](#12-reserva)
13. [RENOVARSE](#13-renovarse)
14. [ESTUDIANTE](#14-estudiante)
15. [DOCENTE](#15-docente)
16. [BIBLIOTECA](#16-biblioteca)
17. [FISICA (Biblioteca)](#17-fisica-biblioteca)
18. [VIRTUAL (Biblioteca)](#18-virtual-biblioteca)
19. [Ubicación](#19-ubicación)
20. [Sanciona](#20-sanciona)

---

### 1. LIBRO

| Columna | Tipo de Dato | Llave Primaria (PK) | Llave Foránea (FK) | Descripción / Referencia |
| :--- | :--- | :---: | :---: | :--- |
| **ID_libro** | `INT` | Si | No | Identificador único del libro |
| **Titulo** | `CHAR(n)` | No | No | Título de la obra |
| **Idioma** | `CHAR(n)` | No | No | Idioma del libro |
| **Nro_paginas** | `INT` | No | No | Cantidad total de páginas |

---

### 2. CLASIFICA

> *Tabla intermedia (Relación $N:M$ entre LIBRO y CATEGORIA)*

| Columna | Tipo de Dato | Llave Primaria (PK) | Llave Foránea (FK) | Descripción / Referencia |
| :--- | :--- | :---: | :---: | :--- |
| **fk_LIBRO** | `INT` | Si | Si | Referencia a `LIBRO(ID_libro)` |
| **fk_CATEGORIA** | `INT` | Si | Si | Referencia a `CATEGORIA(ID_categoria)` |

---

### 3. CATEGORIA

| Columna | Tipo de Dato | Llave Primaria (PK) | Llave Foránea (FK) | Descripción / Referencia |
| :--- | :--- | :---: | :---: | :--- |
| **ID_categoria** | `INT` | Si | No | Identificador único de la categoría |
| **Nombre** | `CHAR(n)` | No | No | Nombre de la categoría |
| **Descripcion** | `CHAR(n)` | No | No | Descripción detallada |

---

### 4. ESCRIBE

> *Tabla intermedia (Relación $N:M$ entre LIBRO y AUTOR)*

| Columna | Tipo de Dato | Llave Primaria (PK) | Llave Foránea (FK) | Descripción / Referencia |
| :--- | :--- | :---: | :---: | :--- |
| **fk_LIBRO** | `INT` | Si | Si | Referencia a `LIBRO(ID_libro)` |
| **fk_AUTOR** | `INT` | Si | Si | Referencia a `AUTOR(ID_autor)` |

---

### 5. AUTOR

| Columna | Tipo de Dato | Llave Primaria (PK) | Llave Foránea (FK) | Descripción / Referencia |
| :--- | :--- | :---: | :---: | :--- |
| **ID_autor** | `INT` | Si | No | Identificador único del autor |
| **Nombre** | `CHAR(n)` | No | No | Nombre completo del autor |
| **Fecha_nacimiento** | `DATE` | No | No | Fecha de nacimiento |
| **Fecha_fallecido** | `DATE` | No | No | Fecha de fallecimiento (opcional) |

---

### 6. PUBLICA

> *Tabla intermedia (Relación $N:M$ entre EDITORIAL y LIBRO)*

| Columna | Tipo de Dato | Llave Primaria (PK) | Llave Foránea (FK) | Descripción / Referencia |
| :--- | :--- | :---: | :---: | :--- |
| **fk_EDITORIAL** | `INT` | Si | Si | Referencia a `EDITORIAL(NIT)` |
| **fk_LIBRO** | `INT` | Si | Si | Referencia a `LIBRO(ID_libro)` |

---

### 7. EDITORIAL

| Columna | Tipo de Dato | Llave Primaria (PK) | Llave Foránea (FK) | Descripción / Referencia |
| :--- | :--- | :---: | :---: | :--- |
| **NIT** | `INT` | Si | No | Número de identificación tributaria |
| **Nombre** | `CHAR(n)` | No | No | Nombre comercial de la editorial |
| **Pais** | `CHAR(n)` | No | No | País de origen |

---

### 8. EJEMPLARES

| Columna | Tipo de Dato | Llave Primaria (PK) | Llave Foránea (FK) | Descripción / Referencia |
| :--- | :--- | :---: | :---: | :--- |
| **ID_ejemplar** | `INT` | Si | No | Identificador único del ejemplar |
| **fk_LIBRO** | `INT` | No | Si | Referencia a `LIBRO(ID_libro)` |
| **fk_Ubicación** | `INT` | No | Si | Referencia a `Ubicación(Id_Ubicacion)` |

---

### 9. FISICO

> *Subtipo de EJEMPLARES (Ejemplares físicos)*

| Columna | Tipo de Dato | Llave Primaria (PK) | Llave Foránea (FK) | Descripción / Referencia |
| :--- | :--- | :---: | :---: | :--- |
| **fk_EJEMPLARES** | `INT` | Si | Si | Referencia a `EJEMPLARES(ID_ejemplar)` |
| **Cod_barras** | `INT` | No | No | Código de barras físico |
| **Estado** | `CHAR(n)` | No | No | Estado de conservación |
| **Cantidad** | `INT` | No | No | Stock o unidades disponibles |

---

### 10. VIRTUAL (Ejemplares)

> *Subtipo de EJEMPLARES (Ejemplares digitales)*

| Columna | Tipo de Dato | Llave Primaria (PK) | Llave Foránea (FK) | Descripción / Referencia |
| :--- | :--- | :---: | :---: | :--- |
| **fk_EJEMPLARES** | `INT` | Si | Si | Referencia a `EJEMPLARES(ID_ejemplar)` |
| **URL** | `CHAR(n)` | No | No | Enlace de acceso digital |
| **Licencia** | `CHAR(n)` | No | No | Tipo o clave de licencia |

---

### 11. USUARIO

| Columna | Tipo de Dato | Llave Primaria (PK) | Llave Foránea (FK) | Descripción / Referencia |
| :--- | :--- | :---: | :---: | :--- |
| **ID_usuario** | `INT` | Si | No | Identificador único del usuario |
| **Nombre** | `CHAR(n)` | No | No | Nombre completo |
| **Telefono** | `INT` | No | No | Número telefónico de contacto |
| **Dirección** | `CHAR(n)` | No | No | Dirección de residencia |
| **fk_BIBLIOTECA** | `INT` | No | Si | Sede principal asignada `BIBLIOTECA(ID_sede)` |

---

### 12. RESERVA

| Columna | Tipo de Dato | Llave Primaria (PK) | Llave Foránea (FK) | Descripción / Referencia |
| :--- | :--- | :---: | :---: | :--- |
| **ID_reserva** | `INT` | Si | No | Identificador único del préstamo/reserva |
| **Fecha_prestamo** | `DATE` | No | No | Fecha en la que se realiza la reserva |
| **Fecha_devolucion** | `DATE` | No | No | Fecha pactada de entrega |
| **fk_USUARIO** | `INT` | No | Si | Referencia a `USUARIO(ID_usuario)` |
| **fk_EJEMPLARES** | `INT` | No | Si | Referencia a `EJEMPLARES(ID_ejemplar)` |

---

### 13. RENOVARSE

| Columna | Tipo de Dato | Llave Primaria (PK) | Llave Foránea (FK) | Descripción / Referencia |
| :--- | :--- | :---: | :---: | :--- |
| **ID_renovacion** | `INT` | Si | No | Identificador único de renovación |
| **Fecha_solicitud** | `DATE` | No | No | Fecha en que se solicita la prórroga |
| **Fecha_vencimiento** | `DATE` | No | No | Nueva fecha límite de devolución |
| **fk_RESERVA** | `INT` | No | Si | Referencia a `RESERVA(ID_reserva)` |

---

### 14. ESTUDIANTE

> *Especialización del rol de USUARIO*

| Columna | Tipo de Dato | Llave Primaria (PK) | Llave Foránea (FK) | Descripción / Referencia |
| :--- | :--- | :---: | :---: | :--- |
| **fk_USUARIO** | `INT` | Si | Si | Referencia a `USUARIO(ID_usuario)` |

---

### 15. DOCENTE

> *Especialización del rol de USUARIO*

| Columna | Tipo de Dato | Llave Primaria (PK) | Llave Foránea (FK) | Descripción / Referencia |
| :--- | :--- | :---: | :---: | :--- |
| **fk_USUARIO** | `INT` | Si | Si | Referencia a `USUARIO(ID_usuario)` |

---

### 16. BIBLIOTECA

| Columna | Tipo de Dato | Llave Primaria (PK) | Llave Foránea (FK) | Descripción / Referencia |
| :--- | :--- | :---: | :---: | :--- |
| **ID_sede** | `INT` | Si | No | Identificador de la sede |
| **Nombre** | `CHAR(n)` | No | No | Nombre de la biblioteca o sede |

---

### 17. FISICA (Biblioteca)

> *Subtipo de BIBLIOTECA (Sede física)*

| Columna | Tipo de Dato | Llave Primaria (PK) | Llave Foránea (FK) | Descripción / Referencia |
| :--- | :--- | :---: | :---: | :--- |
| **fk_BIBLIOTECA** | `INT` | Si | Si | Referencia a `BIBLIOTECA(ID_sede)` |
| **Direccion** | `CHAR(n)` | No | No | Ubicación geográfica |
| **Telefono** | `INT` | No | No | Teléfono de contacto de la sede |

---

### 18. VIRTUAL (Biblioteca)

> *Subtipo de BIBLIOTECA (Sede virtual)*

| Columna | Tipo de Dato | Llave Primaria (PK) | Llave Foránea (FK) | Descripción / Referencia |
| :--- | :--- | :---: | :---: | :--- |
| **fk_BIBLIOTECA** | `INT` | Si | Si | Referencia a `BIBLIOTECA(ID_sede)` |
| **Ubicacion_web** | `CHAR(n)` | No | No | URL o portal web de la sede |

---

### 19. Ubicación

| Columna | Tipo de Dato | Llave Primaria (PK) | Llave Foránea (FK) | Descripción / Referencia |
| :--- | :--- | :---: | :---: | :--- |
| **Id_Ubicacion** | `INT` | Si | No | Identificador único de ubicación |
| **Estanteria** | `INT` | No | No | Número de estantería |
| **Piso** | `INT` | No | No | Número de piso |
| **Sección** | `INT` | No | No | Código o número de sección |
| **fk_BIBLIOTECA** | `INT` | No | Si | Referencia a `BIBLIOTECA(ID_sede)` |

---

### 20. Sanciona

| Columna | Tipo de Dato | Llave Primaria (PK) | Llave Foránea (FK) | Descripción / Referencia |
| :--- | :--- | :---: | :---: | :--- |
| **ID_Sancion** | `INT` | Si | No | Identificador único de la sanción |
| **Fecha_inicio** | `DATE` | No | No | Fecha en la que inicia la penalización |
| **Fecha_fin** | `DATE` | No | No | Fecha limite de la sanción |
| **Motivo** | `VARCHAR(255)` | No | No | Causa o razón de la infracción |
| **fk_USUARIO** | `INT` | No | Si | Referencia a `USUARIO(ID_usuario)` |