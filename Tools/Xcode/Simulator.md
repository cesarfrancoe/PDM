## Guía: Creación de un simulador de iOS

El simulador de iOS es una herramienta que permite ejecutar y probar aplicaciones móviles sin necesidad de un dispositivo físico. Está integrado en Xcode y facilita el desarrollo al ofrecer distintos modelos de iPhone y versiones de iOS para validar interfaces y funcionalidades básicas.

Tanto Xcode como el iOS Simulator únicamente pueden ejecutarse en macOS.

**Nota:** Antes de continuar, asegúrese de tener Xcode correctamente instalado. La guía de instalación se encuentra disponible en:

[Guía de instalación de Xcode](https://github.com/cesarfrancoe/PDM/blob/main/Tools/Xcode/README.md)

---

### Creación del simulador

Abre Xcode y accede al gestor de dispositivos desde el menú **Window → Devices and Simulators**. Luego, selecciona la pestaña **Simulators** y presiona el botón **"+"** para crear un nuevo dispositivo virtual.

Para optimizar el consumo de recursos, se recomienda utilizar preferiblemente la siguiente configuración:

* Dispositivo: iPhone Xʀ
* Sistema operativo: iOS 18.x

Si esta configuración no se encuentra disponible o se requiere compatibilidad con versiones recientes de iOS, se recomienda utilizar:

* Dispositivo: iPhone 14
* Sistema operativo: iOS 26.x

**Nota:** iOS 26 no es compatible con iPhone Xʀ.

Si la versión de iOS no aparece disponible, debes descargarla previamente desde **Xcode → Settings → Platforms**.

Una vez creado el simulador, elimina los dispositivos virtuales que no se estén utilizando desde esta misma ventana. Esto permite optimizar el uso de almacenamiento y mantener el entorno más ligero.

---

### Ejecución (sin proyecto)

Puedes ejecutar el simulador sin necesidad de abrir o crear un proyecto de las siguientes formas:

**A) Desde Xcode**

* Menú: **Xcode → Open Developer Tool → Simulator**

**B) Desde Spotlight**

* Buscar: **Simulator**

**C) Desde la terminal**

```bash
open -a Simulator
```

**Nota:** Para facilitar el acceso, puedes anclar el simulador al Dock. Una vez abierto, haz clic derecho sobre el ícono del Simulator en el Dock y selecciona **Options → Keep in Dock**.

---

### Notas finales

El simulador es adecuado para desarrollo y pruebas iniciales. Sin embargo, no reemplaza completamente un dispositivo físico.

Para pruebas de rendimiento, es preferible utilizar un dispositivo físico, ya que permite evaluar de forma más realista el comportamiento de la aplicación y evita sobrecargar el equipo de desarrollo con la ejecución del simulador, lo que impacta tanto el rendimiento de la app como del equipo de desarrollo.
