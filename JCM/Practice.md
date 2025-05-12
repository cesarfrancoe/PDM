# **Jetpack Compose Multiplatform (JCM)**

---

## **Introducción general**

### ¿Qué es Jetpack Compose Multiplatform?

**Jetpack Compose Multiplatform (JCM)** es un framework de interfaces de usuario creado por **JetBrains** (con el apoyo de **Google** para Android) que permite desarrollar apps modernas usando un solo lenguaje (**Kotlin**) y compartir el código en múltiples plataformas: Android, iOS, desktop y web.

---

### **¿Cómo funciona?**

* Se basa en **Kotlin Multiplatform**, lo que permite compartir tanto la lógica como las interfaces de usuario.
* Utiliza un enfoque **declarativo** mediante Jetpack Compose: describes cómo debe lucir la interfaz, en lugar de cómo construirla paso a paso.
* Ofrece una **integración nativa real**:

  * En Android, usa directamente Jetpack Compose sobre la JVM.
  * En iOS, se compila a código nativo mediante Kotlin/Native.

---

### **¿Qué se necesita?**

| Requisito              | Descripción                                                          |
| ---------------------- | -------------------------------------------------------------------- |
| **IDE**                | Android Studio o IntelliJ IDEA con soporte para Kotlin Multiplatform |
| **Lenguaje**           | Kotlin (con soporte multiplataforma)                                 |
| **Herramientas**       | Gradle, Kotlin/Native (iOS), Kotlin/JVM (Android)                    |
| **Simulador/Emulador** | Emulador de Android y/o simulador de iOS (requiere Xcode)            |

---

### **Comparación con otros frameworks multiplataforma**

| **Framework**                 | **Lenguaje**          | **Tipo de UI**                  | **Acceso nativo**          | **Reutilización lógica/UI** | **¿Usa UI nativa del sistema operativo?** |
| ----------------------------- | --------------------- | ------------------------------- | -------------------------- | --------------------------- | ----------------------------------------- |
| Jetpack Compose Multiplatform | Kotlin                | Declarativa (Compose)           | Total                      | Alta (incluye UI)           | Sí (100%)                                 |
| Flutter                       | Dart                  | Declarativa (Flutter UI)        | Alto (con plugins)         | Alta                        | No (UI propia de Flutter)                 |
| React Native                  | JavaScript            | Declarativa (JSX)               | Alto (a través de bridges) | Parcial                     | Parcial (usa bridges a nativos)           |
| Xamarin / .NET MAUI           | C#                    | Imperativa o declarativa (MAUI) | Alto                       | Parcial                     | Sí (usa controles nativos de .NET MAUI)   |
| Ionic                         | JavaScript/TypeScript | HTML + CSS                      | Limitado (usa WebView)     | Alta en web, baja nativa    | No (usa WebView)                          |

### 📝 **Nota**

**En esta tabla, “¿Usa UI nativa del sistema operativo?” indica si el framework convierte sus controles de interfaz en elementos nativos de la plataforma.**
Por ejemplo, **Jetpack Compose Multiplatform** transforma un botón en un control como `android.widget.Button` en Android o una vista nativa equivalente en iOS.
Esto garantiza una mejor integración visual, funcional y de accesibilidad.

En contraste, frameworks como **Flutter** dibujan sus propias interfaces sobre un lienzo gráfico, sin usar los controles nativos del sistema operativo.

## **Práctica 1 – Favorite Places (código 100% compartido)**

### 🎯 Objetivo de la práctica

Desarrollar desde cero una App multiplataforma (Android + iOS) utilizando únicamente código en el módulo `commonMain`, que permita:

* Ver una lista de lugares favoritos.
* Agregar nuevos lugares.
* Ver detalles de un lugar.
* Eliminar lugares.

Todo el código de la lógica y de la interfaz de usuario estará compartido entre plataformas.

---

### 🟦 Parte 1: Crear el proyecto desde Android Studio

1. Abre **Android Studio** y crea un nuevo proyecto:

   * Selecciona: **New Project > Multiplatform > Compose Multiplatform Application**.
   * Si no aparece esta plantilla, activa el plugin “Kotlin Multiplatform” desde **Settings > Plugins**.

2. Configura el proyecto:

   * **Name**: `FavoritePlaces`
   * **Language**: Kotlin
   * **Platforms**: Android e iOS
   * **Build System**: Gradle (Kotlin DSL)

3. Espera a que se sincronice el proyecto y verifica que se creen las siguientes carpetas:

```
shared/
 └─ src/
     ├─ commonMain/
     ├─ androidMain/
     └─ iosMain/
```

---

### 📄 Archivo: `Place.kt`

**Ubicación:** `shared/src/commonMain/kotlin/model/Place.kt`
**Propósito:** Este archivo define la clase de datos `Place`, que representa un lugar favorito con su ID, nombre, descripción y ciudad.

```kotlin
package model

// Data class that represents a Place with its ID, name, description, and city
data class Place(
    val id: Int,
    val name: String,
    val description: String,
    val city: String
)
```

---

