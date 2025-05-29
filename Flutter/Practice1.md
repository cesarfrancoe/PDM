# 📘 Práctica 1: Favorite Places

**Interfaz desarrollada con Flutter (Multiplataforma Android & iOS)**

---

## ✅ Requisitos técnicos

A continuación se detallan los requisitos recomendados por sistema operativo para desarrollar esta práctica con Flutter:

### Para usuarios de macOS

* macOS 12 o superior
* Flutter SDK (versión estable más reciente)
* Android Studio o Visual Studio Code
* Xcode instalado (incluye el simulador de iOS)
* Emulador Android funcional
* Java 17 o superior (si usas Android Studio)
* Dart y Flutter correctamente configurados (`flutter doctor` debe estar en verde)

> Esta configuración permite desarrollar y probar la App en Android e iOS desde el mismo equipo.

---

### Para usuarios de Windows

* Windows 10 o superior
* Flutter SDK (versión estable más reciente)
* Android Studio o Visual Studio Code
* Emulador Android funcional
* Java 17 o superior (si usas Android Studio)
* Dart y Flutter correctamente configurados (`flutter doctor` debe estar en verde)

> Esta configuración permite desarrollar y probar la App únicamente en Android.

---

### Para usuarios de distribuciones Linux

* Distribución moderna (por ejemplo, Ubuntu 22.04, Fedora 38)
* Flutter SDK (versión estable más reciente)
* Android Studio o Visual Studio Code
* Emulador Android funcional
* Java 17 o superior (si usas Android Studio)
* Dart y Flutter correctamente configurados (`flutter doctor` debe estar en verde)

> Esta configuración permite desarrollar y probar la App únicamente en Android.

---

## 🧰 Generación del proyecto

### Pasos para generar el proyecto base:

1. Abrir una terminal o línea de comandos.
2. Ejecutar el siguiente comando para crear un nuevo proyecto Flutter:

```bash
flutter create favorite_places
```

3. Acceder a la carpeta del proyecto:

```bash
cd favorite_places
```

4. Abrir el proyecto en Android Studio o VS Code:

```bash
code .    # si usas Visual Studio Code
```

5. Ejecutar `flutter doctor` y solucionar posibles advertencias o errores.

> Este comando crea un proyecto base con la estructura estándar de Flutter, listo para desarrollar una aplicación multiplataforma.

---

## 📁 Estructura del proyecto

Después de crear el proyecto, encontrarás una estructura como la siguiente:

```
favorite_places/
├── android/               ← Código nativo Android
├── ios/                   ← Código nativo iOS
├── lib/                   ← Código principal de la aplicación (Dart)
│   ├── main.dart          ← Punto de entrada
│   ├── models/            ← Definición del modelo Place
│   ├── screens/           ← Pantallas (Home, Add)
│   ├── widgets/           ← Componentes reutilizables (PlaceCard)
│   └── data/              ← Repositorio estático (PlaceStore)
├── pubspec.yaml           ← Archivo de configuración del proyecto
└── test/                  ← Pruebas unitarias (opcional en esta práctica)
```

> Todo el desarrollo principal se realiza dentro de la carpeta `lib/`.

---

## 🚀 Implementación paso a paso

---

## 📁 Organización del código

Antes de comenzar con la implementación, asegúrate de crear las siguientes carpetas dentro del directorio `lib/` para mantener una estructura clara y modular:

```
lib/
├── data/         ← Repositorio y lógica de datos (place_store.dart)
├── models/       ← Definición del modelo Place (place.dart)
├── screens/      ← Pantallas principales (home_screen.dart, add_place_screen.dart)
└── widgets/      ← Componentes visuales reutilizables (place_row.dart)
```

> Puedes crear estas carpetas desde tu IDE o directamente desde el explorador de archivos.

---

### 🧱 Paso 1: Definición del modelo `Place`

**Ruta del archivo:**
`lib/models/place.dart`

```dart
class Place {
  final int id;
  final String name;
  final String description;

  Place({
    required this.id,
    required this.name,
    required this.description,
  });
}
```

> Esta clase representa un lugar favorito. Más adelante se puede extender para incluir otros atributos como ubicación o imagen.

---

### 📦 Paso 2: Repositorio de datos dinámico `PlaceStore`

**Ruta del archivo:**
`lib/data/place_store.dart`

```dart
import 'package:flutter/foundation.dart';
import '../models/place.dart';

class PlaceStore extends ChangeNotifier {
  final List<Place> _places = [
    Place(id: 1, name: 'Mount Fuji', description: 'Iconic volcano in Japan'),
    Place(id: 2, name: 'Eiffel Tower', description: 'Famous landmark in Paris'),
    Place(id: 3, name: 'Grand Canyon', description: 'Impressive natural formation in the USA'),
  ];

  List<Place> get places => List.unmodifiable(_places);

  void addPlace(String name, String description) {
    final newPlace = Place(
      id: (_places.isNotEmpty ? _places.map((p) => p.id).reduce((a, b) => a > b ? a : b) : 0) + 1,
      name: name,
      description: description,
    );
    _places.add(newPlace);
    notifyListeners();
  }
}
```

