# Guía Práctica – Jetpack Compose Multiplatform

## Introducción general

### Definición de Jetpack Compose Multiplatform

Jetpack Compose Multiplatform (JCM) es un framework moderno, declarativo y multiplataforma desarrollado en Kotlin. Permite construir interfaces gráficas reutilizables para Android, iOS, escritorio y web, a partir de una sola base de código. Se basa en el enfoque declarativo de Jetpack Compose, originalmente diseñado para Android, y lo extiende a múltiples plataformas a través de Kotlin Multiplatform (KMP).

---

### Arquitectura y funcionamiento

Jetpack Compose Multiplatform se apoya en Kotlin Multiplatform para compartir tanto la lógica de negocio como la interfaz gráfica. La estructura del proyecto se organiza en los siguientes módulos:

* `commonMain`: contiene la lógica compartida entre plataformas.
* `androidMain` y `iosMain`: contienen el código específico para cada plataforma.
* Si se desea compartir la UI, esta se define en `commonMain` utilizando Compose.

---

### Requisitos técnicos para el desarrollo

| Requisito    | Detalle                                                 |
| ------------ | ------------------------------------------------------- |
| IDE          | Android Studio                                          |
| Lenguaje     | Kotlin                                                  |
| Herramientas | Gradle, Kotlin Multiplatform, Compose, Kotlin/Native    |
| Simuladores  | Emulador de Android y simulador de iOS (requiere Xcode) |

---

### Instalación del plugin Kotlin Multiplatform

Antes de comenzar con cualquier práctica, es necesario tener instalado el siguiente complemento en Android Studio:

1. Abrir Android Studio
2. Ir a **Settings > Plugins > Marketplace**
3. Buscar **Kotlin Multiplatform**
4. Hacer clic en **Install** y reiniciar Android Studio

Este plugin habilita el soporte necesario para trabajar con proyectos Kotlin Multiplatform y Compose.

---

### Comparación con otros frameworks multiplataforma

| Framework                     | Lenguaje     | Tipo de UI               | Reutilización lógica/UI | Usa UI nativa del sistema operativo |
| ----------------------------- | ------------ | ------------------------ | ----------------------- | ----------------------------------- |
| Jetpack Compose Multiplatform | Kotlin       | Declarativa (Compose)    | Alta (UI compartida)    | Sí (solo en Android)                |
| Flutter                       | Dart         | Declarativa (Flutter UI) | Alta                    | No (usa motor gráfico propio)       |
| React Native                  | JavaScript   | Declarativa (JSX)        | Media                   | Parcial (usa puentes nativos)       |
| Xamarin / .NET MAUI           | C#           | Declarativa (XAML)       | Media                   | Sí (usa controles nativos)          |
| Ionic                         | JS/TS + HTML | Web UI + WebView         | Alta                    | No (usa WebView)                    |

**Nota:** “Usa UI nativa del sistema operativo” indica si el framework utiliza directamente componentes gráficos propios del sistema operativo (por ejemplo, `UIButton` en iOS o `android.widget.Button` en Android).
Tanto **Jetpack Compose Multiplatform** como **Flutter** utilizan **Skia**, un motor gráfico que dibuja directamente los elementos de la interfaz, lo que permite compartir la UI pero implica que **en iOS no se usan los componentes nativos de UIKit**.

---

## Descripción de las prácticas

### Práctica 1 – Favorite Places

Esta práctica consiste en desarrollar una aplicación multiplataforma con una única interfaz gráfica escrita en Compose Multiplatform. Tanto la lógica como la UI se encuentran en `commonMain`, lo que permite compartir todo el código entre Android e iOS.

**Tecnologías utilizadas:**

* Kotlin Multiplatform
* Jetpack Compose Multiplatform
* Gradle Kotlin DSL

---

### Práctica 2 – Favorite Places Pro

En esta práctica, la lógica de la aplicación se encuentra en `commonMain`, pero la interfaz se implementa de forma separada para cada plataforma: Compose para Android y SwiftUI para iOS. Esta arquitectura permite aprovechar los componentes nativos del sistema operativo.

**Tecnologías utilizadas:**

* Kotlin Multiplatform
* Jetpack Compose (Android)
* SwiftUI (iOS)

---

## Comparación entre las dos prácticas

| Aspecto                     | Práctica 1 – UI compartida                                | Práctica 2 – UI nativa por plataforma |
| --------------------------- | --------------------------------------------------------- | ------------------------------------- |
| Código reutilizado          | Toda la lógica y la UI                                    | Solo la lógica                        |
| UI en Android               | Jetpack Compose                                           | Jetpack Compose                       |
| UI en iOS                   | Renderizada con Skia (no UIKit nativa, similar a Flutter) | SwiftUI (nativa)                      |
| Desempeño visual en iOS     | Menor fidelidad                                           | Alta fidelidad                        |
| Curva de aprendizaje        | Más sencilla (solo Kotlin)                                | Más compleja (Kotlin + Swift)         |
| Mantenimiento               | Un solo código                                            | Código separado por plataforma        |
| Interoperabilidad requerida | No                                                        | Sí (Kotlin ↔ Swift)                   |

---

## Ventajas y desventajas de cada práctica

### Práctica 1 – Favorite Places (UI compartida)

**Ventajas:**

* Permite una alta reutilización de código, incluyendo lógica y UI.
* Requiere conocimientos de un solo lenguaje (Kotlin).
* Simplifica el mantenimiento: un solo flujo de desarrollo.
* Ideal para equipos pequeños y proyectos MVP.
* Facilita la evolución y escalabilidad hacia escritorio o web.

**Desventajas:**

* En iOS, la UI no es nativa (usa Skia, el mismo motor gráfico que Flutter), lo que puede afectar la experiencia del usuario.
* Algunas animaciones o componentes específicos de iOS pueden no replicarse fielmente.
* Menor integración con el ecosistema de diseño y accesibilidad de iOS.

---

### Práctica 2 – Favorite Places Pro (UI nativa por plataforma)

**Ventajas:**

* Ofrece una experiencia visual totalmente nativa en cada plataforma.
* Permite el uso directo de SwiftUI en iOS y Jetpack Compose en Android.
* Mayor fidelidad al diseño y comportamiento de cada sistema operativo.
* Posibilita un mejor aprovechamiento de APIs y componentes específicos.

**Desventajas:**

* La interfaz debe desarrollarse dos veces, lo que aumenta el esfuerzo.
* Requiere conocimientos de Swift y Kotlin, así como herramientas distintas (Xcode y Android Studio).
* Mayor complejidad técnica al trabajar con interoperabilidad Kotlin ↔ Swift.
* El mantenimiento puede ser más costoso si las plataformas divergen.

