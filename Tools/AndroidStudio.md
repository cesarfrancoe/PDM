# Guía de Descarga, Instalación y Configuración de Android Studio

## 1. Descarga de Android Studio

Android Studio es el entorno de desarrollo oficial para aplicaciones Android, mantenido por Google. Incluye el SDK, emuladores y herramientas necesarias para el desarrollo y pruebas de aplicaciones móviles.



### 1.1 Requisitos mínimos del sistema

Antes de realizar la descarga, verifica que el equipo cumpla con los siguientes requisitos mínimos:

- Sistema operativo:
  - Windows 10 u 11 (64 bits)
  - macOS (64 bits)
  - Linux (64 bits)
- Memoria RAM: mínimo 8 GB (4 GB puede funcionar con limitaciones)
- Espacio en disco: al menos 8 GB libres
- Procesador con soporte de virtualización (Intel VT-x o AMD-V)
- Conexión a Internet para la descarga de componentes adicionales

> Nota: Android Studio incluye un JDK compatible, por lo que no es necesario instalar Java por separado.

### 1.2 Descarga desde el sitio oficial

1. Abre un navegador web.
2. Accede al sitio oficial de Android Studio:  
   https://developer.android.com/studio
3. Haz clic en el botón **Download Android Studio**.
4. Acepta los términos y condiciones de uso.
5. Descarga el instalador correspondiente a tu sistema operativo.

Se recomienda **no descargar Android Studio desde sitios externos**, para evitar versiones desactualizadas o modificadas.

### 1.3 Verificación del instalador descargado

Una vez finalizada la descarga:
- Verifica que el archivo corresponda a la versión estable.
- Comprueba que el tamaño del archivo sea coherente (varios cientos de MB).
- No descomprimas ni ejecutes el archivo hasta completar la descarga correctamente.

## 2. Instalación de Android Studio

En esta sección se describe el proceso de instalación de Android Studio una vez descargado el instalador oficial. El procedimiento es similar en todos los sistemas operativos, con pequeñas variaciones específicas.

### 2.1 Instalación en Windows

1. Ejecuta el archivo descargado con extensión `.exe`.
2. Cuando se inicie el asistente de instalación, haz clic en **Next**.
3. Selecciona los componentes a instalar:
   - Android Studio
   - Android SDK
   - Android Virtual Device (AVD)
4. Mantén seleccionadas todas las opciones y continúa.
5. Acepta la ruta de instalación por defecto:
   - Android Studio: `C:\Program Files\Android\Android Studio`
   - SDK: `C:\Users\usuario\AppData\Local\Android\Sdk`
6. Haz clic en **Install** y espera a que finalice el proceso.
7. Una vez completada la instalación, selecciona **Start Android Studio** y pulsa **Finish**.

### 2.2 Instalación en macOS

1. Abre el archivo `.dmg` descargado.
2. Arrastra el icono de **Android Studio** a la carpeta **Applications**.
3. Accede a **Applications** y ejecuta Android Studio.
4. Si el sistema muestra un aviso de seguridad, confirma que deseas abrir la aplicación.

### 2.3 Instalación en Linux

