# Guía: Instalación de Android SDK

Android SDK es el conjunto oficial de herramientas proporcionadas por [Android Developers](https://developer.android.com?utm_source=chatgpt.com) para el desarrollo de aplicaciones Android. Este SDK incluye componentes esenciales como herramientas de compilación, plataformas Android, utilidades de depuración, emuladores y herramientas de línea de comandos necesarias para construir, ejecutar y probar aplicaciones en diferentes dispositivos y versiones del sistema operativo Android.

En esta guía se describe el proceso de instalación y configuración manual del Android SDK utilizando únicamente las herramientas oficiales de línea de comandos (`cmdline-tools`), sin depender de entornos de desarrollo integrados (IDE). Además, se presentan los pasos necesarios para configurar el SDK en macOS, Linux y Windows, incluyendo la instalación de componentes básicos mediante `sdkmanager`, la configuración de variables de entorno y la verificación del entorno de desarrollo.

# Instalación en macOS

## Requisitos de sistema

### Hardware

* Computadora Mac
* Apple Silicon o Intel x86_64
* 8 GB RAM mínimo
* 20–30 GB libres

### Software

* macOS Sonoma (14.7.x) o superior
* Android SDK Command-line Tools

## Descarga de Android SDK Command-line Tools

[Android SDK Command-line Tools](https://developer.android.com/tools)

## Descomprimir archivo en Descargas

## Crear estructura del SDK

```bash id="z6q1pt"
mkdir -p ~/Library/Android/SDK/cmdline-tools/latest
```

## Mover herramientas

```bash id="x2m8kv"
mv ~/Downloads/cmdline-tools/* \
~/Library/Android/SDK/cmdline-tools/latest
```

## Eliminar quarantine

```bash id="j4r9yc"
xattr -dr com.apple.quarantine ~/Library/Android
```

## Configurar PATH

```bash id="n7v3qw"
export ANDROID_HOME=$HOME/Library/Android/SDK
```

## Instalar componentes básicos

```bash id="p5t1xm"
sdkmanager "platform-tools"
sdkmanager "build-tools;36.0.0"
sdkmanager "platforms;android-36"
sdkmanager "emulator"
```

## Verificación

```bash id="c8k2wr"
adb --version
```

# Instalación en Linux

## Requisitos de sistema

### Hardware

* Procesador x86_64
* 8 GB RAM mínimo
* 20–30 GB libres

### Software

* Ubuntu 24.04 LTS o superior
* Terminal Bash
* unzip

## Descargar Android SDK Command-line Tools

[Android SDK Command-line Tools](https://developer.android.com/tools)

## Descomprimir archivo en Descargas


## Crear estructura del SDK

```bash id="v1n7qy"
mkdir -p ~/Android/SDK/cmdline-tools/latest
```

## Mover herramientas

```bash id="m4x8kc"
mv ~/Downloads/cmdline-tools/* \
~/Android/SDK/cmdline-tools/latest
```

## Configurar PATH

Editar:

```bash id="r9p2tw"
nano ~/.bashrc
```

Agregar:

```bash id="k5v6xm"
export ANDROID_HOME=$HOME/Android/SDK
export PATH=$ANDROID_HOME/cmdline-tools/latest/bin:$PATH
export PATH=$ANDROID_HOME/platform-tools:$PATH
export PATH=$ANDROID_HOME/emulator:$PATH
```

## Aplicar cambios

```bash id="f3q1zp"
source ~/.bashrc
```

## Instalar componentes básicos

```bash id="u8w5kn"
sdkmanager "platform-tools"
sdkmanager "build-tools;36.0.0"
sdkmanager "platforms;android-36"
sdkmanager "emulator"
```

## Verificación

```bash id="t7m4rx"
adb --version
```

# Instalación en Windows

## Requisitos de sistema

### Hardware

* Procesador x86_64
* 8 GB RAM mínimo
* 20–30 GB libres

### Software

* Windows 10/11 64 bits
* PowerShell o CMD

## Descargar Android SDK Command-line Tools

[Android SDK Command-line Tools](https://developer.android.com/tools)

## Descomprimir archivo en Descargas

La carpeta inicial será similar a:

```text id="q2v9pc"
C:\Users\USERNAME\Downloads\cmdline-tools
```

## Crear estructura del SDK

Crear:

```text id="y5k1wr"
C:\Android\SDK\cmdline-tools\latest
```

## Mover herramientas

Mover el contenido de:

```text id="h8t4xn"
C:\Users\USERNAME\Downloads\cmdline-tools
```

hacia:

```text id="b1m7qz"
C:\Android\SDK\cmdline-tools\latest
```


## Configurar variables de entorno

### ANDROID_HOME

```text id="p6v3kc"
C:\Android\SDK
```

### PATH

```text id="d9x2rw"
%ANDROID_HOME%\cmdline-tools\latest\bin
%ANDROID_HOME%\platform-tools
%ANDROID_HOME%\emulator
```

## Verificar sdkmanager

```powershell id="w4n8qp"
sdkmanager --version
```

## Instalar componentes básicos

```powershell id="m7r1tx"
sdkmanager "platform-tools"
sdkmanager "build-tools;36.0.0"
sdkmanager "platforms;android-36"
sdkmanager "emulator"
```

## Verificación

```powershell id="k3v5yc"
adb --version
```

# Notas finales

* `sdkmanager` permite administrar completamente Android SDK desde Terminal.
* No es necesario instalar un IDE.
* Se recomienda instalar únicamente los componentes requeridos.
* Mantener el SDK actualizado mejora compatibilidad y estabilidad.
