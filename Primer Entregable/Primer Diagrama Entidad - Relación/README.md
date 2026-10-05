# Diagramas — Entrega 1

Modelos gráficos del proyecto **Sistema de Gestión de una Biblioteca Universitaria**.

## Integrantes

| Nombre completo | Código |
|---|---:|
| Juan Camilo Hernández Parra | 2250174 |
| Bramdon Julián González Velandia | 2250196 |
| Jhulian Stewar Prieto Zuluaga | 2251751 |
| Nicolas Soto Sánchez | 2250145 |
| Nicolas David Sanguino Ortiz | 2250157 |


## Inventario

| **Archivo** | **Descripción** | 
|---------|-----------|
| [`Primer Modelo-E-R`](https://github.com/PerroTostado/Sistema-de-Gestion-de-Biblioteca-Universitaria---Base-de-Datos/blob/d2b25d44e49fb8eed0b544ca71d37d0d695151c7/Primer%20Entregable/Primer%20Diagrama%20Entidad%20-%20Relaci%C3%B3n/primer-modelo-e-r.md) | Diagrama Propuesto. | 

## Notación utilizada

El modelo está en **notación de Chen**. Se resume aquí como referencia rápida:

| **Símbolo** | **Significado** | 
|---------|-----------|
| Rectángulo | Entidad fuerte |  
| Rombo | Relación | 
| Óvalo | Atributo | 
| Óvalo con texto **subrayado** | Atributo clave primaria (PK) | 
| Triángulo boca abajo | Especialización / generalización disjunta | 
| `(min, max)` sobre las líneas | Cardinalidad y participación de la relación | 

## Contenido del modelo E-R

* **16 entidades** — 10 entidades principales/fuertes y 6 entidades especializadas (subclases/hijas).

* **9 relaciones** — Incluye relaciones simples y la relación con atributos propios `Sanciona`.

* **3 especializaciones** — Generalización de recursos y actores:

  * `EJEMPLARES` → `FÍSICO` / `VIRTUAL`

  * `USUARIO` → `ESTUDIANTE` / `DOCENTE`

  * `BIBLIOTECA` → `FÍSICA` / `VIRTUAL`
