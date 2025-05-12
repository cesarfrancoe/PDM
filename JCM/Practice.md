# **Jetpack Compose Multiplatform (JCM)**

---

## **Introducción general**

### ¿Qué es Jetpack Compose Multiplatform?

**Jetpack Compose Multiplatform (JCM)** es un framework de interfaces de usuario creado por **JetBrains** (con el apoyo de **Google** para Android) que permite desarrollar apps modernas usando un solo lenguaje (**Kotlin**) y compartir el código en múltiples plataformas: Android, iOS, desktop y web.

---

### **¿Cómo funciona?**

* Se basa en **Kotlin Multiplatform**, lo que permite compartir tanto la lógica como las interfaces de usuario.
* Utiliza un enfoque **declarativo** mediante Jetpack Compose: describes cómo debe lucir la interfaz, en lugar de cómo construirla paso a paso.
* Ofrece una **integración nativa real**:

  * En Android, usa directamente Jetpack Compose sobre la JVM.
  * En iOS, se compila a código nativo mediante Kotlin/Native.

---

### **¿Qué se necesita?**

| Requisito              | Descripción                                                          |
| ---------------------- | -------------------------------------------------------------------- |
| **IDE**                | Android Studio o IntelliJ IDEA con soporte para Kotlin Multiplatform |
| **Lenguaje**           | Kotlin (con soporte multiplataforma)                                 |
| **Herramientas**       | Gradle, Kotlin/Native (iOS), Kotlin/JVM (Android)                    |
| **Simulador/Emulador** | Emulador de Android y/o simulador de iOS (requiere Xcode)            |

---

### **Comparación con otros frameworks multiplataforma**

| **Framework**                 | **Lenguaje**          | **Tipo de UI**                  | **Acceso nativo**          | **Reutilización lógica/UI** | **¿Usa UI nativa del sistema operativo?** |
| ----------------------------- | --------------------- | ------------------------------- | -------------------------- | --------------------------- | ----------------------------------------- |
| Jetpack Compose Multiplatform | Kotlin                | Declarativa (Compose)           | Total                      | Alta (incluye UI)           | Sí (100%)                                 |
| Flutter                       | Dart                  | Declarativa (Flutter UI)        | Alto (con plugins)         | Alta                        | No (UI propia de Flutter)                 |
| React Native                  | JavaScript            | Declarativa (JSX)               | Alto (a través de bridges) | Parcial                     | Parcial (usa bridges a nativos)           |
| Xamarin / .NET MAUI           | C#                    | Imperativa o declarativa (MAUI) | Alto                       | Parcial                     | Sí (usa controles nativos de .NET MAUI)   |
| Ionic                         | JavaScript/TypeScript | HTML + CSS                      | Limitado (usa WebView)     | Alta en web, baja nativa    | No (usa WebView)                          |

### 📝 **Nota**

**En esta tabla, “¿Usa UI nativa del sistema operativo?” indica si el framework convierte sus controles de interfaz en elementos nativos de la plataforma.**
Por ejemplo, **Jetpack Compose Multiplatform** transforma un botón en un control como `android.widget.Button` en Android o una vista nativa equivalente en iOS.
Esto garantiza una mejor integración visual, funcional y de accesibilidad.

En contraste, frameworks como **Flutter** dibujan sus propias interfaces sobre un lienzo gráfico, sin usar los controles nativos del sistema operativo.