### 📄 Archivo: `PlaceRepository.kt`

**Ubicación:** `shared/src/commonMain/kotlin/repository/PlaceRepository.kt`
**Propósito:** Este archivo implementa un repositorio en memoria para almacenar, consultar, agregar y eliminar lugares.

```kotlin
package repository

import model.Place
import kotlin.random.Random

// In-memory repository for managing favorite places
object PlaceRepository {
    private val places = mutableListOf<Place>()

    fun getAll(): List<Place> = places

    fun addPlace(name: String, description: String, city: String) {
        val newPlace = Place(
            id = Random.nextInt(),
            name = name,
            description = description,
            city = city
        )
        places.add(newPlace)
    }

    fun removePlace(id: Int) {
        places.removeIf { it.id == id }
    }
}
```

---

### 📄 Archivo: `App.kt`

**Ubicación:** `shared/src/commonMain/kotlin/ui/App.kt`
**Propósito:** Este archivo contiene la función principal `FavoritePlacesApp`, que sirve como punto de entrada de la interfaz y llama al componente de navegación.

```kotlin
package ui

import androidx.compose.runtime.Composable

// Entry point of the app that calls the navigation host
@Composable
fun FavoritePlacesApp() {
    NavigationHost()
}
```

---

### 📄 Archivo: `Navigation.kt`

**Ubicación:** `shared/src/commonMain/kotlin/ui/Navigation.kt`
**Propósito:** Define las pantallas disponibles y el flujo de navegación entre ellas usando una variable de estado.

```kotlin
package ui

import androidx.compose.runtime.*
import model.Place

// Screens used in the navigation flow
sealed class Screen {
    object Home : Screen()
    object Add : Screen()
    data class Detail(val place: Place) : Screen()
}

// Main navigation logic using simple state-based switching
@Composable
fun NavigationHost() {
    var screen by remember { mutableStateOf<Screen>(Screen.Home) }

    when (val current = screen) {
        is Screen.Home -> HomeScreen(
            onAdd = { screen = Screen.Add },
            onDetail = { place -> screen = Screen.Detail(place) }
        )
        is Screen.Add -> AddPlaceScreen(
            onBack = { screen = Screen.Home }
        )
        is Screen.Detail -> PlaceDetailScreen(
            place = current.place,
            onBack = { screen = Screen.Home }
        )
    }
}
```

---

### 📄 Archivo: `HomeScreen.kt`

**Ubicación:** `shared/src/commonMain/kotlin/ui/HomeScreen.kt`
**Propósito:** Muestra una lista de lugares con opción de navegar a la pantalla de detalles o agregar un nuevo lugar.

```kotlin
package ui

import androidx.compose.foundation.clickable
import androidx.compose.foundation.layout.*
import androidx.compose.foundation.lazy.LazyColumn
import androidx.compose.foundation.lazy.items
import androidx.compose.material3.*
import androidx.compose.runtime.*
import androidx.compose.ui.Modifier
import androidx.compose.ui.unit.dp
import model.Place
import repository.PlaceRepository

// Main screen showing the list of favorite places
@Composable
fun HomeScreen(
    onAdd: () -> Unit,
    onDetail: (Place) -> Unit
) {
    val places = remember { mutableStateListOf<Place>() }

    // Load initial data
    LaunchedEffect(Unit) {
        places.clear()
        places.addAll(PlaceRepository.getAll())
    }

    Column(Modifier.fillMaxSize().padding(16.dp)) {
        Text("Favorite Places", style = MaterialTheme.typography.headlineSmall)
        Spacer(Modifier.height(16.dp))

        LazyColumn(Modifier.weight(1f)) {
            items(places, key = { it.id }) { place ->
                Card(
                    modifier = Modifier
                        .fillMaxWidth()
                        .padding(vertical = 4.dp)
                        .clickable { onDetail(place) }
                ) {
                    Column(Modifier.padding(12.dp)) {
                        Text(place.name, style = MaterialTheme.typography.titleMedium)
                        Text(place.city, style = MaterialTheme.typography.bodyMedium)
                    }
                }
            }
        }

        Spacer(Modifier.height(8.dp))

        Button(onClick = onAdd, modifier = Modifier.fillMaxWidth()) {
            Text("Add New Place")
        }
    }
}
```
---

### 📄 Archivo: `AddPlaceScreen.kt`

**Ubicación:** `shared/src/commonMain/kotlin/ui/AddPlaceScreen.kt`
**Propósito:** Pantalla con formulario para ingresar un nuevo lugar. Incluye campos para nombre, descripción y ciudad. Al guardar, se agrega el lugar al repositorio y se vuelve a la pantalla principal.

