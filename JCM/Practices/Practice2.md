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
   * **UI Implementation**: Do not share UI (use only SwiftUI)

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

Perfecto. A continuación iniciaremos la sección **“Implementación paso a paso”** de la **Práctica 2 – Favorite Places Pro**, con la estructura actualizada, incluyendo:

* `PlaceRow` como componente reutilizable
* Pantalla `AddPlaceView.swift` y `AddPlaceScreen.kt`
* Navegación en ambas plataformas
* FAB en Android
* Interfaz nativa en cada sistema

---

## Implementación paso a paso

### Paso 1: Definición del modelo `Place`

Se define la estructura básica de un lugar, con los atributos `id`, `name` y `description`. Este modelo se declara en el módulo compartido `shared` y será reutilizado por las interfaces de Android e iOS.

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

> Este modelo será expuesto automáticamente a Swift como `Place`, y su campo `description` será accesible desde Swift como `description_`, ya que `description` es una palabra reservada en ese lenguaje.

---

### Paso 2: Repositorio de datos dinámico `PlaceStore`

Este repositorio reemplaza al repositorio estático tradicional. Mantiene una lista observable de lugares mediante un `StateFlow`, lo que permite actualizar la UI en Android automáticamente y acceder a los datos desde Swift en iOS.

**Ruta del archivo:**
`shared/src/commonMain/kotlin/org/example/favoriteplaces/data/PlaceStore.kt`

```kotlin
package org.example.favoriteplaces.data

import kotlinx.coroutines.flow.MutableStateFlow
import kotlinx.coroutines.flow.StateFlow
import org.example.favoriteplaces.model.Place

object PlaceStore {
    private val _places = MutableStateFlow(
        listOf(
            Place(1, "Mount Fuji", "Iconic volcano in Japan"),
            Place(2, "Eiffel Tower", "Famous landmark in Paris"),
            Place(3, "Grand Canyon", "Impressive natural formation in the USA")
        )
    )

    val places: StateFlow<List<Place>> = _places

    fun addPlace(name: String, description: String) {
        val current = _places.value
        val newPlace = Place(
            id = (current.maxOfOrNull { it.id } ?: 0) + 1,
            name = name,
            description = description
        )
        _places.value = current + newPlace
    }
}
```

> Este objeto puede usarse directamente en Compose (con `collectAsState`) y desde Swift como `PlaceStore.shared`.

---

### Paso 3: Pantallas `AddPlaceScreen.kt` y `AddPlaceView.swift` para registrar nuevos lugares

Estas pantallas permiten al usuario ingresar el nombre y la descripción de un nuevo lugar. Al presionar "Guardar", se agrega a la lista observable a través de `PlaceStore`.

---

#### Android – `AddPlaceScreen.kt`

**Ruta del archivo:**
`androidApp/src/main/java/org/example/favoriteplaces/android/ui/AddPlaceScreen.kt`

```kotlin
package org.example.favoriteplaces.android.ui

import androidx.compose.foundation.layout.*
import androidx.compose.material3.*
import androidx.compose.runtime.*
import androidx.compose.ui.Modifier
import androidx.compose.ui.unit.dp
import org.example.favoriteplaces.data.PlaceStore

@Composable
fun AddPlaceScreen(onBack: () -> Unit) {
    var name by remember { mutableStateOf("") }
    var description by remember { mutableStateOf("") }

    Column(modifier = Modifier.padding(16.dp)) {
        Text("New Place", style = MaterialTheme.typography.headlineMedium)
        Spacer(modifier = Modifier.height(16.dp))

        OutlinedTextField(
            value = name,
            onValueChange = { name = it },
            label = { Text("Name") },
            modifier = Modifier.fillMaxWidth()
        )

        Spacer(modifier = Modifier.height(8.dp))

        OutlinedTextField(
            value = description,
            onValueChange = { description = it },
            label = { Text("Description") },
            modifier = Modifier.fillMaxWidth()
        )

        Spacer(modifier = Modifier.height(24.dp))

        Button(
            onClick = {
                if (name.isNotBlank() && description.isNotBlank()) {
                    PlaceStore.addPlace(name, description)
                    onBack()
                }
            },
            modifier = Modifier.fillMaxWidth(),
            enabled = name.isNotBlank() && description.isNotBlank()
        ) {
            Text("Save")
        }

        Spacer(modifier = Modifier.height(8.dp))

        OutlinedButton(onClick = onBack, modifier = Modifier.fillMaxWidth()) {
            Text("Cancel")
        }
    }
}
```

---

#### iOS – `AddPlaceView.swift`

**Ruta del archivo:**
`iosApp/iosApp/AddPlaceView.swift`

```swift
import SwiftUI
import shared

struct AddPlaceView: View {
    @Environment(\.dismiss) var dismiss

    @State private var name: String = ""
    @State private var description: String = ""

    var body: some View {
        VStack(alignment: .leading, spacing: 12) {
            Text("New Place")
                .font(.title2)

            TextField("Name", text: $name)
                .textFieldStyle(.roundedBorder)

            TextField("Description", text: $description)
                .textFieldStyle(.roundedBorder)

            Spacer()

            Button("Save") {
                if !name.isEmpty && !description.isEmpty {
                    PlaceStore.shared.addPlace(name: name, description: description)
                    dismiss()
                }
            }
            .frame(maxWidth: .infinity)
            .buttonStyle(.borderedProminent)

            Button("Cancel") {
                dismiss()
            }
            .frame(maxWidth: .infinity)
        }
        .padding()
        .navigationTitle("Add Place")
    }
}
```

