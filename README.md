# WorkFlex – Sistema de Gestión de Reservas para Espacios de Coworking

Proyecto académico desarrollado para la asignatura **Programación II e Ingeniería del Software**.

WorkFlex plantea el análisis y diseño de una plataforma digital orientada a centralizar la gestión de espacios de coworking, sustituyendo procesos manuales basados en hojas de cálculo y correo electrónico por una solución estructurada, escalable y preparada para futuras ampliaciones.

## Descripción del proyecto

La plataforma está diseñada para permitir la gestión integrada de:

- usuarios y perfiles;
- sedes y espacios de coworking;
- disponibilidad de espacios;
- reservas;
- membresías;
- accesos;
- pagos y facturación;
- ocupación y generación de informes.

El proyecto se centra en las fases de **análisis, modelado y diseño arquitectónico**, sin incluir la implementación completa de la aplicación.

## Objetivos

El objetivo principal es definir una solución técnica que permita:

- centralizar la información de WorkFlex;
- reducir errores derivados de la gestión manual;
- evitar conflictos de disponibilidad;
- mejorar la trazabilidad de reservas y pagos;
- facilitar la integración con servicios externos;
- permitir el crecimiento futuro de la plataforma.

## Metodología

Se propone un modelo de desarrollo **ágil basado en Scrum**, combinado con un enfoque incremental.

La planificación se organiza en distintos sprints:

1. Usuarios, sedes y espacios.
2. Disponibilidad y reservas.
3. Membresías y accesos.
4. Pagos y facturación.
5. Administración e informes.

La priorización inicial de requisitos se ha realizado mediante el método **MoSCoW**.

## Modelado del sistema

El proyecto incluye diferentes modelos UML:

- Diagrama de casos de uso.
- Diagrama de clases.
- Diagrama de secuencia del proceso de reserva.

El modelo contempla como entidades principales:

```text
Usuario
Membresía
Sede
Espacio
Reserva
Pago
Factura
```

Una reserva puede encontrarse en los siguientes estados:

```text
PENDIENTE_PAGO
CONFIRMADA
CANCELADA
FINALIZADA
```

## Diseño de software

La aplicación se plantea siguiendo el patrón arquitectónico:

```text
Model – View – Controller
          MVC
```

Además, se consideran otros patrones de diseño cuando aportan una ventaja concreta:

- **Factory**, para desacoplar la integración con diferentes proveedores de pago.
- **Strategy**, para gestionar reglas variables asociadas a membresías, precios o condiciones de reserva.
- **Singleton**, únicamente en situaciones específicas donde tenga sentido compartir una única instancia de configuración.

Se prioriza la **composición frente a la herencia** cuando proporciona mayor flexibilidad al modelo.

## Arquitectura

Se propone una arquitectura modular organizada inicialmente como una única aplicación.

Los principales módulos son:

```text
Usuarios y autenticación
Sedes y espacios
Reservas
Membresías
Pagos y facturación
Administración e informes
```

La estructura general sigue el siguiente esquema:

```text
Usuario
   │
   ▼
Interfaz Web / App
   │
   ▼
Capa de aplicación y lógica de negocio
   │
   ├── Usuarios y autenticación
   ├── Sedes y espacios
   ├── Reservas
   ├── Membresías
   ├── Pagos y facturación
   └── Administración e informes
   │
   ▼
Capa de acceso a datos
   │
   ▼
Base de datos
```

Los servicios externos, como las pasarelas de pago o los sistemas de autenticación, se integran mediante APIs.

## API REST

La plataforma contempla una API REST versionada:

```text
/api/v1/
```

Algunos endpoints representativos son:

```http
GET    /api/v1/sedes
GET    /api/v1/sedes/{id}/espacios
GET    /api/v1/espacios/disponibilidad

POST   /api/v1/reservas
GET    /api/v1/reservas/{id}
PATCH  /api/v1/reservas/{id}

PATCH  /api/v1/reservas/{id}/cancelacion

GET    /api/v1/usuarios/{id}/membresia

POST   /api/v1/pagos
GET    /api/v1/facturas/{id}
```

La cancelación de una reserva no implica su eliminación del sistema. La reserva pasa al estado:

```text
CANCELADA
```

permitiendo conservar la trazabilidad de la operación y liberar nuevamente el espacio correspondiente.

## Flujo básico de una reserva

```text
Usuario
   │
   ▼
Consulta disponibilidad
   │
   ▼
Selecciona espacio
   │
   ▼
Validación de disponibilidad
   │
   ▼
Reserva → PENDIENTE_PAGO
   │
   ▼
Procesamiento del pago
   │
   ├── Pago correcto → CONFIRMADA
   │
   └── Pago rechazado → liberar espacio
```

## Prototipado

Se han definido wireframes para representar los principales flujos de interacción con la plataforma.

Entre ellos:

- consulta de disponibilidad;
- selección de espacios;
- confirmación de reserva.

Los wireframes se utilizan como una representación preliminar de la interfaz y permiten validar la navegación antes de desarrollar la GUI definitiva.

## Requisitos no funcionales

La propuesta también contempla aspectos relacionados con:

- seguridad;
- protección de datos;
- rendimiento;
- escalabilidad;
- disponibilidad;
- integridad de la información;
- trazabilidad;
- usabilidad;
- compatibilidad;
- mantenibilidad;
- interoperabilidad.

## Estructura del repositorio

Una posible organización del repositorio sería:

```text
WorkFlex/
│
├── README.md
│
├── docs/
│   ├── memoria-proyecto.pdf
│   ├── uml/
│   ├── arquitectura/
│   └── wireframes/
│
├── diagrams/
│   ├── casos-uso.png
│   ├── clases.png
│   ├── secuencia-reserva.png
│   └── arquitectura.png
│
└── api/
    └── endpoints.md
```

## Documentación

La memoria completa del proyecto incluye:

- análisis del problema;
- requisitos funcionales y no funcionales;
- priorización MoSCoW;
- metodología de desarrollo;
- modelado conceptual;
- diagramas UML;
- patrones de diseño;
- arquitectura;
- estrategia de APIs;
- seguridad y escalabilidad;
- wireframes;
- anexos técnicos.

## Estado del proyecto

```text
Análisis                 ✔
Requisitos               ✔
Modelado conceptual      ✔
UML                      ✔
Arquitectura             ✔
Diseño API REST          ✔
Wireframes               ✔
Implementación           Pendiente / fuera del alcance académico
```

## Autor

**Jose María Ochoa Carriches**

Bachelor en Informática  
Asignatura: **Programación II e Ingeniería del Software**

Curso académico **2026/27**

---

Proyecto desarrollado con fines académicos.
