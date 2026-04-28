# Laboratorio Introduccion OOP

Desarrollar un laboratorio de Programación Orientada a Objetos que permita comprender, aplicar y consolidar los principios fundamentales de este paradigma, mediante la creación y modelación de soluciones en Java que integren conceptos como clases, objetos, herencia, encapsulamiento, abstracción y polimorfismo implementando metodologias agiles Scrum.

## Enunciado del problema

La biblioteca universitaria XYZ ha experimentado un crecimiento significativo en la cantidad de estudiantes, docentes y material bibliográfico disponible. Actualmente, muchos de sus procesos se realizan de manera manual o con herramientas poco integradas, lo que ha generado inconvenientes como pérdida de información, dificultades en el control de préstamos, demoras en la atención a los estudiantes y falta de trazabilidad sobre el estado de los libros.

Además del préstamo de libros físicos, la biblioteca ofrece servicios como reservas, renovación de préstamos, consulta del catálogo, y gestión de sanciones por retrasos en la devolución. Sin embargo, estos servicios no están centralizados en un sistema eficiente, lo que afecta la calidad del servicio y la experiencia de los estudiantes.

Ante esta situación, la universidad ha decidido desarrollar un sistema de información que permita gestionar de manera integral la biblioteca, facilitando el control, organización y seguimiento del material bibliográfico, así como la administración de los servicios ofrecidos a los estudiantes.

El sistema deberá permitir, entre otras funcionalidades:

- Registrar y gestionar libros, estudiantes y categorías.
- Controlar el préstamo y devolución de libros.
- Permitir la reserva y renovación de material bibliográfico.
- Gestionar multas o sanciones por retrasos.
- Consultar la disponibilidad de libros en tiempo real.

---

## Proposito de la activiidad

A partir de este contexto, los estudiantes deberán analizar la problemática y diseñar una solución siguiendo un enfoque ágil, generando los siguientes artefactos:

- Historias de estudiante redactadas con la estructura ```Como [rol], quiero [funcionalidad], para [beneficio]```, aplicando criterios INVEST y definiendo criterios de aceptación mediante la técnica Gherkin (Given–When–Then).
- Product Backlog priorizado, identificando las historias necesarias para construir un Producto Mínimo Viable (MVP).
- Planeación de Sprints, definiendo el número de iteraciones y las historias de estudiante a desarrollar en cada una.
- Diagrama de clases, basado en el análisis de las historias de estudiante, que represente la estructura del sistema.

---

## Guia introductoria

### Ejemplo de Historias de estudiante (HU)

#### HU01 – Registrar estudiante

Como **bibliotecario**, quiero **registrar nuevos estudiantes en el sistema**, para **permitirles acceder a los servicios de la biblioteca**.

#### Criterios de aceptación (Gherkin)

- **Dado** que el bibliotecario está en el sistema **cuando** ingresa los datos del estudiante correctamente, **entonces** el sistema registra el estudiante exitosamente
- **Dado** que falta información obligatoria **cuando** intenta registrar el estudiante, **entonces** el sistema muestra un mensaje de error

#### HU02 – Consultar catálogo de libros

Como **estudiante**, quiero **buscar libros por título, autor o categoría**, para **encontrar material de interés**.

#### Criterios de aceptación:

- **Dado** que el estudiante accede al catálogo **cuando** ingresa un criterio de búsqueda, **entonces** el sistema muestra los libros relacionados.

#### HU03 – Prestar libro

Como **bibliotecario**, quiero **registrar el préstamo de un libro**, para llevar control de los libros entregados.

#### Criterios de aceptación

- **Dado** que el libro está disponible **cuando** se registra el préstamo, **entonces** el sistema cambia el estado del libro a “prestado”.
- **Dado** que el libro no está disponible **cuando** se intenta prestar, **entonces** el sistema muestra una alerta.

#### HU04 – Devolver libro

