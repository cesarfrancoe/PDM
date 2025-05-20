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

   * **Project Name**: `FavoritePlacesPro`
   * **Project ID**: `org.example.favoriteplacepro.android`
   * **Target platforms**: Android y iOS
   * **UI Implementation**: Do not share UI (use only SwiftUI)

3. Hacer clic en **Download Project**.

4. Extraer el archivo `.zip` descargado y abrir el proyecto con Android Studio:
   `File > Open` → seleccionar la carpeta extraída.

5. Esperar la sincronización de Gradle.
   Android Studio configurará automáticamente los módulos:

   * `composeApp` (Jetpack Compose)

   * `iosApp` (SwiftUI)

   * `shared` (lógica común entre plataformas)

   > ⚠️ Si Android Studio sugiere actualizar el **Android Gradle Plugin (AGP)**, selecciona la opción **"Don't ask for this project"** para evitar conflictos con la configuración de Kotlin Multiplatform.

---

## Estructura del proyecto

El proyecto generado contiene los siguientes módulos principales:

```
FavoritePlacesPro/
├── composeApp/           ← Aplicación Android con interfaz Jetpack Compose
├── iosApp/               ← Aplicación iOS con interfaz SwiftUI
│   ├── iosApp/
│   └── iosApp.xcodeproj
└── shared/               ← Módulo compartido (modelo y lógica)
    ├── src/commonMain/
    ├── src/androidMain/
    └── src/iosMain/
```

### Detalles por módulo:

* **`composeApp/`**: contiene el código de la aplicación Android. Aquí se desarrolla toda la interfaz utilizando Jetpack Compose. Incluye:

  * `MainActivity.kt`: actividad principal de Android.
  * `App.kt`: punto de entrada a la interfaz.

* **`iosApp/`**: contiene la aplicación para iOS. Toda la interfaz se implementa usando SwiftUI, organizada dentro de `iosApp/iosApp`.

* **`shared/`**: contiene la lógica compartida entre plataformas. Se encuentra estructurada en tres carpetas:

  * `commonMain`: definición del modelo `Place` y el repositorio dinámico `PlaceStore`.
  * `androidMain`: puede incluir código específico para Android (si se requiere).
  * `iosMain`: puede incluir código específico para iOS (si se requiere).

---

## Convención de nombres y organización del código por plataforma

Dado que la interfaz gráfica se implementa por separado en cada sistema operativo, se recomienda seguir una convención de nombres coherente en cada plataforma para mantener el código organizado y comprensible.

### En Android (`composeApp`)

* Los archivos que definen pantallas completas deben usar el sufijo `Screen`, por ejemplo:

  * `HomeScreen.kt`
  * `AddPlaceScreen.kt`

* Los componentes visuales reutilizables pueden usar el sufijo `Row`, siguiendo el estilo común para listas:

  * `PlaceRow.kt`

> Todos los archivos de interfaz en Android se ubican dentro de `composeApp/src/androidMain/kotlin`.

---

### En iOS (`iosApp`)

* Los archivos que definen pantallas completas en SwiftUI deben usar el sufijo `View`, por ejemplo:

  * `HomeView.swift`
  * `AddPlaceView.swift`

* Los componentes visuales reutilizables dentro de listas pueden usar el sufijo `Row`:

  * `PlaceRow.swift`

> Todos los archivos de interfaz para iOS se ubican en `iosApp/iosApp`.

---

### Código compartido (`shared`)

* El módulo `shared` contiene exclusivamente la lógica de negocio común (modelo y repositorio).
* Se recomienda organizar el código en subpaquetes:

  * `model` → para clases como `Place.kt`
  * `data` → para clases como `PlaceStore.kt`

---

## Implementación paso a paso

---

## Organización del código

Antes de comenzar con la implementación, asegúrate de crear las siguientes carpetas (si no existen), para mantener una organización limpia del proyecto:

### En `shared` (código común)

```
shared/
└── src/
    └── commonMain/
        └── kotlin/
            └── org/
                └── example/
                    └── favoriteplacespro/
                        ├── model/      ← Aquí se ubica Place.kt
                        └── data/       ← Aquí se ubica PlaceStore.kt
```

### En `composeApp` (interfaz de Android)

```
composeApp/
└── src/
    └── androidMain/
        └── kotlin/
            └── org/
                └── example/
                    └── favoriteplacespro/
                        └── android/
                            └── ui/     ← Aquí van HomeScreen.kt, AddPlaceScreen.kt, PlaceRow.kt
```

> Las carpetas pueden crearse directamente desde Android Studio (New > Package) o desde el explorador de archivos.

---

### Paso 1: Definición del modelo `Place`

Se define la estructura básica de un lugar, con los atributos `id`, `name` y `description`. Este modelo se declara en el módulo compartido `shared` y será reutilizado por las interfaces de Android e iOS.

**Ruta del archivo:**
`shared/src/commonMain/kotlin/org/example/favoriteplacespro/model/Place.kt`

```kotlin
package org.example.favoriteplacespro.model

data class Place(
    val id: Int,
    val name: String,
    val description: String
)
```

