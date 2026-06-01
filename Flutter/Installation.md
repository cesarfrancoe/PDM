# Guía de instalación de Flutter

# Introducción

Flutter es un framework de desarrollo multiplataforma que permite crear aplicaciones móviles para Android e iOS a partir de una única base de código utilizando el lenguaje Dart.

Aunque el código fuente es compartido, el resultado del proceso de compilación son dos aplicaciones independientes: una aplicación Android, distribuida normalmente en formatos `.apk` o `.aab`, y una aplicación iOS, distribuida normalmente en formato `.ipa`. Debido a ello, cada plataforma requiere herramientas específicas para compilar, ejecutar y probar las aplicaciones generadas.

Para Android se requiere el Android SDK, incluido en Android Studio. Para iOS se requiere adicionalmente Xcode, herramienta oficial de Apple disponible únicamente para macOS.

Es importante tener en cuenta que, aunque Flutter permite desarrollar aplicaciones para Android e iOS desde macOS, Windows y Linux, únicamente macOS permite compilar, ejecutar y probar aplicaciones iOS. Por esta razón, los desarrolladores que necesiten trabajar con dispositivos iPhone o simuladores iOS deben utilizar obligatoriamente un equipo Mac.

Esta guía describe el proceso de instalación y configuración de Flutter en macOS, Windows y Linux, incluyendo las herramientas necesarias para desarrollar, compilar, ejecutar y probar aplicaciones móviles en cada plataforma.

# 1. Instalación en macOS

## 1.1 Requisitos del sistema

### Hardware

* Computadora Apple (Mac)
* Arquitectura del procesador: Intel x86_64 o Apple Silicon ARM64 (M1, M2, M3, etc.) **(recomendado)**
* Memoria RAM: 8 GB mínimo o 16 GB **(recomendado)**
* Almacenamiento disponible: 10 GB mínimo o 20 GB o más **(recomendado)**

### Sistema operativo

* macOS 14 (Sonoma) o superior **(recomendado)**

### Herramientas requeridas

* Visual Studio Code **(recomendado)**

  Editor recomendado para el desarrollo con Flutter. Requiere instalar las extensiones Flutter y Dart.

* Android Studio

  Incluye Android SDK y Android Emulator.

  Guía de creación del emulador Android:

  [https://github.com/cesarfrancoe/PDM/blob/main/Tools/AndroidStudio/Emulator.md](https://github.com/cesarfrancoe/PDM/blob/main/Tools/AndroidStudio/Emulator.md)

* Xcode

  Incluye iOS Simulator.

  Guías:

  * Instalación de Xcode:

    [https://github.com/cesarfrancoe/PDM/blob/main/Tools/Xcode/README.md](https://github.com/cesarfrancoe/PDM/blob/main/Tools/Xcode/README.md)

  * Creación del simulador iOS:

    [https://github.com/cesarfrancoe/PDM/blob/main/Tools/Xcode/Simulator.md](https://github.com/cesarfrancoe/PDM/blob/main/Tools/Xcode/Simulator.md)

* Git

### Medio de ejecución

#### iOS

* Simulador iOS o dispositivo iPhone físico **(recomendado)**

#### Android

* Emulador Android o dispositivo Android físico **(recomendado)**

### Notas importantes

* Permite desarrollo, compilación y ejecución para Android e iOS.

* Los dispositivos físicos son recomendados porque ofrecen mayor rendimiento, pruebas más reales y menor consumo de recursos del equipo de desarrollo.

* El simulador iOS solo funciona en macOS y requiere Xcode.

* Flutter genera aplicaciones Android (`.apk` / `.aab`) y aplicaciones iOS (`.ipa`).

* Visual Studio Code no incluye Android SDK, por lo que se requiere instalar adicionalmente Android Studio o configurar el SDK manualmente.

---

## 1.2 Instalación y configuración de Xcode

Seguir la guía:

[https://github.com/cesarfrancoe/PDM/blob/main/Tools/Xcode/README.md](https://github.com/cesarfrancoe/PDM/blob/main/Tools/Xcode/README.md)

---

## 1.3 Creación del simulador iOS

Seguir la guía:

[https://github.com/cesarfrancoe/PDM/blob/main/Tools/Xcode/Simulator.md](https://github.com/cesarfrancoe/PDM/blob/main/Tools/Xcode/Simulator.md)

---

## 1.4 Verificación de Xcode

Verificar instalación:

```bash
xcode-select -p
```

Verificar versión:

```bash
xcodebuild -version
```

Verificar Command Line Tools:

```bash
xcode-select --install
```

---

## 1.5 Configuración básica de Xcode

Aceptar licencia:

```bash
sudo xcodebuild -license accept
```

Configurar el directorio de desarrollo:

```bash
sudo xcode-select -s /Applications/Xcode.app/Contents/Developer
```

---

## 1.6 Instalación del SDK de Flutter

### Descargar Flutter

Descargar el SDK desde:

[https://flutter.dev](https://flutter.dev)

Guardar el archivo descargado en la carpeta **Descargas**.

---

### Descomprimir Flutter

Descomprimir el archivo descargado. Como resultado se creará una carpeta llamada:

```text
~/Downloads/flutter
```

---

### Mover Flutter a la carpeta Library

Abrir Terminal y ejecutar:

```bash
mv ~/Downloads/flutter ~/Library
```

Verificar:

```bash
ls ~/Library/flutter
```

La ubicación final deberá ser:

```text
~/Library/flutter
```

y el ejecutable principal deberá encontrarse en:

```text
~/Library/flutter/bin/flutter
```

---

## 1.7 Configuración del PATH

Editar el archivo de configuración de Zsh:

```bash
nano ~/.zshrc
```

Agregar la siguiente línea:

```bash
export PATH="$PATH:$HOME/Library/flutter/bin"
```

Aplicar los cambios:

```bash
source ~/.zshrc
```

---

## 1.8 Verificación de Flutter

Verificar la instalación:

```bash
flutter doctor
```

Este comando detecta dependencias faltantes y sugiere acciones correctivas.

---

## 1.9 Configuración Android

Seguir la guía:

[https://github.com/cesarfrancoe/PDM/blob/main/Tools/AndroidStudio/Emulator.md](https://github.com/cesarfrancoe/PDM/blob/main/Tools/AndroidStudio/Emulator.md)

### Consideración importante

En equipos con procesadores Intel:

* Utilizar imágenes de sistema `x86_64`.
* Flutter ya no soporta imágenes `x86`.

---

## 1.10 Verificación final

### Ejecutar el simulador iOS desde Terminal

```bash
open -a Simulator
```

### Ejecutar el emulador Android desde Terminal

Listar emuladores disponibles:

```bash
emulator -list-avds
```

Ejecutar un emulador:

```bash
emulator -avd <NOMBRE_EMULADOR>
```

### Verificar dispositivos disponibles

```bash
flutter devices
```

### Crear un proyecto Flutter

```bash
flutter create my_app
```

### Ingresar al proyecto

```bash
cd my_app
```

### Ejecutar la aplicación

```bash
flutter run
```

### Resultado esperado

* `flutter doctor` no presenta errores críticos.
* El simulador iOS inicia correctamente.
* El emulador Android inicia correctamente.
* `flutter devices` detecta dispositivos disponibles.
* La aplicación Flutter se ejecuta correctamente.






## Observaciones técnicas

* Flutter utiliza compilación AOT/JIT con Dart.
* No requiere máquina virtual adicional (como JVM en Android tradicional).
* El rendimiento es cercano a nativo gracias a su motor gráfico (Skia).
