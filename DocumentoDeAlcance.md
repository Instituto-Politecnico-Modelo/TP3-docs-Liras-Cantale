# DOCUMENTO DE ALCANCE DEL PROYECTO
## GymRat Tracker — App de Progreso de Entrenamiento
### Trabajo Práctico — Email de Cliente

| Campo | Detalle |
|---|---|
| **Materia** | Desarrollo de Sistemas |
| **Institución** | Instituto Politécnico Modelo |
| **Fecha** | Marzo 2026 |

---

## 1. Descripción General del Sistema

El presente proyecto consiste en el desarrollo de una aplicación móvil multiplataforma para el seguimiento de entrenamiento físico en gimnasios. La aplicación permitirá a los alumnos registrar sus ejercicios, pesos y repeticiones, visualizar su progreso a lo largo del tiempo, y compartir logros con sus compañeros de grupo.

El sistema surge a partir del requerimiento expresado por el cliente, quien necesita reemplazar el registro manual en cuadernos por una solución digital accesible desde el celular. Un punto clave es que la aplicación debe funcionar sin conexión a internet, dado que las instalaciones del gimnasio (subsuelo) no cuentan con señal.

La aplicación también incluirá análisis de técnica en tiempo real mediante la cámara del dispositivo, y una red social interna cerrada para fomentar la comunidad entre alumnos.

---

## 2. Objetivos del Proyecto

### 2.1 Objetivo General

Desarrollar una aplicación móvil multiplataforma que permita a los alumnos de un gimnasio registrar y visualizar su progreso de entrenamiento, recibir correcciones de postura en tiempo real y compartir logros, funcionando de forma autónoma sin requerir conexión a internet.

### 2.2 Objetivos Específicos

- Permitir el registro de ejercicios con los campos Ejercicio, Kilos y Repeticiones por sesión.
- Visualizar la evolución del rendimiento mediante gráficos históricos por ejercicio.
- Analizar la técnica del alumno en tiempo real usando la cámara del dispositivo y brindar correcciones de postura.
- Proveer una red social interna cerrada donde los alumnos puedan publicar fotos y reaccionar a las publicaciones de sus compañeros.
- Garantizar el funcionamiento completo de la app sin conexión a internet.
- Ofrecer una experiencia equivalente en dispositivos Android e iOS.

---

## 3. Alcance Funcional — IN SCOPE

Las siguientes funcionalidades están confirmadas dentro del alcance del proyecto:

| Funcionalidad | Estado |
|---|---|
| Registro de entrenamiento: Ejercicio, Kilos y Repeticiones por sesión | ✅ INCLUIDO |
| Creación, edición y eliminación de entradas de entrenamiento | ✅ INCLUIDO |
| Historial de sesiones por alumno | ✅ INCLUIDO |
| Gráfico de evolución de peso y repeticiones por ejercicio | ✅ INCLUIDO |
| Vista de resumen semanal y mensual de entrenamiento | ✅ INCLUIDO |
| Panel de administración web para el entrenador | ✅ INCLUIDO |
| Registro público de usuarios (el alta la gestiona el entrenador) | ✅ INCLUIDO |
| Soporte multiplataforma: Android e iOS con experiencia equivalente | ✅ INCLUIDO |

---

## 4. Alcance Funcional — OUT OF SCOPE

Las siguientes funcionalidades quedan fuera del alcance de este proyecto, ya sea por implicar integraciones externas, hardware adicional o estar fuera del contexto del trabajo práctico:

| Funcionalidad | Estado |
|---|---|
| Planes de entrenamiento personalizados | ❌ EXCLUIDO |
| Integración con wearables (smartwatch, sensores externos) | ❌ EXCLUIDO |
| Pagos o suscripciones in-app | ❌ EXCLUIDO |
| Soporte para múltiples gimnasios u organizaciones | ❌ EXCLUIDO |
| Moderación de contenido en la red social | ❌ EXCLUIDO |
| Exportación de datos (PDF, CSV, Excel) | ❌ EXCLUIDO |
| Análisis de postura en tiempo real mediante cámara del dispositivo | ❌ EXCLUIDO |
| Alertas visuales y sonoras al detectar mala técnica | ❌ EXCLUIDO |
| Red social interna: perfil de usuario con foto | ❌ EXCLUIDO |
| Red social interna: publicación de fotos de progreso | ❌ EXCLUIDO |
| Red social interna: feed de publicaciones del grupo | ❌ EXCLUIDO |
| Red social interna: reacciones ("likes") entre alumnos | ❌ EXCLUIDO |
| Funcionamiento completo offline (sin conexión a internet) | ❌ EXCLUIDO  |
| Sincronización automática de datos al recuperar señal |  ❌ EXCLUIDO |