> Este modelo será expuesto automáticamente a Swift como `Place`, y su campo `description` será accesible desde Swift como `description_`, ya que `description` es una palabra reservada en ese lenguaje.

---

### Paso 2: Repositorio de datos dinámico `PlaceStore`

Este repositorio mantiene una lista observable de lugares mediante un `StateFlow`, lo que permite actualizar la UI en Android automáticamente y acceder a los datos desde Swift en iOS.

Antes de implementar `PlaceStore`, es importante tener en cuenta que este repositorio utiliza **corutinas** y `StateFlow`. Por lo tanto, es necesario realizar una configuración previa en el módulo `shared`.

#### 📌 Configuración previa para usar corutinas (versión moderna con `libs.versions.toml`)

1. Abre el archivo `libs.versions.toml` (ubicado usualmente en `gradle/libs.versions.toml`) y agrega lo siguiente:

```toml
[versions]
coroutines = "1.8.0"

[libraries]
kotlinx-coroutines-core = { module = "org.jetbrains.kotlinx:kotlinx-coroutines-core", version.ref = "coroutines" }
```

> Si estás usando el formato XML (`libs.versions.xml`), agrega estas entradas de forma equivalente en las secciones `[versions]` y `[libraries]`.

2. Luego, abre el archivo `shared/build.gradle.kts` y asegúrate de incluir la dependencia de corutinas en `commonMain`:

```kotlin
kotlin {
    sourceSets {
        commonMain.dependencies {
            implementation(libs.kotlinx.coroutines.core)
        }
    }
}
```

3. Sincroniza el proyecto para aplicar los cambios.
4. Crear `PlaceStore.kt`.

**Ruta del archivo:**
`shared/src/commonMain/kotlin/org/example/favoriteplacespro/data/PlaceStore.kt`

```kotlin
package org.example.favoriteplacespro.data

import kotlinx.coroutines.flow.MutableStateFlow
import kotlinx.coroutines.flow.StateFlow
import org.example.favoriteplacespro.model.Place

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

    fun getPlacesSnapshot(): List<Place> = places.value
}
```

> Este objeto puede usarse directamente en Compose (con `collectAsState`) y desde Swift como `PlaceStore.shared`.

---

### Paso 3: Pantallas `AddPlaceScreen.kt` y `AddPlaceView.swift` para registrar nuevos lugares

Estas pantallas permiten al usuario ingresar el nombre y la descripción de un nuevo lugar. Al presionar "Guardar", se agrega a la lista observable a través de `PlaceStore`.

---

#### Android – `AddPlaceScreen.kt`

**Ruta del archivo:**
`composedApp/src/main/java/org/example/favoriteplacespro/android/ui/AddPlaceScreen.kt`

```kotlin
package org.example.favoriteplacespro.android.ui

import androidx.compose.foundation.layout.*
import androidx.compose.material3.*
import androidx.compose.runtime.*
import androidx.compose.ui.Modifier
import androidx.compose.ui.unit.dp
import org.example.favoriteplacespro.data.PlaceStore

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
import Shared

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
`composeApp/src/main/java/org/example/favoriteplacespro/android/ui/PlaceRow.kt`

```kotlin
package org.example.favoriteplacespro.android.ui

import androidx.compose.foundation.layout.*
import androidx.compose.material3.*
import androidx.compose.runtime.Composable
import androidx.compose.ui.Modifier
import androidx.compose.ui.unit.dp
import org.example.favoriteplacespro.model.Place

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
import Shared

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
`composeApp/src/main/java/org/example/favoriteplacespro/android/ui/HomeScreen.kt`

```kotlin
package org.example.favoriteplacespro.android.ui

import androidx.compose.foundation.layout.*
import androidx.compose.material.icons.Icons
import androidx.compose.material.icons.filled.Add
import androidx.compose.material3.*
import androidx.compose.runtime.*
import androidx.compose.ui.Modifier
import androidx.compose.ui.unit.dp
import org.example.favoriteplacespro.data.PlaceStore

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
import Shared

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
        places = PlaceStore.shared.getPlacesSnapshot() as? [Place] ?? []
    }
}

struct HomeView_Previews: PreviewProvider {
    static var previews: some View {
        HomeView()
    }
}
```

---

### Paso 5: Puntos de entrada en `MainActivity.kt` y `iOSApp.swift`

---

#### Android – `MainActivity.kt`

**Ruta del archivo:**
`composeApp/src/main/java/org/example/favoriteplacespro/android/MainActivity.kt`

```kotlin
package org.example.favoriteplacepro.android

import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.activity.enableEdgeToEdge
import androidx.compose.runtime.Composable
import androidx.compose.ui.tooling.preview.Preview
import org.example.favoriteplacespro.android.ui.HomeScreen

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        enableEdgeToEdge()
        super.onCreate(savedInstanceState)

        setContent {
            HomeScreen()
        }
    }
}

@Preview
@Composable
fun AppAndroidPreview() {
    HomeScreen()
}
```

> Esta es la actividad principal de Android. Llama a `HomeScreen`, que ya maneja internamente la navegación hacia `AddPlaceScreen`.

---

#### iOS – `iOSApp.swift`

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