Como **bibliotecario**, quiero **registrar la devolución de un libro**, para **actualizar su disponibilidad**.

#### Criterios de aceptación:

- Dado que el libro fue prestado **cuando** se registra la devolución, **entonces** el sistema actualiza su estado a “disponible”.

#### HU05 – Reservar libro

Como **estudiante**, quiero **reservar un libro**, para **asegurar su disponibilidad cuando esté libre**.

#### Criterios de aceptación:

- Dado que el libro no está disponible **cuando** el estudiante realiza una reserva, **entonces** el sistema registra la reserva correctamente.

#### HU06 – Generar multa

Como **bibliotecario**, quiero **generar multas por retraso en la devolución**, para **fomentar la responsabilidad en los estudiantes**.

#### Criterios de aceptación:

- **Dado** que un libro se devuelve fuera de la fecha **cuando** el sistema calcula el retraso, **entonces** se genera una multa automáticamente.

---

### Ejemplo de Product Backlog

| Prioridad | ID   | Historia de estudiante | Valor |
| --------- | ---- | ------------------- | ----- |
| Alta      | HU01 | Registrar estudiante   | Alta  |
| Alta      | HU03 | Prestar libro       | Alta  |
| Alta      | HU04 | Devolver libro      | Alta  |
| Alta      | HU02 | Consultar catálogo  | Alta  |
| Media     | HU05 | Reservar libro      | Media |
| Media     | HU06 | Generar multa       | Media |

> MVP sugerido: HU01, HU02, HU03, HU04

---

## Ejemplo de Planeación de Sprints

### Sprint 1 (Base del sistema)

- HU01 – Registrar estudiante.
- HU02 – Consultar catálogo.

### Sprint 2 (Operaciones principales)

- HU03 – Prestar libro.
- HU04 – Devolver libro.

### Sprint 3 (Funciones adicionales)
- HU05 – Reservar libro.
- HU06 – Generar multa.

---

## Ejemplo de Diagrama de Clases (conceptual)

- estudiante
  - id
  - nombre
  - tipo (estudiante/docente)

- Libro
  - id
  - título
  - autor
  - estado

- Préstamo
  - fechaInicio
  - fechaFin
  - estado
  - Reserva
  - fecha
  - estado

- Multa
  - valor
  - fecha
  - estado

> Relaciones clave:
> - Un Estudiante puede tener muchos Préstamos
> - Un Libro puede estar asociado a un Préstamo
> - Un Estudiante puede tener Multas

```
@startuml

class estudiante {
  - id: int
  - nombre: String
  - email: String
  - tipo: String
  + registrarse()
  + consultarHistorial()
}

class Libro {
  - id: int
  - titulo: String
  - autor: String
  - categoria: String
  - estado: String
  + consultarDisponibilidad()
}

class Prestamo {
  - id: int
  - fechaInicio: Date
  - fechaFin: Date
  - estado: String
  + registrarPrestamo()
  + registrarDevolucion()
}

class Reserva {
  - id: int
  - fecha: Date
  - estado: String
  + crearReserva()
  + cancelarReserva()
}

class Multa {
  - id: int
  - valor: double
  - fechaGeneracion: Date
  - estado: String
  + calcularMulta()
  + pagarMulta()
}

class Bibliotecario {
  + registrarestudiante()
  + gestionarPrestamo()
  + generarMulta()
}

' Relaciones
estudiante "1" -- "0..*" Prestamo : realiza
Libro "1" -- "0..*" Prestamo : es prestado en

estudiante "1" -- "0..*" Reserva : realiza
Libro "1" -- "0..*" Reserva : es reservado en

estudiante "1" -- "0..*" Multa : recibe

Bibliotecario ..> estudiante : gestiona
Bibliotecario ..> Prestamo : administra
Bibliotecario ..> Multa : genera

Prestamo "1" -- "0..1" Multa : genera

@enduml
```