---

### Paso 4: Pantalla Principal

### Componente auxiliar `PlaceRow`

Este componente se utiliza dentro de `HomeScreen` (en Android) y `HomeView` (en iOS) para renderizar de forma uniforme cada elemento de la lista.

---

#### Android – `PlaceRow.kt`

**Ruta del archivo:**
`androidApp/src/main/java/org/example/favoriteplaces/android/ui/PlaceRow.kt`

```kotlin
package org.example.favoriteplaces.android.ui

import androidx.compose.foundation.layout.*
import androidx.compose.material3.*
import androidx.compose.runtime.Composable
import androidx.compose.ui.Modifier
import androidx.compose.ui.unit.dp
import org.example.favoriteplaces.model.Place

@Composable
fun PlaceRow(place: Place) {
    Column(modifier = Modifier
        .fillMaxWidth()
        .padding(8.dp)) {
        Text(text = place.name, style = MaterialTheme.typography.titleMedium)
        Spacer(modifier = Modifier.height(2.dp))
        Text(text = place.description, style = MaterialTheme.typography.bodyMedium)
    }
}
```

---

#### iOS – `PlaceRow.swift`

**Ruta del archivo:**
`iosApp/iosApp/PlaceRow.swift`

```swift
import SwiftUI
import shared

struct PlaceRow: View {
    let place: Place

    var body: some View {
        VStack(alignment: .leading, spacing: 4) {
            Text(place.name)
                .font(.headline)
            Text(place.description_)
                .font(.subheadline)
        }
        .padding(.vertical, 6)
    }
}
```

> En Swift, `description` se accede como `description_` por ser palabra reservada.

---

### Paso pantallas principales con navegación y lista de lugares

---

#### Android – `HomeScreen.kt` con FAB y `Scaffold`

**Ruta del archivo:**
`androidApp/src/main/java/org/example/favoriteplaces/android/ui/HomeScreen.kt`

```kotlin
package org.example.favoriteplaces.android.ui

import androidx.compose.foundation.layout.*
import androidx.compose.material.icons.Icons
import androidx.compose.material.icons.filled.Add
import androidx.compose.material3.*
import androidx.compose.runtime.*
import androidx.compose.ui.Modifier
import androidx.compose.ui.unit.dp
import org.example.favoriteplaces.data.PlaceStore

@Composable
fun HomeScreen() {
    var showForm by remember { mutableStateOf(false) }

    if (showForm) {
        AddPlaceScreen(onBack = { showForm = false })
    } else {
        val places by PlaceStore.places.collectAsState()

        Scaffold(
            floatingActionButton = {
                FloatingActionButton(onClick = { showForm = true }) {
                    Icon(Icons.Default.Add, contentDescription = "Add Place")
                }
            }
        ) { paddingValues ->
            Column(
                modifier = Modifier
                    .padding(paddingValues)
                    .padding(16.dp)
            ) {
                Text("Favorite Places", style = MaterialTheme.typography.headlineMedium)

                Spacer(modifier = Modifier.height(16.dp))

                places.forEach { place ->
                    PlaceRow(place)
                    Spacer(modifier = Modifier.height(8.dp))
                }
            }
        }
    }
}
```

---

#### iOS – `HomeView.swift` con `NavigationView` y `.sheet`

**Ruta del archivo:**
`iosApp/iosApp/HomeView.swift`

```swift
import SwiftUI
import shared

struct HomeView: View {
    @State private var places: [Place] = []
    @State private var showForm = false

    var body: some View {
        NavigationView {
            List(places, id: \.id) { place in
                PlaceRow(place: place)
            }
            .navigationTitle("Favorite Places")
            .toolbar {
                ToolbarItem(placement: .navigationBarTrailing) {
                    Button {
                        showForm = true
                    } label: {
                        Image(systemName: "plus")
                    }
                }
            }
            .onAppear {
                loadPlaces()
            }
            .sheet(isPresented: $showForm, onDismiss: loadPlaces) {
                AddPlaceView()
            }
        }
    }

    func loadPlaces() {
        places = PlaceStore.shared.places as? [Place] ?? []
    }
}
```

---
Perfecto. Finalizamos la sección de implementación paso a paso con el **Paso 5: Puntos de entrada en Android e iOS**.

Este paso asegura que la ejecución de la app inicie desde las pantallas principales (`HomeScreen` en Android y `HomeView` en iOS), que ahora incorporan navegación y permiten agregar lugares.

---

### Paso 5: Puntos de entrada en `MainActivity.kt` y `iOSApp.swift`

---

#### Android – `MainActivity.kt`

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

> Esta es la actividad principal de Android. Llama a `HomeScreen`, que ya maneja internamente la navegación hacia `AddPlaceScreen`.

---

#### 🟩 iOS – `iOSApp.swift`

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

> Esta es la estructura de entrada principal en SwiftUI. Llama a `HomeView`, que contiene la lista de lugares y el acceso al formulario `AddPlaceView`.

