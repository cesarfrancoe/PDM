# Guía paso a paso: Construcción de una App en Flutter

## Introducción

Flutter es un framework de desarrollo de interfaces de usuario creado por Google que permite construir aplicaciones **multiplataforma** (Android, iOS, web y escritorio) a partir de un único código fuente, utilizando el lenguaje Dart.

A diferencia de los enfoques tradicionales de desarrollo móvil, Flutter utiliza un modelo **declarativo**, donde la interfaz se describe como una función del estado de la aplicación. Esto implica que, en lugar de modificar elementos visuales de forma imperativa, se reconstruye la interfaz cada vez que el estado cambia.

### Características principales

* **Multiplataforma real:** un solo código base para múltiples sistemas operativos
* **Alto rendimiento:** compilación nativa (AOT) y motor gráfico propio (Skia)
* **Hot Reload:** permite ver cambios en tiempo real sin reiniciar la aplicación
* **Arquitectura basada en widgets:** todos los elementos de la UI son widgets reutilizables
* **Modelo declarativo:** la UI se construye a partir del estado

### Modelo de desarrollo en Flutter

El principio fundamental es:

> “Dado un estado, la interfaz se reconstruye automáticamente”

Esto se traduce en el siguiente flujo:

1. El usuario interactúa con la aplicación
2. Se modifica el estado
3. Flutter reconstruye los widgets afectados
4. La UI se actualiza automáticamente

---

## Archivo de trabajo

Archivo principal: `lib/main.dart`
Todos los cambios se realizan sobre este archivo.

---

## Paso 1: Definir la estructura base

**Qué se hace:**
Se define el punto de entrada de la aplicación y el widget raíz.

**Para qué sirve:**
Establece el inicio del ciclo de vida de la app y el contenedor principal sobre el cual se construirá toda la interfaz.

**Cómo hacerlo:**
Reemplazar todo el contenido de `main.dart` por:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return const MaterialApp(
      home: HomeScreen(),
    );
  }
}
```

---

## Paso 2: Crear la pantalla principal

**Qué se hace:**
Se define la primera pantalla visible de la aplicación.

**Para qué sirve:**
Permite visualizar contenido inicial y validar que la aplicación renderiza correctamente.

**Cómo hacerlo:**
Agregar al final del archivo:

```dart
class HomeScreen extends StatelessWidget {
  const HomeScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return const Scaffold(
      body: Center(
        child: Text('Hola Flutter'),
      ),
    );
  }
}
```

---

## Paso 3: Agregar estructura visual (Scaffold + AppBar)

**Qué se hace:**
Se introduce una estructura visual estándar con barra superior.

**Para qué sirve:**
`Scaffold` proporciona una base consistente de UI (barra, cuerpo, botones flotantes).
`AppBar` mejora la navegación y contexto de la pantalla.

**Cómo hacerlo:**
Reemplazar el `Scaffold` actual por:

```dart
return Scaffold(
  appBar: AppBar(
    title: const Text('Mi Primera App'),
  ),
  body: const Center(
    child: Text('Hola Flutter'),
  ),
);
```

---

## Paso 4: Introducir layout (Column)

**Qué se hace:**
Se reemplaza un widget simple por una estructura de múltiples elementos.

**Para qué sirve:**
Permite organizar componentes verticalmente, base de cualquier UI real.

**Cómo hacerlo:**
Reemplazar `body` por:

```dart
body: Column(
  mainAxisAlignment: MainAxisAlignment.center,
  children: const [
    Text('Bienvenido'),
    Text('Aplicación en Flutter'),
  ],
),
```

---

## Paso 5: Introducir estado (StatefulWidget)

**Qué se hace:**
Se convierte la pantalla en un componente con estado mutable.

**Para qué sirve:**
Permite que la interfaz cambie dinámicamente en respuesta a eventos.

**Cómo hacerlo:**

Reemplazar `HomeScreen` por:

```dart
class HomeScreen extends StatefulWidget {
  const HomeScreen({super.key});

  @override
  State<HomeScreen> createState() => _HomeScreenState();
}
```

Agregar debajo:

```dart
class _HomeScreenState extends State<HomeScreen> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Mi Primera App'),
      ),
      body: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: const [
          Text('Bienvenido'),
          Text('Aplicación en Flutter'),
        ],
      ),
    );
  }
}
```

---

## Paso 6: Definir estado y lógica

**Qué se hace:**
Se introduce una variable de estado y una función que la modifica.

**Para qué sirve:**
Modela datos que cambian durante la ejecución.

**Cómo hacerlo:**

```dart
int counter = 0;

void increment() {
  setState(() {
    counter++;
  });
}
```

---

## Paso 7: Vincular estado con UI

**Qué se hace:**
Se muestra el estado en pantalla.

**Para qué sirve:**
Conecta datos con representación visual.

**Cómo hacerlo:**

```dart
body: Column(
  mainAxisAlignment: MainAxisAlignment.center,
  children: [
    const Text('Contador:'),
    Text('$counter', style: const TextStyle(fontSize: 24)),
  ],
),
```

---

## Paso 8: Agregar interacción

**Qué se hace:**
Se agrega un botón que modifica el estado.

**Para qué sirve:**
Completa el ciclo interacción → estado → UI.

**Cómo hacerlo:**

```dart
floatingActionButton: FloatingActionButton(
  onPressed: increment,
  child: const Icon(Icons.add),
),
```

---

## Paso 9: Ajustar layout

**Qué se hace:**
Se mejora la alineación visual.

**Para qué sirve:**
Garantiza consistencia en la presentación.

**Cómo hacerlo:**

```dart
body: Center(
  child: Column(
    mainAxisAlignment: MainAxisAlignment.center,
    children: [
      const Text('Contador:'),
      Text('$counter', style: const TextStyle(fontSize: 24)),
    ],
  ),
),
```

---

## Paso 10: Separar componentes

**Qué se hace:**
Se extrae un widget reutilizable.

**Para qué sirve:**
Mejora organización y mantenibilidad.

**Cómo hacerlo:**

```dart
class CounterText extends StatelessWidget {
  final int value;

  const CounterText({super.key, required this.value});

  @override
  Widget build(BuildContext context) {
    return Text(
      '$value',
      style: const TextStyle(fontSize: 24),
    );
  }
}
```

Uso:

```dart
CounterText(value: counter),
```
