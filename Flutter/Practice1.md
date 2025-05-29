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

