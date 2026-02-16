# Tipos de Aplicaciones Móviles

## Arquitectura, Forma de Desarrollo y Herramientas Actuales

---

# 1. Clasificación de Aplicaciones Móviles

Las aplicaciones móviles pueden clasificarse desde **dos perspectivas diferentes**:

1. Según su **arquitectura cliente-servidor**
2. Según su **forma de desarrollo (tecnología utilizada)**

Es importante no mezclar estos conceptos.

---

# 2. Clasificación por Arquitectura

Esta clasificación responde a la pregunta:

> ¿Dónde se ejecuta la lógica de negocio y cómo se gestionan los datos?

## 2.1 Thin Client (Cliente Delgado)

* Toda la lógica de negocio está en el servidor.
* La aplicación solo muestra información y envía solicitudes.
* Requiere conexión permanente a Internet.

Ejemplos:

* Web Apps tradicionales
* Wrapper Apps (WebView que carga un sitio remoto)
* Oracle APEX

---

## 2.2 Thick Client (Cliente Grueso)

* Parte de la lógica se ejecuta en el dispositivo.
* Puede almacenar datos localmente.
* Puede funcionar parcialmente sin conexión.

Ejemplos:

* Flutter
* React Native
* Jetpack Compose Multiplatform
* Xamarin / .NET MAUI
* Ionic con almacenamiento local

---

## 2.3 Standalone

* Funciona completamente sin servidor.
* Toda la lógica y datos están en el dispositivo.

Ejemplos:

* Calculadoras
* Apps de edición offline
* Juegos sin conexión

---

# 3. Clasificación por Forma de Desarrollo

Esta clasificación responde a:

> ¿Cómo fue construida la aplicación?

---

## 3.1 Native Apps

Aplicaciones desarrolladas específicamente para cada sistema operativo.

Lenguajes:

* iOS: Swift, Objective-C
* Android: Kotlin, Java

Características:

* Acceso directo a APIs del sistema
* Mejor rendimiento
* UI completamente nativa

Ejemplo:

* WhatsApp
* Instagram (núcleo principal)
* Gmail

---

## 3.2 Hybrid Apps

Aplicaciones que usan tecnologías web (HTML, CSS, JS) dentro de una WebView, pero empaquetadas como app.

Frameworks:

* Ionic
* Apache Cordova
* Capacitor

Características:

* Un solo código base
* Acceso a funciones nativas mediante plugins
* Rendimiento inferior al nativo puro

---

## 3.3 Wrapper Apps

Aplicaciones que solo contienen un WebView que carga un sitio web remoto.

Características:

* No tienen lógica local
* Son Thin Client
* Pueden ser rechazadas por las tiendas si no agregan valor

Ejemplo:

* App que solo carga [https://miempresa.com](https://miempresa.com)

---

## 3.4 Progressive Web Apps (PWA)

Web Apps avanzadas que:

* Se pueden instalar
* Tienen ícono y splash screen
* Pueden funcionar offline (con Service Workers)

No son apps nativas, pero pueden parecerlo.

---

## 3.5 Multiplataforma Nativa (Cross-Platform Nativo)

No usan WebView. Generan UI nativa real.

### Flutter

* Lenguaje: Dart
* Renderizado: Motor propio (Skia)
* No usa componentes nativos estándar
* Alto rendimiento

### React Native

* Lenguaje: JavaScript / TypeScript
* Renderiza componentes nativos
* Usa bridge JS ↔ nativo
* Rendimiento medio-alto

### Jetpack Compose Multiplatform (JCM)

* Lenguaje: Kotlin
* Comparte lógica entre plataformas
* Renderiza UI nativa
* En Android usa Compose
* En iOS puede integrarse con UIKit o SwiftUI

### Xamarin / .NET MAUI

* Lenguaje: C#
* Usa bindings a componentes nativos
* Integración con ecosistema .NET

### Skip (skip.tools)

* Lenguaje: Swift
* Sintaxis inspirada en SwiftUI / React
* Compila a UI nativa en iOS y Android
* No usa WebView
* No usa bridge JS
* No depende de SwiftUI directamente

---

# 4. Ionic, Cordova y Capacitor

## 4.1 Apache Cordova

* Proyecto open source
* Permite empaquetar Web Apps como apps móviles
* Usa WebView
* Acceso a hardware mediante plugins

Limitaciones:

* Arquitectura antigua
* Plugins desactualizados
* Difícil mantenimiento en proyectos grandes

---

## 4.2 Capacitor

* Creado por el equipo de Ionic
* Sucesor moderno de Cordova
* Mejor integración con Android Studio y Xcode
* Soporte para PWA
* Plugins modernos

Actualmente es el runtime recomendado para Ionic.

---

# 5. Oracle APEX en Móvil

Oracle APEX:

* Es una plataforma low-code
* Genera Web Apps responsive
* No genera apps nativas

Clasificación:

* Forma de desarrollo: Web App
* Arquitectura: Thin Client

Puede convertirse en:

* Wrapper App
* PWA (con configuraciones adicionales)

---

# 6. Diferencia entre Componentes Nativos y Componentes Propios

## 6.1 Frameworks que usan Componentes Nativos

* React Native
* Xamarin
* Jetpack Compose
* Skip

Ventaja:

* UI coherente con el sistema
* Mejor integración

---

## 6.2 Frameworks que usan Componentes Propios

* Flutter
* Motores de juegos (Unity)

Ventaja:

* UI idéntica en todas las plataformas
* Control visual total

Desventaja:

* No sigue guías visuales nativas automáticamente

---

# 7. Qué usan las Grandes Empresas

## Google

* Kotlin + Jetpack Compose para Android
* Swift para iOS
* Flutter en proyectos específicos

## Microsoft

* .NET MAUI
* React Native
* Nativo cuando es necesario

## Meta

* React Native + código nativo
* Arquitectura híbrida

## Amazon

* Principalmente nativo
* Multiplataforma en herramientas internas

## Oracle

* Web empresarial (APEX)
* Integraciones móviles empresariales

---

# 8. Conclusión Académica

No existe una única tecnología correcta.

La elección depende de:

* Rendimiento requerido
* Experiencia de usuario
* Presupuesto
* Tiempo de desarrollo
* Acceso a hardware
* Escalabilidad futura
* Tamaño del equipo

---

# 9. Resumen Conceptual Final

Arquitectura:

* Thin Client
* Thick Client
* Standalone

Forma de desarrollo:

* Native
* Hybrid
* Wrapper
* PWA
* Multiplataforma Nativa

Motor de renderizado:

* Componentes nativos
* Componentes propios

