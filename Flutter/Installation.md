## 1. Requisitos previos

Antes de instalar Flutter, valida lo siguiente:

### Sistema operativo soportado

* Windows 10/11 (64 bits)
* macOS (para desarrollo iOS)
* Linux (Ubuntu recomendado)

### Espacio y herramientas

* Al menos 2.5 GB de espacio libre
* Git instalado (verifica con: `git --version`)

---

## 2. Instalación del SDK de Flutter

### Paso 1: Descargar Flutter

* Ir al sitio oficial: [https://docs.flutter.dev](https://docs.flutter.dev)
* Descargar el SDK según tu sistema operativo

### Paso 2: Descomprimir

* Extraer en una ruta sin espacios ni caracteres especiales
  Ejemplo recomendado:

  * Windows: `C:\src\flutter`
  * macOS/Linux: `~/development/flutter`

### Paso 3: Configurar variables de entorno

Agregar Flutter al PATH:

**Windows:**

* Editar variables de entorno
* Agregar: `C:\src\flutter\bin`

**macOS/Linux:**
Editar el archivo `~/.zshrc` o `~/.bashrc`:

```bash
export PATH="$PATH:$HOME/development/flutter/bin"
```

Luego ejecutar:

```bash
source ~/.zshrc
```

---

## 3. Verificación de instalación

Ejecutar en terminal:

```bash
flutter doctor
```

Este comando diagnostica el entorno y muestra dependencias faltantes.

---

## 4. Instalación de Android Studio

Instalar Android Studio:

### Durante la instalación:

* Seleccionar:

  * Android SDK
  * Android SDK Platform
  * Android Virtual Device (AVD)

### Configurar:

Abrir Android Studio → More Actions → SDK Manager:

* Instalar:

  * Android SDK (última versión estable)
  * Android SDK Command-line Tools

---

## 5. Configuración de emulador

En Android Studio:

* Ir a **Device Manager**
* Crear un dispositivo virtual:

  * Modelo recomendado: Pixel 3 o superior
  * API recomendada: 29 o superior

---

## 6. Aceptar licencias

Ejecutar:

```bash
flutter doctor --android-licenses
```

Aceptar todas las licencias.

---

## 7. Instalación de plugins (IDE)

Si usas Android Studio o VS Code:

### Android Studio:

* Instalar plugins:

  * Flutter
  * Dart

### VS Code (opcional):

* Extensiones:

  * Flutter
  * Dart

---

## 8. Verificación final

Ejecutar nuevamente:

```bash
flutter doctor
```

El resultado esperado:

* Sin errores críticos
* Todo en estado `[✓]` o advertencias menores

---

## 9. Prueba inicial

Crear y ejecutar una app de prueba:

```bash
flutter create hello_flutter
cd hello_flutter
flutter run
```

Esto debería lanzar la aplicación en el emulador o dispositivo físico.

---

## 10. (Opcional) Configuración para iOS

Solo en macOS:

* Instalar Xcode desde App Store
* Ejecutar:

```bash
sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer
sudo xcodebuild -runFirstLaunch
```

* Instalar simuladores desde Xcode

---

## Observaciones técnicas

* Flutter utiliza compilación AOT/JIT con Dart.
* No requiere máquina virtual adicional (como JVM en Android tradicional).
* El rendimiento es cercano a nativo gracias a su motor gráfico (Skia).