> Este repositorio utiliza `ChangeNotifier` para actualizar la interfaz automáticamente cuando se agregan nuevos lugares.

---

### 📝 Paso 3: Pantalla para registrar nuevos lugares (`AddPlaceScreen`)

Esta pantalla permite al usuario agregar un nuevo lugar. Contiene un formulario con campos de texto para el nombre y la descripción. Al presionar el botón “Guardar”, se actualiza el repositorio y se retorna a la pantalla principal.

**Ruta del archivo:**
`lib/screens/add_place_screen.dart`

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';
import '../data/place_store.dart';

class AddPlaceScreen extends StatefulWidget {
  final VoidCallback onPlaceAdded;

  const AddPlaceScreen({super.key, required this.onPlaceAdded});

  @override
  State<AddPlaceScreen> createState() => _AddPlaceScreenState();
}

class _AddPlaceScreenState extends State<AddPlaceScreen> {
  final _nameController = TextEditingController();
  final _descController = TextEditingController();

  @override
  void dispose() {
    _nameController.dispose();
    _descController.dispose();
    super.dispose();
  }

  void _savePlace() {
    final name = _nameController.text.trim();
    final desc = _descController.text.trim();

    if (name.isNotEmpty && desc.isNotEmpty) {
      Provider.of<PlaceStore>(context, listen: false).addPlace(name, desc);
      widget.onPlaceAdded();
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('New Place')),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          children: [
            TextField(
              controller: _nameController,
              decoration: const InputDecoration(labelText: 'Name'),
            ),
            const SizedBox(height: 12),
            TextField(
              controller: _descController,
              decoration: const InputDecoration(labelText: 'Description'),
            ),
            const SizedBox(height: 24),
            ElevatedButton(
              onPressed: _savePlace,
              child: const Text('Save'),
            ),
            TextButton(
              onPressed: () => Navigator.pop(context),
              child: const Text('Cancel'),
            ),
          ],
        ),
      ),
    );
  }
}
```

---

### 🧩 Paso 4: Componente visual reutilizable (`PlaceRow`)

Este widget representa visualmente un lugar individual. Se utiliza dentro de la pantalla principal para mostrar la lista de lugares.

**Ruta del archivo:**
`lib/widgets/place_row.dart`

```dart
import 'package:flutter/material.dart';
import '../models/place.dart';

class PlaceRow extends StatelessWidget {
  final Place place;

  const PlaceRow({super.key, required this.place});

  @override
  Widget build(BuildContext context) {
    return Column(
      crossAxisAlignment: CrossAxisAlignment.start,
      children: [
        Text(place.name, style: Theme.of(context).textTheme.titleMedium),
        const SizedBox(height: 4),
        Text(place.description, style: Theme.of(context).textTheme.bodyMedium),
      ],
    );
  }
}
```

---

### 🏠 Paso 5: Pantalla principal (`HomeScreen`)

Esta pantalla muestra el título de la App y la lista completa de lugares. Utiliza `Consumer` para observar el repositorio `PlaceStore` y renderiza la interfaz con un botón flotante para agregar lugares.

**Ruta del archivo:**
`lib/screens/home_screen.dart`

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';
import '../data/place_store.dart';
import '../widgets/place_row.dart';
import 'add_place_screen.dart';

class HomeScreen extends StatelessWidget {
  const HomeScreen({super.key});

  @override
  Widget build(BuildContext context) {
    final places = context.watch<PlaceStore>().places;

    return Scaffold(
      appBar: AppBar(title: const Text('Favorite Places')),
      body: ListView.separated(
        padding: const EdgeInsets.all(16),
        itemCount: places.length,
        separatorBuilder: (_, __) => const SizedBox(height: 12),
        itemBuilder: (context, index) {
          return PlaceRow(place: places[index]);
        },
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          Navigator.push(
            context,
            MaterialPageRoute(
              builder: (_) => AddPlaceScreen(
                onPlaceAdded: () => Navigator.pop(context),
              ),
            ),
          );
        },
        child: const Icon(Icons.add),
      ),
    );
  }
}
```

---

### 🏁 Paso 6: Punto de entrada (`main.dart`)

Este archivo configura la aplicación, registra el proveedor `PlaceStore` usando `ChangeNotifierProvider` y define la pantalla inicial (`HomeScreen`).

**Ruta del archivo:**
`lib/main.dart`

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';
import 'data/place_store.dart';
import 'screens/home_screen.dart';

void main() {
  runApp(const FavoritePlacesApp());
}

class FavoritePlacesApp extends StatelessWidget {
  const FavoritePlacesApp({super.key});

  @override
  Widget build(BuildContext context) {
    return ChangeNotifierProvider(
      create: (_) => PlaceStore(),
      child: MaterialApp(
        debugShowCheckedModeBanner: false,
        title: 'Favorite Places',
        theme: ThemeData(
          colorScheme: ColorScheme.fromSeed(seedColor: Colors.indigo),
          useMaterial3: true,
        ),
        home: const HomeScreen(),
      ),
    );
  }
}
```