1. Descomprime el archivo `.zip` descargado en una ubicación de tu preferencia.
2. Accede a la carpeta descomprimida.
3. Ejecuta el archivo `studio.sh` ubicado en la carpeta `bin`:
   ```bash
   ./studio.sh

## 3. Configuración del SDK y del Emulador Android (AVD)

Una vez instalado Android Studio, es necesario verificar el SDK y configurar un emulador Android con parámetros adecuados para equipos de bajos recursos. En esta guía se estandariza el uso de un **Pixel 3 con Android 10 (API 29)**.

### 3.1 Verificación del Android SDK

1. Abre Android Studio.
2. En la pantalla inicial, selecciona **More Actions > SDK Manager**.
3. En la pestaña **SDK Platforms**, verifica que esté instalada la siguiente plataforma:
   - Android 10 (API 29)

   Si no está instalada:
   - Marca la casilla correspondiente.
   - Haz clic en **Apply** y acepta las licencias.

4. Accede a la pestaña **SDK Tools** y asegúrate de que estén instalados:
   - Android SDK Build-Tools
   - Android SDK Platform-Tools
   - Android Emulator

5. Aplica los cambios si realizaste alguna modificación.

### 3.2 Creación del dispositivo virtual (AVD)

1. Desde la pantalla principal de Android Studio, selecciona **More Actions > Virtual Device Manager**.
2. Haz clic en **Create Device**.
3. En la lista de dispositivos, selecciona:
   - Categoría: Phone
   - Modelo: Pixel 3
4. Haz clic en **Next**.

### 3.3 Selección de la imagen del sistema

1. En la lista de imágenes del sistema, selecciona:
   - Android 10
   - API Level: 29
   - Arquitectura: x86_64
2. Si la imagen no está descargada, haz clic en **Download**.
3. Una vez descargada, selecciona la imagen y pulsa **Next**.

### 3.4 Configuración avanzada del AVD

En la pantalla de configuración del dispositivo virtual, ajusta los siguientes parámetros:

- AVD Name: Pixel_3_API_29
- RAM: 1024 MB
- Internal Storage: 6 GB (mínimo permitido por el sistema)
- Graphics:
  - Hardware (recomendado)
  - Software (usar solo si no hay soporte de virtualización)
- Boot Option: Cold Boot (por defecto)

Mantén el resto de opciones con sus valores predeterminados.

Haz clic en **Finish** para crear el emulador.

### 3.5 Prueba del emulador

1. En el **Virtual Device Manager**, localiza el emulador creado.
2. Haz clic en el botón **Play**.
3. Espera a que el sistema Android inicie completamente.

El primer arranque puede tardar varios minutos. Una vez iniciado, el emulador estará listo para ejecutar aplicaciones Android.

## 4. Creación y ejecución de un proyecto Android de prueba

El objetivo de esta sección es validar que Android Studio, el SDK y el emulador han sido configurados correctamente mediante la creación y ejecución de una aplicación básica basada en **Views (XML)**.

### 4.1 Creación de un nuevo proyecto

1. Abre Android Studio.
2. En la pantalla inicial, selecciona **New Project**.
3. En la lista de plantillas, selecciona **Empty Views Activity**.
4. Haz clic en **Next**.

> Nota: Se utiliza *Empty Views Activity* para trabajar con interfaces tradicionales basadas en XML, adecuadas para cursos introductorios y para comprender la arquitectura clásica de Android.

### 4.2 Configuración del proyecto

Completa los campos con los siguientes valores recomendados:

- Name: `AppPrueba`
- Package name: `com.example.appprueba`
- Save location: ruta por defecto
- Language: **Kotlin**
- Minimum SDK: **API 21 (Android 5.0)** o superior
- Build configuration language: **Kotlin DSL** (por defecto)

Haz clic en **Finish** para crear el proyecto.

Android Studio realizará automáticamente:
- La creación de la estructura del proyecto.
- La configuración de Gradle.
- La sincronización inicial de dependencias.

Este proceso puede tardar varios minutos la primera vez.

### 4.3 Revisión de la estructura del proyecto

Una vez finalizada la sincronización, verifica que:

- No existan errores en la pestaña **Build**.
- Se haya generado el archivo `MainActivity.kt`.
- Exista el archivo de diseño `activity_main.xml` en la carpeta `res/layout`.

Esto confirma que el proyecto basado en **Views + XML** se creó correctamente.

### 4.4 Ejecución de la aplicación en el emulador

1. Inicia el emulador **Pixel 3 – API 29**.
2. En la barra superior de Android Studio, selecciona el dispositivo virtual activo.
3. Haz clic en el botón **Run (▶)**.
4. Espera a que el proyecto se compile y se instale en el emulador.

Si la ejecución es correcta:
- La aplicación se instalará sin errores.
- Se mostrará una pantalla en blanco con el texto inicial por defecto.

### 4.5 Verificación final

La ejecución exitosa del proyecto confirma que:
- Android Studio está correctamente instalado.
- El SDK y las herramientas de compilación funcionan.
- El emulador responde correctamente con la configuración definida.


