# Guía: Instalación de Android SDK

Android SDK es el conjunto oficial de herramientas proporcionadas por [Android Developers](https://developer.android.com?utm_source=chatgpt.com) para el desarrollo de aplicaciones Android. Este SDK incluye componentes esenciales como herramientas de compilación, plataformas Android, utilidades de depuración, emuladores y herramientas de línea de comandos necesarias para construir, ejecutar y probar aplicaciones en diferentes dispositivos y versiones del sistema operativo Android.

En esta guía se describe el proceso de instalación y configuración manual del Android SDK utilizando únicamente las herramientas oficiales de línea de comandos (`cmdline-tools`), sin depender de entornos de desarrollo integrados (IDE). Además, se presentan los pasos necesarios para configurar el SDK en macOS, Linux y Windows, incluyendo la instalación de componentes básicos mediante `sdkmanager`, la configuración de variables de entorno y la verificación del entorno de desarrollo.

---

# Instalación en macOS

### Requisitos de sistema

**Hardware:**

* Computadora Mac (Apple)
* Procesador: Apple Silicon (M1 o superior) **(recomendado)** o Intel x86_64 (soportado)
* Memoria RAM: mínimo 8 GB (16 GB recomendado)
* Almacenamiento disponible: al menos 20–30 GB libres

**Software:**

* macOS Sonoma (14.7.x) o superior
* Android SDK Command-line Tools

---

### Descarga de Android SDK Command-line Tools

Descargar las herramientas oficiales desde:

[Android SDK Command-line Tools](https://developer.android.com/tools)

---

### Instalación de Android SDK

1. Descargar el archivo ZIP correspondiente a macOS
2. Abrir la carpeta `Descargas`
3. Descomprimir el archivo descargado
4. Abrir Terminal
5. Crear la estructura del SDK:

```bash id="p8m3tx"
mkdir -p ~/Library/Android/SDK/cmdline-tools/latest
```

6. Mover las herramientas descargadas:

```bash id="q4v7kn"
mv ~/Downloads/cmdline-tools/* \
~/Library/Android/SDK/cmdline-tools/latest
```

Si es requerido:

```bash id="z1r5wc"
sudo mv ~/Downloads/cmdline-tools/* \
~/Library/Android/SDK/cmdline-tools/latest
```

7. Eliminar el atributo de cuarentena de macOS:

```bash id="m6x2qp"
xattr -dr com.apple.quarantine ~/Library/Android
```

Si es requerido:

```bash id="f3t9yv"
sudo xattr -dr com.apple.quarantine ~/Library/Android
```

8. Editar el archivo `.zshrc`:

```bash id="v5n1kr"
nano ~/.zshrc
```

9. Agregar las siguientes líneas:

```bash id="j7w4mc"
export ANDROID_HOME=$HOME/Library/Android/SDK
export PATH=$ANDROID_HOME/cmdline-tools/latest/bin:$PATH
export PATH=$ANDROID_HOME/platform-tools:$PATH
export PATH=$ANDROID_HOME/emulator:$PATH
```

10. Aplicar cambios:

```bash id="r2k8xn"
source ~/.zshrc
```

11. Verificar `sdkmanager`:

```bash id="c9q5tp"
sdkmanager --version
```

12. Instalar componentes básicos:

```bash id="n4v7ym"
sdkmanager "platform-tools"
sdkmanager "build-tools;36.0.0"
sdkmanager "platforms;android-36"
sdkmanager "emulator"
```

13. Aceptar licencias:

```bash id="x6m3qc"
sdkmanager --licenses
```

14. Verificar instalación:

```bash id="k1t9wr"
adb --version
```

---

# Instalación en Linux

### Requisitos de sistema

**Hardware:**

* Procesador x86_64
* Memoria RAM: mínimo 8 GB (16 GB recomendado)
* Almacenamiento disponible: al menos 20–30 GB libres

**Software:**

* Ubuntu 24.04 LTS o superior
* Terminal Bash
* `unzip`
* Android SDK Command-line Tools

---

### Descarga de Android SDK Command-line Tools

Descargar las herramientas oficiales desde:

[Android SDK Command-line Tools](https://developer.android.com/tools)

---

### Instalación de Android SDK

1. Descargar el archivo ZIP correspondiente a Linux
2. Abrir la carpeta `Descargas`
3. Descomprimir el archivo descargado
4. Abrir Terminal
5. Crear la estructura del SDK:

```bash id="w3p8tm"
mkdir -p ~/Android/SDK/cmdline-tools/latest
```

6. Mover las herramientas descargadas:

```bash id="g7m2xq"
mv ~/Downloads/cmdline-tools/* \
~/Android/SDK/cmdline-tools/latest
```

Si es requerido:

```bash id="t4v9kc"
sudo mv ~/Downloads/cmdline-tools/* \
~/Android/SDK/cmdline-tools/latest
```

7. Editar el archivo `.bashrc`:

```bash id="h6q1zn"
nano ~/.bashrc
```

8. Agregar las siguientes líneas:

```bash id="p2w5xr"
export ANDROID_HOME=$HOME/Android/SDK
export PATH=$ANDROID_HOME/cmdline-tools/latest/bin:$PATH
export PATH=$ANDROID_HOME/platform-tools:$PATH
export PATH=$ANDROID_HOME/emulator:$PATH
```

9. Aplicar cambios:

```bash id="m8t4qy"
source ~/.bashrc
```

10. Verificar `sdkmanager`:

```bash id="v1k7np"
sdkmanager --version
```

11. Instalar componentes básicos:

```bash id="r5m3xc"
sdkmanager "platform-tools"
sdkmanager "build-tools;36.0.0"
sdkmanager "platforms;android-36"
sdkmanager "emulator"
```

12. Aceptar licencias:

```bash id="q9w2tk"
sdkmanager --licenses
```

13. Verificar instalación:

```bash id="f4x8mv"
adb --version
```

---

# Instalación en Windows

### Requisitos de sistema

**Hardware:**

* Procesador x86_64
* Memoria RAM: mínimo 8 GB (16 GB recomendado)
* Almacenamiento disponible: al menos 20–30 GB libres

**Software:**

* Windows 10/11 64 bits
* PowerShell o CMD
* Android SDK Command-line Tools

---

### Descarga de Android SDK Command-line Tools

Descargar las herramientas oficiales desde:

[Android SDK Command-line Tools](https://developer.android.com/tools)

---

### Instalación de Android SDK

1. Descargar el archivo ZIP correspondiente a Windows
2. Abrir la carpeta `Descargas`
3. Descomprimir el archivo descargado
4. Crear la siguiente estructura de carpetas:

```text id="d8k4mp"
C:\Android\SDK\cmdline-tools\latest
```

5. Mover el contenido de:

```text id="y2q7wc"
C:\Users\USERNAME\Downloads\cmdline-tools
```

hacia:

```text id="u5n1xr"
C:\Android\SDK\cmdline-tools\latest
```

6. Abrir “Variables de entorno”
7. Crear la variable:

```text id="k4m8tp"
ANDROID_HOME
```

con el valor:

```text id="q1v5zn"
C:\Android\SDK
```

8. Agregar las siguientes rutas al `PATH`:

```text id="m7x2kc"
%ANDROID_HOME%\cmdline-tools\latest\bin
%ANDROID_HOME%\platform-tools
%ANDROID_HOME%\emulator
```

9. Abrir PowerShell o CMD
10. Verificar `sdkmanager`:

```powershell id="r3w9qt"
sdkmanager --version
```

11. Instalar componentes básicos:

```powershell id="f8m1xp"
sdkmanager "platform-tools"
sdkmanager "build-tools;36.0.0"
sdkmanager "platforms;android-36"
sdkmanager "emulator"
```

12. Aceptar licencias:

```powershell id="t6k4yn"
sdkmanager --licenses
```

13. Verificar instalación:

```powershell id="n2v7qc"
adb --version
```

---

# Android Emulator Archive (Opcional)

Si se requiere descargar versiones específicas del emulador Android:

[Android Emulator Archive](https://developer.android.com/studio/emulator_archive?utm_source=chatgpt.com)

Esto puede ser útil para:

* Compatibilidad con versiones anteriores
* Problemas de estabilidad
* Arquitecturas específicas
* Instalaciones manuales avanzadas

---

# Actualizar SDK

Para actualizar los componentes instalados:

```bash id="x9m3tw"
sdkmanager --update
```

---

# Notas finales

* `cmdline-tools` permite administrar completamente Android SDK desde Terminal
* No es necesario instalar un IDE para utilizar el SDK
* `sdkmanager` permite descargar plataformas, herramientas y emuladores adicionales
* Se recomienda instalar únicamente las versiones necesarias del SDK
* Mantener el SDK actualizado mejora compatibilidad y estabilidad
