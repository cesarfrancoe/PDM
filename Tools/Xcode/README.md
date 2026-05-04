## Guía: Instalación de Xcode

Xcode es el entorno oficial de desarrollo de Apple para crear aplicaciones iOS, macOS, watchOS y tvOS. Esta guía cubre su instalación y la configuración básica de herramientas necesarias.

---

### Requisitos de sistema

**Hardware:**

* Computadora Mac (Apple)
* Procesador: Apple Silicon (M1 o superior) **(recomendado)** o Intel x86_64 (soportado)
* Memoria RAM: mínimo 8 GB (16 GB recomendado)
* Almacenamiento disponible: al menos 20–30 GB libres

**Software:**

* Sistema operativo: macOS Ventura o superior
* Conexión a internet

Referencia de compatibilidad (versiones recientes):

| macOS (versión exacta) | Versión de Xcode soportada |
| ---------------------- | -------------------------- |
| Sonoma (14.7.x)        | Xcode 16.2                 |
| Sequoia (15.6.x)       | Xcode 16.4 y Xcode 26.3    |
| Tahoe (26.4.x)         | Xcode 26.4+                |

---

### Instalación de Xcode

**Opción 1: App Store (recomendada)**

1. Abrir App Store
2. Buscar **Xcode**
3. Seleccionar Xcode
4. Clic en **Instalar**

**Opción 2: Archivo descargado (.xip)**

1. Ubicar el archivo `.xip`
2. Doble clic para descomprimir
3. Mover **Xcode.app** a **Applications**

---

### Instalación de herramientas (antes de abrir Xcode)

Para evitar configuraciones adicionales en el primer arranque:

1. Abrir Terminal
2. Instalar Command Line Tools:

   ```
   xcode-select --install
   ```
3. Seleccionar la versión activa de Xcode (si aplica):

   ```
   sudo xcode-select -s /Applications/Xcode.app
   ```
4. Descargar el runtime de iOS:

   ```
   xcodebuild -downloadPlatform iOS
   ```

Este último comando permite tener listo el simulador sin necesidad de abrir Xcode.

---

### Primera ejecución

1. Abrir Xcode desde Launchpad o Spotlight
2. Aceptar los términos de licencia
3. Verificar que no se requieran descargas adicionales

---

### Verificación

En Terminal:

```
xcodebuild -version
```

---

### Notas finales

* Instalar las herramientas y runtimes previamente reduce tiempos de espera
* Permite iniciar directamente con desarrollo o uso del simulador
* Se recomienda mantener una sola versión activa de Xcode