---

## 5. Usuarios del Sistema

| Rol | Descripción | Permisos principales |
|---|---|---|
| **Entrenador** | Administrador del grupo/clase | Alta de alumnos, acceso a todos los perfiles y reportes |
| **Alumno** | Usuario final de la aplicación | Registro de entrenamientos, visualización de progreso, uso de red social |

---

## 6. Arquitectura Técnica

El sistema seguirá una arquitectura cliente móvil con backend opcional para sincronización, priorizando el funcionamiento local en el dispositivo:

| Capa | Tecnología / Detalle |
|---|---|
| **Framework mobile** | React Native — desarrollo multiplataforma (Android e iOS) |
| **Almacenamiento local** | SQLite mediante AsyncStorage — persistencia offline |
| **Análisis de postura** | Modelo de ML on-device (TensorFlow Lite / MediaPipe) |
| **Gráficos** | React Native Charts / Victory Native |
| **Backend (sincronización)** | Node.js + Express — sincronización al recuperar señal |
| **Base de datos remota** | PostgreSQL — persistencia centralizada al sincronizar |
| **Autenticación** | JWT — obligatorio para todos los endpoints del backend |
| **Almacenamiento de imágenes** | Local en el dispositivo; sincronización diferida con servidor |

---

## 7. Supuestos

Para la realización de este proyecto se asumen las siguientes condiciones como verdaderas:

- Cada alumno posee un smartphone con cámara funcional (Android o iOS).
- El modelo de análisis de postura puede correr localmente en el dispositivo sin requerir servidor externo.
- La red social es cerrada: solo acceden alumnos del mismo gimnasio o grupo.
- El entrenador gestiona el alta de usuarios; no existe registro público ni autogestión de cuentas.
- El almacenamiento de fotos de la red social es local en el dispositivo; la sincronización con servidor es diferida.
- El sistema operará principalmente offline; la sincronización es secundaria y ocurre cuando hay señal disponible.
- El cliente proveerá las credenciales del servidor de producción para la fase de sincronización.
- No se requerirá moderación automatizada de contenido en la red social para esta versión.

---

## 8. Restricciones

- El stack tecnológico es fijo y no puede modificarse: React Native, SQLite, TensorFlow Lite / MediaPipe, Node.js y PostgreSQL.
- La aplicación debe funcionar sin ningún tipo de conexión a internet (todas las funcionalidades core deben estar disponibles offline).
- No se permite el uso de hardware externo ni sensores adicionales al propio smartphone del alumno.
- Toda funcionalidad debe estar cubierta por un issue en el tablero Kanban de GitHub Projects antes de ser implementada.
- Todo commit debe estar vinculado a al menos un issue mediante el número de issue en el mensaje de commit.
- La autenticación JWT es obligatoria en todos los endpoints protegidos del backend de sincronización.

---

## 9. Entidades Principales del Sistema

Las siguientes entidades conformarán el modelo de datos de la aplicación:

| Entidad | Atributos / Descripción |
|---|---|
| **Usuario** | id, nombre, apellido, email, passwordHash, rol (ENTRENADOR / ALUMNO), fotoPerfil |
| **Sesión** | id, usuario (FK), fecha, notas |
| **Entrada** | id, sesión (FK), ejercicio, kilos, repeticiones, orden |
| **Publicación** | id, usuario (FK), foto, descripción, fechaHora |
| **Reacción** | id, publicación (FK), usuario (FK), tipo (LIKE) |

---

## 10. Criterios de Aceptación

El proyecto se considerará completado cuando se cumplan todos los siguientes criterios:

- Un alumno puede registrar un ejercicio con kilos y repeticiones sin necesidad de conexión a internet.
- Los gráficos de progreso se actualizan correctamente al agregar nuevas entradas de entrenamiento.
- El análisis de postura por cámara funciona en tiempo real y emite alerta cuando detecta mala técnica.
- Un alumno puede publicar una foto en la red social y sus compañeros pueden reaccionar a ella.
- Toda la funcionalidad principal opera sin ningún tipo de señal o conexión a internet.
- La aplicación corre correctamente en un dispositivo Android y en un dispositivo iOS.
- La sincronización se activa automáticamente al detectar conexión disponible sin intervención del usuario.
- Todos los issues del Kanban están en estado Done al finalizar el proyecto.

