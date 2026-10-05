# Diagramas — Entrega 1

Modelos gráficos del proyecto **Sistema de Gestión de una Biblioteca Universitaria**.

---

## Inventario

| Archivo | Descripción |
|---------|-------------|
| [`diagramas_entrega_1.md`]([https://github.com/PerroTostado/Sistema-de-Gestion-de-Biblioteca-Universitaria---Base-de-Datos/blob/main/Primer%20Entregable/Primer%20Diagrama%20Entidad%20-%20Relaci%C3%B3n/primer-modelo-e-r.md](https://github.com/PerroTostado/Sistema-de-Gestion-de-Biblioteca-Universitaria---Base-de-Datos/blob/main/Primer%20Entregable/Primer%20Diagrama%20Entidad%20-%20Relación/diagramas_entrega_1.md)) | Documento detallado del Primer Modelo Entidad-Relación. |
| [`primer-modelo-e-r.md`]([https://github.com/PerroTostado/Sistema-de-Gestion-de-Biblioteca-Universitaria---Base-de-Datos/blob/main/Primer%20Entregable/Primer%20Diagrama%20Entidad%20-%20Relaci%C3%B3n/primer-modelo-e-r.md](https://github.com/PerroTostado/Sistema-de-Gestion-de-Biblioteca-Universitaria---Base-de-Datos/blob/main/Primer%20Entregable/Primer%20Diagrama%20Entidad%20-%20Relación/primer-modelo-e-r.md)) | Documento detallado del Primer Modelo Entidad-Relación. |

---

## Notación utilizada

El modelo está en **notación de Chen**. La leyenda va embebida en el propio
diagrama; se reproduce aquí como referencia rápida:

| Símbolo | Significado |
|---------|-------------|
| Rectángulo | Entidad fuerte |
| Rectángulo doble | Entidad débil |
| Rombo | Relación |
| Rombo doble | Relación identificadora (de una entidad débil) |
| Óvalo | Atributo |
| Óvalo con texto **subrayado** | Atributo clave (PK) |
| Óvalo con subrayado **punteado** | Clave parcial (de una entidad débil) |
| Óvalo doble | Atributo multivaluado |
| Óvalo punteado | Atributo derivado (calculado) |
| Triángulo `ISA` | Especialización / generalización |
| `(d)` | Especialización disjunta |
| `1`, `N`, `M` sobre las líneas | Cardinalidad de la relación |

---

## Contenido del modelo E-R

- **11 entidades** — 7 fuertes (`LIBRO`, `AUTOR`, `CATEGORÍA`, `EDITORIAL`, `USUARIO`, `BIBLIOTECA`, `UBICACIÓN`) y 4 débiles (`EJEMPLARES`, `RESERVA`, `RENOVACIÓN`, `SANCIÓN`).
- **Múltiples relaciones** — Varias de ellas con atributos propios (como fechas de solicitud, préstamo o devolución).
- **3 especializaciones** — Generalización de recursos y actores: 
  - `EJEMPLARES` → `FÍSICO` / `VIRTUAL`
  - `USUARIO` → `ESTUDIANTE` / `DOCENTE`
  - `BIBLIOTECA` → `FÍSICA` / `VIRTUAL`
- Un **subsistema de circulación y control** conformado por las interacciones entre los usuarios, los ejemplares prestados/reservados y el régimen de sanciones.
