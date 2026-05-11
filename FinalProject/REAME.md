# Proyecto Final

Curso: Programación para Dispositivos Móviles

## Objetivo general

Desarrollar una aplicación móvil cliente/servidor orientada al usuario común, que permita el registro e inicio de sesión y la gestión básica (crear, ver, editar y eliminar) de una entidad principal relacionada con una temática de interés.

El proyecto debe incluir una aplicación móvil nativa o multiplataforma no híbrida y un backend con base de datos relacional. La conexión entre ambos componentes se podrá realizar directamente en red local o mediante herramientas de túnel (LocalTunnel, ngrok, Expose o similares).

Modalidad de trabajo: individual o grupos de hasta 2 estudiantes

---

## Estructura general

### 1. Aplicación móvil (frontend)

Debe ser nativa o multiplataforma compilada a código nativo, no híbrida.

Opciones permitidas:

* Android (Java o Kotlin)
* iOS (Swift o SwiftUI)
* Jetpack Compose Multiplatform (JCM)
* Flutter (Dart)

No se permiten frameworks basados en WebViews (Ionic, Cordova, Capacitor, React Native, entre otros).

La aplicación debe ejecutarse tanto en Android como en iOS, ya sea mediante:

* Emuladores o simuladores
* Dispositivos físicos

La aplicación debe conectarse al backend mediante servicios REST (formato JSON) y presentar:

Pantallas de autenticación:

1. Registro
2. Inicio de sesión

Mínimo tres pantallas correspondientes al dominio principal de la aplicación, por ejemplo:

* Lista de elementos
* Detalle de elemento
* Creación o edición de elemento

---

### 2. Backend (servidor)

Puede desarrollarse en:

* PHP (Slim o Laravel)
* Node.js (Express)
* Java (Spring Boot)
* Swift (Vapor)

Debe incluir:

* Endpoints REST para registro, inicio de sesión y CRUD de una entidad principal.
* Validación básica de datos en el servidor.
* Persistencia en una base de datos relacional.

No se requiere implementar roles, paneles de administración ni autenticación avanzada.

---

### 3. Base de datos relacional

Puede usarse:

* MySQL
* MariaDB
* PostgreSQL
* Oracle
* SQL Server

La base de datos debe incluir al menos cinco tablas relacionadas mediante claves foráneas, correspondientes al dominio principal de la aplicación.

Las tablas técnicas o de soporte relacionadas con autenticación y manejo de sesión no cuentan dentro de estas cinco tablas mínimas.

Ejemplos de tablas que no cuentan:

* usuarios
* sesiones
* tokens
* refresh_tokens
* logs de autenticación

Las cinco tablas mínimas deben pertenecer a la lógica funcional del proyecto. Por ejemplo:

* pedidos
* productos
* categorías
* entregas
* historial_pedidos

o

* eventos
* ubicaciones
* asistentes
* categorías_evento
* registros_asistencia

Se espera que el modelo relacional refleje adecuadamente las relaciones entre entidades del dominio de la aplicación.

---

### 4. Conexión entre la App y el Backend

Para permitir el acceso desde el emulador o el dispositivo físico a los servicios del backend, se debe usar una de las siguientes alternativas:

* Configurar el backend en la misma red local y usar la dirección IP del equipo.
* Exponer el servicio mediante herramientas como LocalTunnel, ngrok o Expose, de modo que el backend sea accesible desde una URL pública temporal.

Cada grupo debe documentar en el archivo README el método usado y las URLs de prueba.

---

### 5. Opciones de despliegue

#### Opción A — Docker Compose o Podman Compose

* Servicios recomendados: api, db y adminer (o pgadmin).
* Ejecución local mediante:

  * `docker-compose up`
  * `podman-compose up`

También se permite desplegar los contenedores en servicios cloud compatibles, por ejemplo:

* Render
* Railway
* Fly.io
* AWS
* Azure
* Google Cloud
* Oracle Cloud
* VPS con Docker o Podman

---

#### Opción B — Podman, kind y kubectl

* Creación de un clúster local con kind.
* Despliegue mediante `kubectl apply -f` con manifiestos Deployment y Service.

También se permite utilizar servicios Kubernetes gestionados en la nube.

---

## Funcionalidades mínimas requeridas

1. Registro de usuario

   * Validación básica de campos.
   * Contraseña cifrada (bcrypt o equivalente).

2. Inicio de sesión

   * Validación de credenciales.
   * Manejo de sesión o token simple.

3. Gestión principal (CRUD)

   * Crear, listar, editar y eliminar registros de la entidad principal.

4. Interfaz móvil funcional

   * Mínimo tres pantallas correspondientes al dominio principal de la aplicación.

---

## Entregables y calendario sugerido

| Semana | Entregable                                  | Descripción                                       |
| ------ | ------------------------------------------- | ------------------------------------------------- |
| 1      | Diseño y modelo entidad-relación            | Boceto de pantallas y estructura de base de datos |
| 2      | Backend y base de datos funcional           | API REST con endpoints básicos                    |
| 3      | Aplicación móvil conectada al backend       | Registro, inicio de sesión y CRUD funcional       |
| 4      | Pruebas, documentación y demostración final | Presentación o video del sistema completo         |

---

## Criterios de evaluación

| Criterio                                                 | Porcentaje |
| -------------------------------------------------------- | ---------- |
| Aplicación móvil (interfaz, flujo y conexión al backend) | 40 %       |
| Backend y base de datos                                  | 30 %       |
| Despliegue o exposición del backend                      | 15 %       |
| Documentación técnica (README, diagramas, endpoints)     | 10 %       |
| Presentación y demostración final                        | 5 %        |

---

## Endpoints mínimos

```text
POST   /api/register
POST   /api/login
GET    /api/items
POST   /api/items
PUT    /api/items/{id}
DELETE /api/items/{id}
```

---

## Temáticas sugeridas (elegir una)

1. Gestión de eventos académicos
2. Citas médicas universitarias
3. Turismo local
4. Control de asistencia
5. Gestor de tareas académicas
6. Voluntariado universitario
7. Inventario de laboratorios
8. Registro de actividad física
9. Aplicación tipo Rappi (pedidos y entregas)
10. Aplicación de rastreo de encomiendas

---

## Lista de verificación para la entrega final

* [ ] Registro e inicio de sesión funcionales
* [ ] CRUD completo en backend
* [ ] Base de datos relacional con al menos cinco tablas de dominio
* [ ] Conexión entre App y backend mediante túnel, red local o despliegue cloud
* [ ] Opción de despliegue documentada
* [ ] Aplicación móvil operativa en Android e iOS
* [ ] Mínimo tres pantallas correspondientes al dominio principal
* [ ] Documentación con README y endpoints
* [ ] Video demostrativo de máximo tres minutos
