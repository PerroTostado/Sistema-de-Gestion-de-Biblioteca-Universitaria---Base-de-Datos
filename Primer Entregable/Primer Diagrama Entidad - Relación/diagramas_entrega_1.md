# Diagramas — Entrega 1

Modelos gráficos del proyecto **Sistema de Gestión de una Biblioteca Universitaria**.

## Inventario

| 

| **Archivo** | **Descripción** | 
| [`primer-modelo-e-r.md`](https://github.com/PerroTostado/Sistema-de-Gestion-de-Biblioteca-Universitaria---Base-de-Datos/blob/main/Primer%20Entregable/Primer%20Diagrama%20Entidad%20-%20Relaci%C3%B3n/primer-modelo-e-r.md) | Diagrama Propuesto. | 

## Notación utilizada

El modelo está en **notación de Chen**. La leyenda va embebida en el propio diagrama; se reproduce aquí como referencia rápida:

| **Símbolo** | **Significado** | 
| Rectángulo | Entidad fuerte | 
| Rectángulo doble | Entidad débil | 
| Rombo | Relación | 
| Rombo doble | Relación identificadora (de una entidad débil) | 
| Óvalo | Atributo | 
| Óvalo con texto **subrayado** | Atributo clave primaria (PK) | 
| Óvalo con subrayado **punteado** | Clave parcial (de una entidad débil) | 
| Triángulo con `d` | Especialización / generalización disjunta | 
| `(min, max)` sobre las líneas | Cardinalidad y participación de la relación | 

## Contenido del modelo E-R

* **16 entidades** — 10 entidades principales/fuertes y 6 entidades especializadas (subclases/hijas).

* **9 relaciones** — Incluye relaciones simples y la relación con atributos propios `Sanciona`.

* **3 especializaciones** — Generalización de recursos y actores:

  * `EJEMPLARES` → `FÍSICO` / `VIRTUAL`

  * `USUARIO` → `ESTUDIANTE` / `DOCENTE`

  * `BIBLIOTECA` → `FÍSICA` / `VIRTUAL`
