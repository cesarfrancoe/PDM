# Guía básica de Jetpack Compose Multiplatform (JCM)

## 1. ¿Qué es JCM?

**Jetpack Compose Multiplatform (JCM)** es un framework de **UI declarativa** creado por **JetBrains** y basado en **Jetpack Compose de Android**.
Su objetivo es permitir que los desarrolladores creen **interfaces gráficas nativas** con un **único código fuente** que puede ejecutarse en varias plataformas:

* **Android**
* **iOS**
* **Desktop** (Windows, macOS, Linux)
* **Web** (experimental)

De esta manera, JCM ayuda a **compartir la mayor parte del código** entre plataformas y reduce el tiempo de desarrollo, manteniendo la **apariencia y comportamiento nativos** en cada sistema operativo.

---

## 2. ¿Qué es la programación declarativa?

La **programación declarativa** es un paradigma en el cual el programador **describe el resultado que quiere obtener** en lugar de indicar paso a paso cómo lograrlo (como ocurre en la programación imperativa).

En interfaces gráficas, esto significa que:

* Tú **describes cómo debe verse la pantalla** en un estado determinado.
* El framework (en este caso Compose) **se encarga de actualizar automáticamente la UI** cuando cambian los datos.

🔎 Ejemplo comparativo:

* **Imperativo:** "Dibuja un botón, posiciónalo en X, cambia el color si pasa esto..."
* **Declarativo:** "Quiero un botón azul que diga 'Enviar'. Si la variable `enabled` es falsa, desactívalo."

---

## 3. Elementos básicos para crear una interfaz con JCM

Cuando trabajas con JCM, los bloques más importantes son:

### a) **Composable functions**

* Son funciones que describen cómo debe verse una parte de la UI.
* Se anotan con `@Composable`.

```kotlin
@Composable
fun Greeting(name: String) {
    Text("Hello $name!")
}
```

### b) **Layout Composables**

* Permiten organizar elementos en pantalla.
* Ejemplos comunes:

  * `Column { ... }` → organiza elementos de arriba hacia abajo.
  * `Row { ... }` → organiza elementos de izquierda a derecha.
  * `Box { ... }` → coloca elementos superpuestos o en posiciones específicas.

```kotlin
@Composable
fun ExampleLayout() {
    Column {
        Text("Title")
        Row {
            Text("Left")
            Text("Right")
        }
    }
}
```

### c) **Material Design Components**

* JCM ofrece componentes listos con estilo **Material Design**:

  * `Button`
  * `Text`
  * `Card`
  * `Scaffold` (estructura base de una pantalla)

```kotlin
@Composable
fun ExampleButton() {
    Button(onClick = { println("Clicked!") }) {
        Text("Click me")
    }
}
```

### d) **State (estado)**

* La UI depende de variables que cambian con el tiempo.
* Se usa `remember { mutableStateOf(...) }` para que Compose sepa **redibujar la pantalla** cuando el valor cambia.

```kotlin
@Composable
fun Counter() {
    var count by remember { mutableStateOf(0) }
    Column {
        Text("Count: $count")
        Button(onClick = { count++ }) {
            Text("Increase")
        }
    }
}
```

En resumen, para crear en JCM necesitas:

1. Funciones `@Composable` para definir UI.
2. Layouts (`Row`, `Column`, `Box`) para organizar.
3. Componentes de Material Design para interacción.
4. Manejo de `State` para que la UI reaccione a cambios de datos.

