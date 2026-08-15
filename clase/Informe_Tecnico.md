# 📄 Informe Técnico del Taller

## 🔖 Nombre del Taller
_Taller X - [Nombre completo del taller]_

## 👥 Integrantes del equipo
- Jorge Alarcon
- Julian Aguirre
- Brayan Presiga

## 🧠 Descripción general del trabajo
El objetivo del taller fue modelar las entidades principales de un dominio de negocio y los flujos de información entre actores y sistemas, mediante un modelo entidad-relación (ERD) y un diagrama de contexto de negocio. Como caso base de trabajo en clase se utilizó el escenario de la Clínica Salud Viva, empresa que gestiona información de pacientes, citas, médicos, especialidades y facturación a través de distintos sistemas (ERP clínico, agendamiento y notificador) que deben interoperar entre sí, incluyendo actores externos como las aseguradoras.
 
La actividad se desarrolló siguiendo la metodología de 4 pasos propuesta en la guía del taller: (1) identificación de entidades, (2) definición de atributos y clave primaria, (3) trazado de relaciones con su verbo asociado, y (4) asignación de cardinalidad a cada relación.
 
## 🔧 Proceso de desarrollo
 
El equipo construyó el modelo de forma incremental, partiendo de las cinco entidades sugeridas en el enunciado (`PACIENTE`, `CITA`, `MÉDICO`, `ESPECIALIDAD`, `FACTURA`):
 
1. **Identificación de entidades**: se listaron las entidades del dominio clínico, diferenciando aquellas que representan actores (Paciente, Médico) de aquellas que representan eventos o procesos (Cita, Factura) y catálogos (Especialidad).
2. **Definición de atributos y llaves primarias**: a cada entidad se le asignaron sus atributos descriptivos (por ejemplo, `PACIENTE` con Nombre, Teléfono, Correo Electrónico, Género y Edad) y se marcó explícitamente su identificador único (`IdPaciente`, `IdCita`, `IdMédico`, `IdEspecialidad`, `IdFactura`).
3. **Trazado de relaciones**: se definieron los verbos que describen cada vínculo entre entidades — `agenda` (Paciente-Cita), `asignado` (Cita-Médico), `tiene` (Cita-Factura) y `posee`/`es poseído` (Médico-Especialidad, a través de la relación `tiene`).
4. **Asignación de cardinalidad**: se revisó cada relación contra las reglas de negocio del enunciado (un paciente puede tener muchas citas; cada cita se asocia a un único médico y a una especialidad) para fijar la cardinalidad correspondiente en cada extremo de la relación.
Como herramienta de modelado se usó un editor de diagramas digital (tipo draw.io), lo que permitió iterar rápidamente sobre la ubicación de entidades, atributos y relaciones, y ajustar la notación (rombos para relaciones, óvalos para atributos, rectángulos para entidades) conforme se recibía retroalimentación del docente.
 
## 🧩 Análisis del modelo propuesto
 
**Estructura del modelo entregado**: el modelo se organiza alrededor de `CITA` como entidad central del proceso de negocio, ya que es el punto donde convergen paciente, médico y (posteriormente) factura. Esto refleja que, en el dominio clínico, la cita es el evento transaccional que dispara el resto del flujo de información: primero se agenda, luego se asigna un médico con una especialidad, y finalmente se genera la facturación asociada.
 
**Representación de las necesidades del negocio**: la separación de `ESPECIALIDAD` como entidad independiente (y no como un atributo de texto libre en `MÉDICO`) permite representar correctamente que un médico puede tener una o varias especialidades y que estas son gestionadas como un catálogo propio, con su propio identificador. De igual forma, modelar `FACTURA` como entidad relacionada 1 a 1 con `CITA` (y no como atributo de esta) permite registrar su propia información de facturación (precio, fecha de facturación) de forma independiente, lo cual es necesario para procesos posteriores como la validación con aseguradoras mencionada en el enunciado del caso.
 
**Supuestos tomados por el equipo**:
- Cada cita genera exactamente una factura (relación 1 a 1), es decir, no se modelan citas sin costo asociado ni facturas que agrupen varias citas.
- Un médico puede poseer una o varias especialidades (cardinalidad 1,n), y una especialidad puede ser poseída por uno o varios médicos.
- El atributo `Nombre` se repite en distintas entidades (`Paciente`, `Médico`, `Especialidad`) porque cada uno corresponde a un concepto distinto dentro de su propia entidad, sin que esto implique redundancia real en el modelo.
## 📈 Diagrama final entregado
> Diagrama ERD del caso base "Clínica Salud Viva" (entrega de la sesión de clase). Entidades: `PACIENTE`, `CITA`, `MÉDICO`, `ESPECIALIDAD`, `FACTURA`. Relaciones: `agenda` (1:N), `asignado` (N:1), `tiene` Cita-Factura (1:1), `tiene`/`posee`/`es poseído` Médico-Especialidad (1,n:1,n).
>
> _(Insertar aquí la imagen exportada del diagrama o el enlace al archivo .drawio correspondiente)_
 
