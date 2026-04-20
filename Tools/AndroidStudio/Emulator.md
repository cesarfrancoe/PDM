# Guía: Creación de un Emulador de Android optimizado en Android Studio

## 1. Introducción

Un emulador de Android permite simular un dispositivo móvil para ejecutar y probar aplicaciones sin hardware físico. La herramienta principal es Android Studio, que integra AVD dentro del Android SDK.

El objetivo de esta guía es **minimizar el consumo de recursos (CPU, RAM y disco)** manteniendo un entorno funcional.

---

## 2. Criterio de optimización

Configuración objetivo:

* Dispositivo: **Pixel 3**
* Sistema: **Android 10 (API 29)**
* Arquitectura: **x86_64 (en equipos no ARM)**

Justificación:

* Pixel 3 → carga gráfica moderada
* API 29 → menor consumo que APIs recientes
* x86_64 → virtualización por hardware en Intel/AMD

---

## 3. Requisitos previos

Hardware:

* CPU con virtualización habilitada
* 8 GB de RAM (recomendado)
* 10 GB de espacio libre

Software:

* Android Studio
* SDK configurado
* Android Emulator Hypervisor Driver

---

## 4. Instalación de componentes

`Tools > SDK Manager`

Instalar:

* **SDK Platform**: Android 10 (API 29)
* **SDK Tools**:

  * Android Emulator
  * Platform-Tools
  * Build-Tools
  * Hypervisor Driver

---

## 5. Creación del dispositivo virtual (AVD)

### Paso 1: Abrir Device Manager

`Device Manager`

---

### Paso 2: Crear Virtual Device

`Create Virtual Device`

---

### Paso 3: Seleccionar perfil de hardware

* Form Factor: **Phone**
* Dispositivo: **Pixel 3**
* Clic: `Next`

---

### Paso 4: Seleccionar imagen del sistema

Configurar:

* API: **29 (Android 10)**
* Services: **Google APIs**
* Imagen: **Google APIs Intel x86_64 Atom System Image**

Clic: `Next`

---

## 6. Configuración completa del dispositivo (CRÍTICO)

En la pantalla **Configure virtual device**:

**Antes de presionar `Finish`, se deben configurar completamente ambas pestañas:**

* **Device**
* **Additional settings**

---

### 6.1 Pestaña: Device

* Name: **Pixel 3**
* Orientation: **Portrait**
* Default Boot: **Cold**

---

### 6.2 Pestaña: Additional settings

#### Cámara

* Front: **None**
* Rear: **None**

---

#### Red

* Speed: **Full**
* Latency: **None**

---

#### Almacenamiento

* Internal Storage: **6 GB**
* Expanded Storage: **None**

---

#### Rendimiento

* CPU cores: **1**
* RAM: **1500 MB**
* VM Heap: **64 MB**

---

#### Gráficos

* Graphics Acceleration: **Automatic**

---

### Paso final

Una vez configuradas ambas pestañas:

`Finish`

---

## 7. Nota técnica sobre arquitectura (IMPORTANTE)

Se recomienda usar **x86_64** en lugar de **x86**, incluso en procesadores Intel/AMD.

Razones:

* Mejor compatibilidad con herramientas modernas
* Mayor estabilidad del emulador
* Mejor rendimiento con virtualización

**Caso específico:**

Frameworks como Flutter han eliminado soporte para imágenes **x86** en versiones recientes.

Por lo tanto:

* **x86 → no recomendado / obsoleto**
* **x86_64 → obligatorio en entornos actuales**

---

## 8. Ejecución del emulador

En Device Manager:

* Clic en **Play (▶)**

---

## 9. Validación

El AVD debe quedar con:

* Pixel 3
* API 29
* ABI: x86_64
* RAM: 1500 MB
* CPU: 1 core

---

## 10. Buenas prácticas

* No ejecutar múltiples emuladores
* Cerrar procesos pesados
* Usar APIs moderadas
* Evitar dispositivos de alta gama en emulación

---

## 11. Conclusión

La combinación:

* Pixel 3
* API 29
* x86_64
* 1500 MB RAM
* 1 CPU core

proporciona un entorno equilibrado, funcional y de bajo consumo dentro de Android Studio, adecuado para desarrollo y pruebas en equipos con recursos limitados.
