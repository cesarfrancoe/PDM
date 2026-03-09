# Práctica 1: Favorite Places

**Interfaz compartida con Jetpack Compose Multiplatform**

---

## Requisitos técnicos

A continuación se detallan los requisitos recomendados por sistema operativo para desarrollar esta práctica con Jetpack Compose Multiplatform:

### Para usuarios de macOS

* macOS 12 o superior
* Android Studio (versión 2023.1.1 o superior recomendada)
* Xcode instalado (incluye el simulador de iOS)
* Simulador de iOS disponible (se puede activar desde Xcode > Preferences > Components)
* Emulador de Android configurado y funcional
* Java 17 o superior correctamente instalado
* SDK de Android y Kotlin configurados

**Nota:** esta configuración permite compilar y ejecutar la aplicación tanto en Android como en iOS desde el mismo equipo.

---

### Para usuarios de Windows

* Windows 10 o superior
* Android Studio (versión 2023.1.1 o superior recomendada)
* Emulador de Android configurado y funcional
* Java 17 o superior correctamente instalado
* SDK de Android y Kotlin configurados

**Nota:** esta configuración permite desarrollar y probar la aplicación únicamente en Android. No es posible compilar ni ejecutar la versión iOS desde Windows.

---

### Para usuarios de distribuciones Linux

* Distribución moderna (por ejemplo, Ubuntu 22.04, Fedora 38, etc.)
* Android Studio (versión 2023.1.1 o superior recomendada)
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

## Implementación paso a paso

### Paso 1: Definición del modelo `Place`

Este modelo representa la estructura básica de un lugar favorito, incluyendo un identificador, un nombre y una descripción.

**Ruta del archivo:**
`composeApp/src/commonMain/kotlin/org/example/favoriteplaces/model/Place.kt`

```kotlin
package org.example.favoriteplaces.model

data class Place(
    val id: Int,
    val name: String,
    val description: String
)
```

> Este modelo puede extenderse en futuras prácticas para incluir otros atributos como ubicación geográfica o imagen asociada.

---

### Paso 2: Repositorio de datos

Este repositorio contiene una función que devuelve una lista estática de lugares favoritos. Simula una fuente de datos local que en futuras versiones podría conectarse a una base de datos o servicio remoto.

**Ruta del archivo:**
`composeApp/src/commonMain/kotlin/org/example/favoriteplaces/data/PlaceRepository.kt`

```kotlin
package org.example.favoriteplaces.data

import org.example.favoriteplaces.model.Place
import kotlinx.coroutines.flow.MutableStateFlow
import kotlinx.coroutines.flow.StateFlow

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

> Este repositorio es útil para separar la lógica de datos de la interfaz, facilitando pruebas y mantenimiento del código.

---

### Paso 3: Pantalla principal `HomeScreen`

Esta pantalla es la responsable de mostrar el título de la app y la lista de lugares favoritos utilizando un diseño vertical. Recupera los datos desde el repositorio y los renderiza mediante tarjetas (`PlaceCard`).

**Ruta del archivo:**
`composeApp/src/commonMain/kotlin/org/example/favoriteplaces/ui/HomeScreen.kt`

```kotlin
@Composable
fun HomeScreen(onAdd: () -> Unit) {
    val places by PlaceStore.places.collectAsState()

    Column(modifier = Modifier.padding(16.dp)) {
        Text("Favorite Places", style = MaterialTheme.typography.headlineMedium)

        Spacer(modifier = Modifier.height(16.dp))

        places.forEach { place ->
            PlaceCard(place)
            Spacer(modifier = Modifier.height(8.dp))
        }

        Spacer(modifier = Modifier.height(24.dp))

        Button(onClick = onAdd, modifier = Modifier.fillMaxWidth()) {
            Text("Add Place")
        }
    }
}
```

> Esta pantalla actúa como punto central de la interfaz. Se puede extender en futuras prácticas para incluir navegación o filtrado.

---

### Paso 4: Pantalla `AddPlaceScreen`

Esta pantalla permite al usuario ingresar un nuevo lugar a través de un formulario compuesto por campos de texto para el nombre y la descripción. Al presionar el botón "Guardar", se agrega el nuevo lugar a la lista compartida a través de PlaceStore, y se retorna automáticamente a la pantalla principal.

**Ruta del archivo:**
`composeApp/src/commonMain/kotlin/org/example/favoriteplaces/ui/AddPlaceScreen.kt`

```kotlin
package org.example.favoriteplaces.ui

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

### Paso 5: Componente reutilizable `PlaceCard`

Este componente muestra los datos de un solo lugar dentro de una tarjeta con estilo Material Design. Se utiliza dentro de `HomeScreen` para renderizar cada elemento de la lista.

**Ruta del archivo:**
`composeApp/src/commonMain/kotlin/org/example/favoriteplaces/ui/PlaceCard.kt`

```kotlin
package org.example.favoriteplaces.ui

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
            Text(
                text = place.name,
                style = MaterialTheme.typography.titleMedium
            )
            Spacer(modifier = Modifier.height(4.dp))
            Text(
                text = place.description,
                style = MaterialTheme.typography.bodyMedium
            )
        }
    }
}
```

> Este componente es completamente reutilizable y se puede adaptar fácilmente para mostrar otros atributos o estilos personalizados.

---

### Paso 6: Punto de entrada `App.kt`

Este archivo define la función `App()`, que actúa como punto de entrada composable compartido entre Android e iOS. Desde aquí se invoca directamente la pantalla principal `HomeScreen`.

**Ruta del archivo:**
`composeApp/src/commonMain/kotlin/org/example/favoriteplaces/App.kt`

```kotlin
package org.example.favoriteplaces

import androidx.compose.runtime.*
import org.example.favoriteplaces.ui.AddPlaceScreen
import org.example.favoriteplaces.ui.HomeScreen

@Composable
fun App() {
    var currentScreen by remember { mutableStateOf("home") }

    if (currentScreen == "home") {
        HomeScreen(onAdd = { currentScreen = "add" })
    } else {
        AddPlaceScreen(onBack = { currentScreen = "home" })
    }
}
```

> Tanto la aplicación Android como la iOS renderizan esta función como su interfaz inicial, permitiendo que toda la UI esté centralizada en `commonMain`.

---

### Paso 7: Integración en Android e iOS

En esta práctica, no es necesario implementar código específico para cada plataforma. Los módulos `androidApp` e `iosApp` ya están configurados para mostrar directamente la interfaz declarada en `App()`.

#### Android

**Archivo:**
`androidApp/src/main/java/.../MainActivity.kt`

Este archivo ya incluye el punto de entrada para Android:

```kotlin
package org.example.favoriteplaces.android

import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import org.example.favoriteplaces.App

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            App()
        }
    }
}
```

#### iOS

**Archivo:**
`iosApp/iosApp.swift`

Este archivo está preconfigurado con Swift para ejecutar el punto de entrada:

```swift
import SwiftUI
import shared

@main
struct iOSApp: App {
    var body: some Scene {
        WindowGroup {
            ContentView() // usa ComposeUIViewController
        }
    }
}
```

**`ContentView.swift`**:

```swift
import shared
import SwiftUI

struct ContentView: UIViewControllerRepresentable {
    func makeUIViewController(context: Context) -> UIViewController {
        return MainViewControllerKt.MainViewController()
    }

    func updateUIViewController(_ uiViewController: UIViewController, context: Context) {}
}
```

> Estos archivos ya están listos desde el proyecto generado en [kmp.jetbrains.com](https://kmp.jetbrains.com) y no requieren modificación para esta práctica. Ambos utilizan la función `App()` definida en `commonMain`.