## 📋 Tabla de actores, entidades o componentes
 
| Nombre del elemento | Tipo    | Descripción                                                        | Responsable |
|----------------------|---------|---------------------------------------------------------------------|-------------|
| Paciente             | Entidad | Persona que agenda y recibe una cita médica                        | Clínica     |
| Cita                 | Entidad | Evento que conecta a un paciente con un médico en una fecha y hora | Clínica     |
| Médico               | Entidad | Profesional de la salud asignado a una o varias citas              | Clínica     |
| Especialidad         | Entidad | Catálogo de áreas médicas que un médico puede poseer                | Clínica     |
| Factura              | Entidad | Documento de cobro generado a partir de una cita                    | Clínica     |
 
## 🔍 Investigación complementaria
 
### Tema investigado:
Buenas prácticas en el diseño de modelos entidad-relación (ERD) en proyectos reales de la industria.
 
### Resumen:
Un diagrama entidad-relación es, en esencia, un tipo de diagrama que representa cómo se relacionan entre sí entidades como personas, objetos o conceptos dentro de un sistema, y su valor principal está en ofrecer una vista de alto nivel que captura el alcance general de un dominio antes de entrar en el detalle técnico de una base de datos [1]. En la práctica profesional se recomienda avanzar en un proceso de seis pasos: identificar las entidades clave, determinar las relaciones entre ellas, asignar cardinalidades según las reglas del negocio, definir atributos, identificar las llaves primarias y finalmente dibujar el diagrama con la notación adecuada [2] — que es prácticamente la misma metodología de 4 pasos aplicada en este taller.
 
Sobre la elección de notación, la literatura técnica distingue entre la notación de Chen, más adecuada para el diseño conceptual y el ámbito académico, y la notación "pata de gallo" (crow's foot), preferida en entornos industriales para el diseño lógico y físico de bases de datos. En proyectos reales el ERD conceptual (sin detalles de implementación) suele usarse primero para validar el entendimiento del negocio con el cliente, y solo después se deriva un modelo lógico y físico con tipos de datos y restricciones concretas.
 
Finalmente, en cuanto a buenas prácticas de mantenimiento, se recomienda mantener el diagrama actualizado a medida que el negocio cambia, aplicar convenciones de nomenclatura consistentes y documentar explícitamente las decisiones de modelado (como los supuestos registrados en la sección anterior de este informe), ya que un buen ERD no solo describe datos sino que también captura la intención del negocio y facilita la toma de decisiones técnicas posteriores. Esto se relaciona directamente con este taller: los supuestos documentados en la sección de análisis (por ejemplo, la relación 1 a 1 entre Cita y Factura) son justamente el tipo de decisión que debe quedar registrada para que el modelo sea entendible por terceros, como recomienda una guía institucional de modelos entidad-relación, que describe el ERD como un artefacto con doble utilidad: comunicar un dominio de la realidad y, a la vez, organizar los datos de un sistema.
 
## 📚 Referencias
 
- [1] Lucidchart. *¿Qué es un diagrama de entidad-relación (ERD)?*. 2026. https://www.lucidchart.com/pages/es/que-es-un-diagrama-entidad-relacion
- [2] Guru99. *Modelo de diagrama de entidad-relación (ER) con ejemplo de DBMS*. 2026. https://www.guru99.com/es/er-diagram-tutorial-dbms.html
- [3] Departamento Nacional de Planeación (DNP). *Guía Modelos Entidad Relación*. Bogotá, 2019. https://colaboracion.dnp.gov.co/CDTI/Oficina%20Informatica/Sistemas%20de%20informaci%C3%B3n/Gu%C3%ADas%20Formatos%20Plantillas/Lineamientos%20Modelos%20Entidad%20Relaci%C3%B3n.pdf
- [4] Jordiedo. *Modelo Entidad-Relación: Guía completa para diseñar bases de datos eficientes*. 2026. https://jordiedo.es/modelo-entidad-relacion/
---
 
_Este documento hace parte de la entrega del Taller 2 del curso AREM (Arquitectura Empresarial) - Universidad de La Sabana._
 
