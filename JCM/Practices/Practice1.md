# Práctica 1: Favorite Places

**Interfaz compartida con Jetpack Compose Multiplatform**

---

## Requisitos técnicos

A continuación se detallan los requisitos recomendados por sistema operativo para desarrollar esta práctica con Jetpack Compose Multiplatform:

### Para usuarios de macOS

* macOS 12 o superior
* Android Studio (versión 2023.1.1 o superior recomendada)
* Xcode instalado (incluye el simulador de iOS)
* Plugin **Kotlin Multiplatform** habilitado en Android Studio
* Simulador de iOS disponible (se puede activar desde Xcode > Preferences > Components)
* Emulador de Android configurado y funcional
* Java 17 o superior correctamente instalado
* SDK de Android y Kotlin configurados

**Nota:** esta configuración permite compilar y ejecutar la aplicación tanto en Android como en iOS desde el mismo equipo.

---

### Para usuarios de Windows

* Windows 10 o superior
* Android Studio (versión 2023.1.1 o superior recomendada)
* Plugin **Kotlin Multiplatform** habilitado en Android Studio
* Emulador de Android configurado y funcional
* Java 17 o superior correctamente instalado
* SDK de Android y Kotlin configurados

**Nota:** esta configuración permite desarrollar y probar la aplicación únicamente en Android. No es posible compilar ni ejecutar la versión iOS desde Windows.

---

### Para usuarios de distribuciones Linux

* Distribución moderna (por ejemplo, Ubuntu 22.04, Fedora 38, etc.)
* Android Studio (versión 2023.1.1 o superior recomendada)
* Plugin **Kotlin Multiplatform** habilitado en Android Studio
* Emulador de Android funcional (requiere KVM o VirtualBox)
* Java 17 o superior correctamente instalado
* SDK de Android y Kotlin configurados

**Nota:** esta configuración permite desarrollar y probar la aplicación únicamente en Android. No es posible compilar ni ejecutar la versión iOS en sistemas Linux.

---

## Generación del proyecto

Para esta práctica se utilizará el generador oficial en línea de JetBrains para crear el proyecto base.

### Pasos para generar el proyecto:

1. Ingresar a la plataforma oficial:
   [https://kmp.jetbrains.com](https://kmp.jetbrains.com)

2. Completar los siguientes campos:

   * **Project name**: `FavoritePlaces`
   * **Target platforms**: Android e iOS
   * **UI Implementation**:
     🔘 *Share UI (with Compose Multiplatform UI framework)*

3. Hacer clic en **Download Project**.

4. Extraer el archivo `.zip` descargado y abrir el proyecto desde Android Studio:

   * `File > Open` → seleccionar la carpeta extraída.

5. Esperar la sincronización automática de Gradle. Si es necesario, actualizar los complementos y aceptar las recomendaciones del IDE.

> Esta configuración crea un proyecto donde tanto la lógica como la interfaz de usuario se encuentran en el módulo `composeApp`, específicamente en el subdirectorio `commonMain`.

---

## Estructura del proyecto

Una vez generado y abierto el proyecto en Android Studio, encontrarás una organización de módulos similar a la siguiente:

```
FavoritePlaces/
├── androidApp/           ← Aplicación Android
├── iosApp/               ← Aplicación iOS (solo compila en macOS)
└── composeApp/
    ├── build.gradle.kts
    └── src/
        ├── commonMain/   ← Lógica de negocio y UI compartida (Jetpack Compose)
        ├── androidMain/  ← Código específico para Android (si se necesita)
        └── iosMain/      ← Código específico para iOS (si se necesita)
```

### Notas importantes:

* Todo el desarrollo de la lógica y la interfaz de usuario se realiza en `commonMain`.
* El módulo `composeApp` contiene todo el código reutilizable.
* Los módulos `androidApp` e `iosApp` son los puntos de entrada específicos de cada plataforma, pero **no es necesario modificar su contenido para esta práctica**.

---

## Convención de nombres para pantallas y componentes

Para mantener una organización clara y coherente en el módulo `commonMain`, se recomienda seguir las siguientes convenciones al nombrar los archivos de interfaz de usuario:

### Pantallas completas (`Screens`)

Los archivos que contienen pantallas completas (composables principales) deben usar el sufijo `Screen`, por ejemplo:

* `HomeScreen.kt` – pantalla principal con la lista de lugares
* `AddPlaceScreen.kt` – pantalla para registrar un nuevo lugar
* `DetailScreen.kt` – pantalla para mostrar los detalles de un lugar

### Componentes reutilizables

Los componentes internos o reutilizables pueden usar sufijos como:

* `Card`: para tarjetas visuales → `PlaceCard.kt`
* `Item`: para elementos de listas → `PlaceItem.kt`
* `Cell`: si se adopta terminología común en iOS → `PlaceCell.kt`

> Esta convención facilita la lectura del proyecto y la navegación dentro del código, especialmente cuando el proyecto crece.

---


