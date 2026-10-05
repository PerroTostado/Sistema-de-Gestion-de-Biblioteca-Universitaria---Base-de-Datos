# BiblioTech, un Sistema de Gestión de Biblioteca Universitaria

**Entrega 1 — Base de Datos I**
Universidad Industrial de Santander · Facultad de Ingenierías Fisicomecánicas

> **BiblioTech** es el diseño de una base de datos para una plataforma que administra los recursos bibliográficos, los procesos de circulación y las políticas de préstamo a través de una red de bibliotecas multi-sede, integrando tanto inventario físico como disponibilidad híbrida y recursos digitales.

---

## Integrantes del grupo

| # | Nombre completo | Código |
|---|-----------------|--------|
| 1 | Juan Camilo Hernández Parra | 2250174 |
| 2 | Bramdon Julián González Velandia | 2250196 |
| 3 | Jhulian Stewar Prieto Zuluaga | 2251751 |
| 4 | Nicolas Soto Sánchez | 2250145 |
| 5 | Nicolas David Sanguino Ortiz | 2250157 |

---

## Contenido

1. [Contexto del problema trabajado en la actividad de exploración](#1-contexto-del-problema-trabajado-en-la-actividad-de-exploración)
2. [Consulta de tendencias actuales en el área del proyecto](#2-consulta-de-tendencias-actuales-en-el-área-del-proyecto)
3. [Consulta de herramientas o sistemas similares con su análisis de funcionalidades](#3-consulta-de-herramientas-o-sistemas-similares-con-su-análisis-de-funcionalidades)
4. [Modelo E-R del proyecto](#4-modelo-e-r-del-proyecto)

---

## 1. Contexto del problema trabajado en la actividad de exploración

### 1.1 Situación
Las bibliotecas universitarias modernas no funcionan como un único espacio físico, sino que operan como una red compuesta por la Biblioteca Central, sucursales en diferentes campus o sedes regionales, y salas de lectura especializadas dentro de las facultades. El inventario se distribuye estratégicamente basándose en las necesidades de cada ubicación, lo que exige una gestión centralizada y eficiente.

### 1.2 Conceptos clave del dominio

| Concepto | Descripción |
|----------|-------------|
| **Título y Ejemplar** | El "título" representa la información general de la obra, mientras que el "ejemplar" es la copia física individual, cada una con su propio código de barras, ubicación y estado. |
| **Circulación** | Procesos de movimiento del inventario: préstamo (retiro por tiempo limitado), renovación (extensión del plazo) y reserva (lista de espera para un ejemplar prestado). |
| **Red de Bibliotecas** | Organización multi-sede que incluye la Biblioteca Central, sucursales y salas especializadas, donde el inventario se distribuye según la necesidad de la ubicación. |
| **Catálogo** | Inventario público clasificado por autor, materia, año, etc., que permite ubicar en qué sede, piso y estante está un recurso. |
| **Políticas y Sanciones** | Reglas de operación que definen privilegios de préstamo según el usuario (estudiante, profesor) y tipo de colección, además de las penalizaciones por no devolver a tiempo. |
| **Tipología de Recursos** | Formatos diversos que incluyen libros, revistas, periódicos, material audiovisual, tesis y equipos de apoyo. |
| **Disponibilidad Híbrida** | Gestión simultánea de colecciones físicas y electrónicas (e-books, artículos), controlando accesos, licencias institucionales y límites de usuarios simultáneos. |

---

## 2. Consulta de tendencias actuales en el área del proyecto

### 2.1 Tendencias de operación y gestión

*   **Gestión integrada de recursos:** Se está pasando de un catálogo centrado en copias físicas a uno que represente una obra en todos sus formatos, controlando existencias físicas, licencias y derechos de acceso digitales.
*   **Automatización y autoservicio:** Implementación de autopréstamo, auto-devolución, renovación automática, reservas web, notificaciones automáticas e identificación mediante códigos de barras y RFID, permitiendo al bibliotecario enfocarse en servicios especializados.
*   **Interoperabilidad entre sedes:** Capacidad de buscar en un sistema único (Biblioteca Central, facultades y sedes regionales), facilitando el préstamo entre bibliotecas, traslado de materiales, devolución multi-ubicación y autenticación única.

### 2.2 Tendencias tecnológicas y de servicio

*   **Plataformas de descubrimiento e IA:** Evolución del catálogo hacia interfaces similares a buscadores modernos, con búsqueda semántica, recomendaciones, metadatos enriquecidos y adaptación a móviles.
*   **Colecciones digitales y multimedia:** Ampliación del inventario tradicional para incluir e-books, revistas electrónicas, bases de datos académicas, datasets y streaming audiovisual, requiriendo gestión de derechos de autor y preservación digital.
*   **Disponibilidad híbrida:** Acceso remoto 24/7 que exige controlar proveedores, licencias, usuarios autorizados, número de accesos y períodos de suscripción.
*   **Flexibilidad en políticas:** Transición de un modelo de control restrictivo a uno que facilita el acceso, con períodos de gracia, renovaciones automáticas y bloqueos orientados a la recuperación real del material.

---

## 3. Consulta de herramientas o sistemas similares con su análisis de funcionalidades

Se analizaron dos sistemas que resuelven las problemáticas de la gestión bibliotecaria universitaria:

### 3.1 Sistema de Bibliotecas de la UIS
Es la plataforma utilizada por la universidad para administrar sus recursos bibliográficos en sus diferentes sedes.
*   **Catálogo Público (OPAC):** Ofrece un buscador para consultar existencias, visualizar la ficha bibliográfica y verificar la sede, piso y colección exacta.
*   **Autogestión del Usuario:** Permite a los estudiantes ingresar con su cuenta para revisar su estado, historial, vencimientos y realizar renovaciones en línea sin asistencia presencial.
*   **Integración Académica:** Se conecta con la administración universitaria para validar si el estudiante está matriculado o tiene multas pendientes, aspecto requerido para grados o matrículas.

### 3.2 Koha (Sistema Integrado de Gestión de Bibliotecas - SIGB)
El primer sistema de gestión de bibliotecas de código abierto a nivel mundial, ampliamente usado por instituciones académicas para gestionar todo su flujo de trabajo.
*   **Módulos Especializados:** Divide la operación en módulos como Circulación, Catalogación y Usuarios.
*   **Gestión de Sucursales:** Diseñado para redes de bibliotecas, permitiendo configurar políticas distintas por sede y rastrear envíos de libros entre ellas.
*   **Notificaciones y Alertas Automáticas:** Reduce la morosidad enviando correos cuando se acerca una fecha de devolución o cuando una reserva ya está lista para ser recogida.

---

## 4. Modelo E-R del proyecto

A continuación se presenta el modelo Entidad-Relación diseñado para el sistema de la biblioteca:
<img width="2472" height="2017" alt="Biblioteca_ER" src="https://github.com/user-attachments/assets/4c8bf5b0-0ee4-40e2-a9ce-983242783180" />


---
