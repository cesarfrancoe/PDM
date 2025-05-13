# Práctica 2: Favorite Places Pro

**Interfaz nativa por plataforma: Jetpack Compose (Android) + SwiftUI (iOS)**

---

## Requisitos técnicos

A continuación se detallan los requisitos recomendados por sistema operativo para desarrollar esta práctica, que utiliza Kotlin Multiplatform para compartir la lógica de negocio, pero implementa la interfaz gráfica de forma nativa en cada plataforma:

### Para usuarios de macOS

* macOS 12 o superior
* Android Studio (versión 2023.1.1 o superior recomendada)
* Xcode instalado (versión 14 o superior)
* Plugin **Kotlin Multiplatform** habilitado en Android Studio
* Simulador de iOS disponible (Xcode > Preferences > Components)
* Emulador de Android configurado y funcional
* Java 17 o superior correctamente instalado
* SDK de Android y Kotlin configurados
* Swift configurado (preinstalado con Xcode)

**Nota:** esta configuración es indispensable para compilar, ejecutar y probar las aplicaciones tanto en Android como en iOS. La UI de iOS se desarrolla directamente en SwiftUI dentro del módulo `iosApp`.

---

### Para usuarios de Windows

* Windows 10 o superior
* Android Studio (versión 2023.1.1 o superior recomendada)
* Plugin **Kotlin Multiplatform** habilitado en Android Studio
* Emulador de Android configurado y funcional
* Java 17 o superior correctamente instalado
* SDK de Android y Kotlin configurados

**Nota:** esta configuración permite desarrollar y probar únicamente la parte Android de la aplicación. No es posible compilar ni ejecutar el módulo iOS (`iosApp`) desde Windows.
**Nota avanzada:** si deseas evitar errores de compilación relacionados con archivos `.swift`, puedes comentar la línea `include(":iosApp")` en el archivo `settings.gradle.kts`. Para mayor estabilidad, también puedes condicionar la configuración de los targets iOS en `shared/build.gradle.kts` verificando que el sistema operativo sea macOS.

---

### Para usuarios de distribuciones Linux

* Distribución moderna (por ejemplo, Ubuntu 22.04, Fedora 38, etc.)
* Android Studio (versión 2023.1.1 o superior recomendada)
* Plugin **Kotlin Multiplatform** habilitado en Android Studio
* Emulador de Android funcional (requiere KVM o VirtualBox)
* Java 17 o superior correctamente instalado
* SDK de Android y Kotlin configurados

**Nota:** esta configuración permite desarrollar y probar únicamente la parte Android de la aplicación. No es posible compilar ni ejecutar el módulo iOS en sistemas Linux.
**Nota avanzada:** para evitar errores relacionados con iOS, se recomienda comentar `include(":iosApp")` en `settings.gradle.kts` y condicionar la configuración de los targets iOS en `shared/build.gradle.kts` usando `if (System.getProperty("os.name").contains("Mac"))`.

---