```kotlin
package ui

import androidx.compose.foundation.layout.*
import androidx.compose.material3.*
import androidx.compose.runtime.*
import androidx.compose.ui.Modifier
import androidx.compose.ui.unit.dp
import repository.PlaceRepository

// Screen to add a new place to the list
@Composable
fun AddPlaceScreen(onBack: () -> Unit) {
    var name by remember { mutableStateOf("") }
    var description by remember { mutableStateOf("") }
    var city by remember { mutableStateOf("") }

    Column(Modifier.fillMaxSize().padding(16.dp)) {
        Text("Add Place", style = MaterialTheme.typography.headlineSmall)
        Spacer(Modifier.height(16.dp))

        OutlinedTextField(
            value = name,
            onValueChange = { name = it },
            label = { Text("Name") },
            modifier = Modifier.fillMaxWidth()
        )
        Spacer(Modifier.height(8.dp))

        OutlinedTextField(
            value = description,
            onValueChange = { description = it },
            label = { Text("Description") },
            modifier = Modifier.fillMaxWidth()
        )
        Spacer(Modifier.height(8.dp))

        OutlinedTextField(
            value = city,
            onValueChange = { city = it },
            label = { Text("City") },
            modifier = Modifier.fillMaxWidth()
        )
        Spacer(Modifier.height(16.dp))

        Button(
            onClick = {
                PlaceRepository.addPlace(name, description, city)
                onBack()
            },
            modifier = Modifier.fillMaxWidth(),
            enabled = name.isNotBlank() && city.isNotBlank()
        ) {
            Text("Save")
        }

        Spacer(Modifier.height(8.dp))

        OutlinedButton(onClick = onBack, modifier = Modifier.fillMaxWidth()) {
            Text("Cancel")
        }
    }
}
```

---

### 📄 Archivo: `PlaceDetailScreen.kt`

**Ubicación:** `shared/src/commonMain/kotlin/ui/PlaceDetailScreen.kt`
**Propósito:** Muestra los detalles de un lugar y ofrece la opción de eliminarlo o volver a la pantalla anterior.

```kotlin
package ui

import androidx.compose.foundation.layout.*
import androidx.compose.material3.*
import androidx.compose.runtime.*
import androidx.compose.ui.Modifier
import androidx.compose.ui.unit.dp
import model.Place
import repository.PlaceRepository

// Screen that shows the details of a selected place
@Composable
fun PlaceDetailScreen(
    place: Place,
    onBack: () -> Unit
) {
    Column(Modifier.fillMaxSize().padding(16.dp)) {
        Text("Place Details", style = MaterialTheme.typography.headlineSmall)
        Spacer(Modifier.height(16.dp))

        Text("Name: ${place.name}", style = MaterialTheme.typography.titleMedium)
        Text("City: ${place.city}", style = MaterialTheme.typography.bodyMedium)
        Spacer(Modifier.height(8.dp))
        Text("Description:", style = MaterialTheme.typography.titleSmall)
        Text(place.description)

        Spacer(Modifier.height(24.dp))

        Button(
            onClick = {
                PlaceRepository.removePlace(place.id)
                onBack()
            },
            modifier = Modifier.fillMaxWidth()
        ) {
            Text("Delete")
        }

        Spacer(Modifier.height(8.dp))

        OutlinedButton(
            onClick = onBack,
            modifier = Modifier.fillMaxWidth()
        ) {
            Text("Back")
        }
    }
}
```

Perfecto. A continuación comenzamos la **nueva versión de la Práctica 2**, con interfaz gráfica completamente **nativa en iOS usando SwiftUI**, y Jetpack Compose en Android.

---

## ✅ **Práctica 2 – Favorite Places Pro (UI nativa en cada plataforma)**

### 🎯 Objetivo de la práctica

Crear una aplicación multiplataforma con:

* ✅ Lógica de datos compartida en `commonMain`.
* ✅ Interfaz de usuario con **Jetpack Compose en Android**.
* ✅ Interfaz de usuario con **SwiftUI en iOS** (100% nativa).

Esta práctica permite a los estudiantes entender cómo reutilizar la lógica de negocio en Kotlin y desarrollar experiencias visuales optimizadas y nativas para cada plataforma.

---

### 🟦 Parte 1: Estructura del proyecto

#### ✅ Paso 1: Crear un nuevo proyecto Multiplatform

1. Abre **Android Studio** y selecciona:

   * **New Project > Compose Multiplatform Application**

2. Configura:

   * **Name**: `FavoritePlacesPro`
   * **Language**: Kotlin
   * **Platforms**: Android + iOS
   * **Build System**: Gradle (Kotlin DSL)

3. Espera a que se cree la siguiente estructura:

```
FavoritePlacesPro/
 ├─ androidApp/           ← Interfaz con Jetpack Compose
 ├─ iosApp/               ← Interfaz con SwiftUI
 └─ shared/
     └─ src/
         ├─ commonMain/   ← Lógica compartida (modelo + repositorio)
         ├─ androidMain/
         └─ iosMain/
```

---

### 🧩 ¿Qué se desarrollará en cada parte?

| Módulo        | Contenido                                                              |
| ------------- | ---------------------------------------------------------------------- |
| `commonMain`  | Modelo `Place`, repositorio `PlaceRepository`                          |
| `androidMain` | Pantallas con Jetpack Compose                                          |
| `iosApp`      | Pantallas con **SwiftUI (en Swift)**, accediendo a la lógica en Kotlin |

---





