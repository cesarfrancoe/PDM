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

**Nota avanzada:** para evitar errores relacionados con iOS, se recomienda comentar `include(":iosApp")` en `settings.gradle.kts` y condicionar la configuración de los targets iOS en `shared/build.gradle.kts` usando `if (System.getProperty("os.name").contains("Mac"))`.

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

## Generación del proyecto

Para esta práctica se utilizará el generador oficial de JetBrains para crear un proyecto base donde la lógica de negocio es compartida, pero la interfaz gráfica se desarrolla de forma independiente en cada plataforma.

### Pasos para generar el proyecto:

1. Ingresar a la plataforma oficial:
   [https://kmp.jetbrains.com](https://kmp.jetbrains.com)

2. Completar los siguientes campos:

   * **Project name**: `FavoritePlacesPro`
   * **Target platforms**: Android e iOS
   * **UI Implementation**:
     🔘 *Separate UIs (SwiftUI for iOS, Compose for Android)*

3. Hacer clic en **Download Project**.

4. Extraer el archivo `.zip` descargado y abrir el proyecto con Android Studio:
   `File > Open` → seleccionar la carpeta extraída.

5. Esperar la sincronización de Gradle.
   Android Studio configurará automáticamente los módulos:

   * `androidApp` (Jetpack Compose)
   * `iosApp` (SwiftUI)
   * `shared` (lógica común entre plataformas)

---

## Estructura del proyecto

El proyecto generado contiene tres módulos principales:

```
FavoritePlacesPro/
├── androidApp/           ← Aplicación Android con UI en Jetpack Compose
├── iosApp/               ← Aplicación iOS con UI en SwiftUI
└── shared/
    ├── build.gradle.kts
    └── src/
        ├── commonMain/   ← Lógica de negocio común (modelo y repositorio)
        ├── androidMain/  ← Código específico para Android
        └── iosMain/      ← Código específico para iOS
```

### Detalles por módulo:

* **`shared/`**: contiene todo el código compartido entre plataformas, incluyendo el modelo `Place` y la clase `PlaceRepository`. Este código está escrito en Kotlin.
* **`androidApp/`**: contiene la interfaz gráfica de Android implementada con Jetpack Compose.
* **`iosApp/`**: contiene la interfaz gráfica de iOS desarrollada en SwiftUI. Este módulo incluye archivos `.swift` y requiere Xcode para compilar y probar.

> A diferencia de la práctica anterior, en esta estructura se busca aprovechar al máximo los componentes nativos de cada sistema operativo, por lo que no se define una UI común en `commonMain`.

---

## Convención de nombres y organización del código por plataforma

Dado que la interfaz gráfica se implementa por separado en cada sistema operativo, es importante mantener una organización clara en ambos módulos (`androidApp` y `iosApp`).

### En Android (`androidApp`)

* Se recomienda usar el sufijo `Screen` para pantallas completas escritas con Jetpack Compose:

  * `HomeScreen.kt`
  * `DetailScreen.kt`
* Los componentes reutilizables pueden llevar sufijos como `Card`, `Item`, o `Section`:

  * `PlaceCard.kt`
  * `PlaceItem.kt`

> Esta convención sigue la misma lógica que en la práctica 1, pero se aplica exclusivamente en el módulo `androidApp`.

---

### En iOS (`iosApp`)

* En SwiftUI es habitual utilizar el sufijo `View` para las estructuras que definen pantallas o componentes de interfaz:

  * `HomeView.swift`
  * `PlaceCellView.swift`

> Aunque Swift permite otras convenciones, `View` es el estándar más extendido y favorece la comprensión inmediata del propósito de cada archivo.

---

### Código compartido (`shared`)

* El módulo `shared` debe contener únicamente lógica de negocio, modelos de datos y repositorios.
* Se mantiene la convención de organizar los paquetes por función:

  * `model` → entidades de datos como `Place.kt`
  * `data` → acceso a datos como `PlaceRepository.kt`

---

## Implementación del modelo y repositorio en `shared`

Todo el código en esta sección debe ubicarse dentro del módulo `shared`, específicamente en el subdirectorio `commonMain`.

### Modelo de datos `Place`

Representa un lugar favorito con identificador, nombre y descripción.

**Ruta del archivo:**
`shared/src/commonMain/kotlin/org/example/favoriteplaces/model/Place.kt`

```kotlin
package org.example.favoriteplaces.model

data class Place(
    val id: Int,
    val name: String,
    val description: String
)
```

---

### Repositorio `PlaceRepository`

Simula una fuente de datos fija. Esta clase puede ser utilizada desde Android y iOS para obtener la misma lista de lugares.

**Ruta del archivo:**
`shared/src/commonMain/kotlin/org/example/favoriteplaces/data/PlaceRepository.kt`

```kotlin
package org.example.favoriteplaces.data

import org.example.favoriteplaces.model.Place

class PlaceRepository {
    fun getAllPlaces(): List<Place> {
        return listOf(
            Place(1, "Mount Fuji", "Iconic volcano in Japan"),
            Place(2, "Eiffel Tower", "Famous landmark in Paris"),
            Place(3, "Grand Canyon", "Impressive natural formation in the USA")
        )
    }
}
```

> Esta lógica es reutilizada por ambos entornos de interfaz (Jetpack Compose y SwiftUI) mediante interoperabilidad multiplataforma.

---

## Interfaz de usuario en Android (Jetpack Compose)

La interfaz en Android se implementa de forma independiente, pero consume la lógica compartida del módulo `shared`.

### Pantalla principal `HomeScreen.kt`

**Ruta del archivo:**
`androidApp/src/main/java/org/example/favoriteplaces/android/ui/HomeScreen.kt`

```kotlin
package org.example.favoriteplaces.android.ui

import androidx.compose.foundation.layout.*
import androidx.compose.material3.*
import androidx.compose.runtime.*
import androidx.compose.ui.Modifier
import androidx.compose.ui.unit.dp
import org.example.favoriteplaces.data.PlaceRepository

@Composable
fun HomeScreen() {
    val repository = remember { PlaceRepository() }
    val places = remember { repository.getAllPlaces() }

    Column(modifier = Modifier.padding(16.dp)) {
        Text("Favorite Places", style = MaterialTheme.typography.headlineMedium)

        Spacer(modifier = Modifier.height(16.dp))

        places.forEach { place ->
            PlaceCard(place)
            Spacer(modifier = Modifier.height(8.dp))
        }
    }
}
```

---

### Componente reutilizable `PlaceCard.kt`

**Ruta del archivo:**
`androidApp/src/main/java/org/example/favoriteplaces/android/ui/PlaceCard.kt`

```kotlin
package org.example.favoriteplaces.android.ui

import androidx.compose.foundation.layout.*
import androidx.compose.foundation.shape.RoundedCornerShape
import androidx.compose.material3.*
import androidx.compose.runtime.Composable
import androidx.compose.ui.Modifier
import androidx.compose.ui.unit.dp
import org.example.favoriteplaces.model.Place

@Composable
fun PlaceCard(place: Place) {
    Card(
        modifier = Modifier.fillMaxWidth(),
        shape = RoundedCornerShape(12.dp),
        elevation = CardDefaults.cardElevation(4.dp)
    ) {
        Column(modifier = Modifier.padding(16.dp)) {
            Text(text = place.name, style = MaterialTheme.typography.titleMedium)
            Spacer(modifier = Modifier.height(4.dp))
            Text(text = place.description, style = MaterialTheme.typography.bodyMedium)
        }
    }
}
```

---

### Actividad principal `MainActivity.kt`

**Ruta del archivo:**
`androidApp/src/main/java/org/example/favoriteplaces/android/MainActivity.kt`

```kotlin
package org.example.favoriteplaces.android

import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import org.example.favoriteplaces.android.ui.HomeScreen

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            HomeScreen()
        }
    }
}
```

> Esta implementación aprovecha completamente Jetpack Compose, pero se mantiene aislada del módulo `shared`, reutilizando únicamente los modelos y datos.

---

## Interfaz de usuario en iOS (SwiftUI)

En esta práctica, la interfaz de usuario para iOS se implementa directamente con SwiftUI, aprovechando los componentes nativos de Apple. La lógica de negocio proviene del módulo `shared` gracias a la interoperabilidad entre Kotlin/Native y Swift.

### Vista principal `HomeView.swift`

**Ruta del archivo:**
`iosApp/iosApp/HomeView.swift`

```swift
import SwiftUI
import shared

struct HomeView: View {
    private let repository = PlaceRepository()

    var body: some View {
        let places = repository.getAllPlaces()

        NavigationView {
            List(places, id: \.id) { place in
                PlaceCellView(place: place)
            }
            .navigationTitle("Favorite Places")
        }
    }
}
```

---

### Componente `PlaceCellView.swift`

**Ruta del archivo:**
`iosApp/iosApp/PlaceCellView.swift`

```swift
import SwiftUI
import shared

struct PlaceCellView: View {
    let place: Place

    var body: some View {
        VStack(alignment: .leading, spacing: 4) {
            Text(place.name)
                .font(.headline)
            Text(place.description_)
                .font(.subheadline)
        }
        .padding(8)
    }
}
```

> ⚠️ **Nota:** como `description` es una palabra reservada en Swift, Kotlin/Native la expone automáticamente como `description_` cuando se accede desde Swift.

---

### Entrada principal `iOSApp.swift`

**Ruta del archivo:**
`iosApp/iosApp/iOSApp.swift`

```swift
import SwiftUI

@main
struct iOSApp: App {
    var body: some Scene {
        WindowGroup {
            HomeView()
        }
    }
}
```

> Esta estructura permite que la interfaz gráfica de iOS sea totalmente nativa, mientras reutiliza la lógica de negocio escrita en Kotlin.

