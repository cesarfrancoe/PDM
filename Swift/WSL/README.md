# Guía: Configuración de entorno para desarrollo en Swift 6 usando WSL 2 y VSCode en Windows

---

## 1. Habilitar WSL 2 en Windows

### Requisitos

* Windows 10 versión 2004 o superior, o Windows 11
* Virtualización habilitada en BIOS

### Pasos

1. Abre PowerShell como administrador y ejecuta:

   ```
   wsl --install
   ```

   Esto instalará WSL 2 y Ubuntu 22.04 por defecto.

2. Si ya tienes WSL, puedes actualizarlo con:

   ```
   wsl --update
   ```

3. Reinicia el equipo si es necesario.

---

## 2. Instalar Ubuntu 22.04

Si no se instaló automáticamente, puedes instalarlo ejecutando:

```
wsl --install -d Ubuntu-22.04
```

O desde Microsoft Store, busca "Ubuntu 22.04 LTS" y haz clic en instalar.

---

## 3. Instalar Swift 6.0 en Ubuntu (WSL)

### a. Actualizar paquetes base

Abre Ubuntu desde el menú inicio y ejecuta:

```
sudo apt update && sudo apt upgrade -y
sudo apt install -y curl git clang libicu-dev
```

### b. Descargar Swift 6.0

```
mkdir -p $HOME/swift
cd $HOME/swift
curl -O https://download.swift.org/swift-6.0-release/ubuntu2204/swift-6.0-RELEASE/swift-6.0-RELEASE-ubuntu22.04.tar.gz
tar -xzf swift-6.0-RELEASE-ubuntu22.04.tar.gz
```

### c. Agregar Swift al PATH

Edita el archivo `~/.bashrc`:

```
nano ~/.bashrc
```

Agrega al final:

```
export PATH="$HOME/swift/swift-6.0-RELEASE-ubuntu22.04/usr/bin:$PATH"
```

Guarda y aplica los cambios:

```
source ~/.bashrc
```

### d. Verificar instalación

```
swift --version
```

Deberías ver la versión 6.0 de Swift instalada correctamente.

---

## 4. Instalar Visual Studio Code y extensiones necesarias

### a. Instalar VSCode

Descarga desde [https://code.visualstudio.com](https://code.visualstudio.com)

### b. Instalar extensiones

Dentro de VSCode:

1. Abre la vista de extensiones (Ctrl + Shift + X)
2. Instala:

   * "Remote - WSL"
   * "Swift" (desarrollada por Swift Server Workgroup)

Estas extensiones permiten abrir proyectos en WSL y tener resaltado de sintaxis, autocompletado y otras herramientas para Swift.

---

## 5. Abrir tu proyecto Swift desde VSCode en WSL

Puedes hacerlo de dos formas:

### a. Desde Ubuntu (WSL)

Navega a tu carpeta de trabajo:

```
cd ~/mis-proyectos
code .
```

### b. Desde VSCode

Haz clic en el ícono verde de WSL en la esquina inferior izquierda y selecciona:

```
Remote-WSL: New Window
```

Luego abre una carpeta o proyecto Swift.

---

## 6. Crear y ejecutar lógica de negocio en Swift

### a. Usando un archivo suelto

1. Crear archivo:

   ```
   nano logic.swift
   ```

2. Escribe el siguiente ejemplo:

   ```swift
   struct Invoice {
       let items: [Double]
       func total() -> Double { items.reduce(0, +) }
   }

   let invoice = Invoice(items: [19.99, 24.50, 7.25])
   print("Total: $\(invoice.total())")
   ```

3. Ejecutar:

   ```
   swift logic.swift
   ```

### b. Usando un proyecto Swift con `swift package`

1. Crear un proyecto:

   ```
   mkdir mi-logica
   cd mi-logica
   swift package init --type executable
   ```

2. Abrir con VSCode:

   ```
   code .
   ```

3. Editar el archivo `Sources/mi-logica/main.swift` con tu lógica.

4. Compilar y ejecutar:

   ```
   swift build
   swift run
   ```

---

## 7. Ejecutar pruebas (opcional)

Agrega funciones de prueba en `Tests/mi-logicaTests` y ejecuta:

```
swift test
```

---

## Resumen

| Elemento                        | Herramienta o Acción                              |
| ------------------------------- | ------------------------------------------------- |
| Subsistema Linux                | WSL 2 con Ubuntu 22.04                            |
| Instalación de Swift            | Swift 6 desde el sitio oficial                    |
| Editor de código                | Visual Studio Code                                |
| Extensiones VSCode recomendadas | Remote - WSL, Swift (SSWG)                        |
| Métodos de ejecución            | Archivos `.swift` sueltos o proyectos con SwiftPM |
| Testing                         | Soportado vía `swift test`                        |
