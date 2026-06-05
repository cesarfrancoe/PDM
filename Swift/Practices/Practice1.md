# Práctica: Desarrollo de una App de Catálogo de Películas en SwiftUI

## Objetivo

Desarrollar paso a paso una aplicación para iPhone utilizando Swift, SwiftUI y Xcode 16.4 que permita mostrar un catálogo de películas y consultar el detalle de cada una mediante navegación entre pantallas.

Al finalizar esta práctica, el estudiante estará en capacidad de:

* Crear proyectos iOS utilizando Xcode.
* Definir modelos de datos utilizando estructuras (`struct`).
* Trabajar con arreglos de objetos.
* Crear interfaces gráficas con SwiftUI.
* Mostrar información mediante listas.
* Implementar navegación utilizando `NavigationStack`.
* Organizar el código en múltiples archivos.

## Requisitos previos

Antes de iniciar esta práctica, el estudiante debe tener instalado:

* Xcode 16.4
* macOS compatible con Xcode 16.4
* Simulador iPhone Xʀ con iOS 18.x

Además, debe tener conocimientos básicos de:

* Variables y constantes
* Estructuras (`struct`)
* Arreglos
* SwiftUI
* Vistas (`View`)
* Componentes `Text`, `Image`, `VStack`, `HStack` y `List`

## Resultado esperado

La aplicación tendrá dos pantallas principales.

La primera mostrará una lista de películas.

```text
+--------------------------------------+
| [Imagen] Avatar                      |
|           Science Fiction - 2009     |
+--------------------------------------+

+--------------------------------------+
| [Imagen] Interstellar                |
|           Science Fiction - 2014     |
+--------------------------------------+

+--------------------------------------+
| [Imagen] The Batman                  |
|           Action - 2022              |
+--------------------------------------+
```

Al seleccionar una película se mostrará una segunda pantalla con el detalle completo.

```text
Avatar

Science Fiction - 2009

Duration: 162 min

Synopsis

A former marine travels to Pandora
and becomes involved in the conflict
between humans and the native population.
```

---

# 1. Creación del proyecto

Abrir Xcode.

Seleccionar:

```text
File > New > Project...
```

Seleccionar la plantilla:

```text
iOS > App
```

Presionar **Next**.

Configurar el proyecto utilizando los siguientes valores:

| Campo                   | Valor        |
| ----------------------- | ------------ |
| Product Name            | MovieCatalog |
| Team                    | None         |
| Organization Identifier | edu.example  |
| Interface               | SwiftUI      |
| Language                | Swift        |
| Storage                 | None         |

Presionar **Next**.

Seleccionar la carpeta donde se almacenará el proyecto.

Presionar **Create**.

Una vez creado el proyecto, observar la estructura generada automáticamente por Xcode.

---

# 2. Creación del modelo de datos

Crear un nuevo archivo Swift.

Seleccionar:

```text
File > New > File...
```

Seleccionar:

```text
Swift File
```

Asignar el nombre:

```text
Movie.swift
```

Agregar el siguiente código:

```swift
import Foundation

struct Movie: Identifiable {
    let id: Int
    let title: String
    let year: Int
    let genre: String
    let duration: Int
    let synopsis: String
    let imageName: String
}
```

### Explicación

Esta estructura representa una película.

Cada objeto almacenará:

* Identificador
* Título
* Año
* Género
* Duración
* Sinopsis
* Nombre de la imagen

La conformidad con `Identifiable` permite que SwiftUI pueda utilizar fácilmente estos objetos dentro de una lista.

---

# 3. Creación de los datos de prueba

Crear un nuevo archivo Swift llamado:

```text
MovieData.swift
```

Agregar el siguiente código:

```swift
import Foundation

let movies: [Movie] = [
    Movie(
        id: 1,
        title: "Avatar",
        year: 2009,
        genre: "Science Fiction",
        duration: 162,
        synopsis: "A former marine travels to Pandora and becomes involved in the conflict between humans and the native population.",
        imageName: "avatar"
    ),

    Movie(
        id: 2,
        title: "Interstellar",
        year: 2014,
        genre: "Science Fiction",
        duration: 169,
        synopsis: "A group of explorers travels through a wormhole in space in an attempt to ensure humanity's survival.",
        imageName: "interstellar"
    ),

    Movie(
        id: 3,
        title: "The Batman",
        year: 2022,
        genre: "Action",
        duration: 176,
        synopsis: "Batman investigates corruption in Gotham City while facing a mysterious criminal known as the Riddler.",
        imageName: "batman"
    )
]
```

### Explicación

Se ha creado un arreglo llamado `movies`.

Cada elemento del arreglo corresponde a una instancia de la estructura `Movie`.

Por ahora se utilizarán tres películas para verificar el funcionamiento de la aplicación.

---

# 4. Agregar imágenes al proyecto

Abrir:

```text
Assets.xcassets
```

Agregar tres imágenes.

Los nombres deben ser exactamente:

```text
avatar
interstellar
batman
```

### Importante

El valor almacenado en la propiedad `imageName` debe coincidir exactamente con el nombre definido en Assets.

Por ejemplo:

```swift
imageName: "avatar"
```

requiere una imagen llamada:

```text
avatar
```

---

# 5. Creación de la vista de fila

Crear un nuevo archivo:

```text
MovieRowView.swift
```

Seleccionar:

```text
SwiftUI View
```

Agregar el siguiente código:

```swift
import SwiftUI

struct MovieRowView: View {

    let movie: Movie

    var body: some View {
        HStack(spacing: 12) {

            Image(movie.imageName)
                .resizable()
                .scaledToFill()
                .frame(width: 70, height: 100)
                .clipped()
                .cornerRadius(8)

            VStack(alignment: .leading, spacing: 6) {

                Text(movie.title)
                    .font(.headline)

                Text("\(movie.genre) - \(movie.year)")
                    .font(.subheadline)
                    .foregroundStyle(.secondary)

                Text("\(movie.duration) min")
                    .font(.caption)
                    .foregroundStyle(.secondary)
            }
        }
        .padding(.vertical, 6)
    }
}

#Preview {
    MovieRowView(movie: movies[0])
}
```

### Explicación

Esta vista será utilizada para representar una película dentro de la lista.

La fila contiene:

* Imagen
* Título
* Género
* Año
* Duración

---

# 6. Creación de la pantalla de detalle

Crear un nuevo archivo:

```text
MovieDetailView.swift
```

Agregar el siguiente código:

```swift
import SwiftUI

struct MovieDetailView: View {

    let movie: Movie

    var body: some View {

        ScrollView {

            VStack(alignment: .leading, spacing: 16) {

                Image(movie.imageName)
                    .resizable()
                    .scaledToFit()
                    .cornerRadius(12)

                Text(movie.title)
                    .font(.largeTitle)
                    .bold()

                Text("\(movie.genre) - \(movie.year)")
                    .font(.title3)
                    .foregroundStyle(.secondary)

                Text("Duration: \(movie.duration) min")

                Text("Synopsis")
                    .font(.title2)
                    .bold()

                Text(movie.synopsis)
            }
            .padding()
        }
        .navigationTitle(movie.title)
        .navigationBarTitleDisplayMode(.inline)
    }
}

#Preview {
    NavigationStack {
        MovieDetailView(movie: movies[0])
    }
}
```

### Explicación

Esta pantalla recibe una película seleccionada y muestra toda su información.

Se utiliza un `ScrollView` para permitir el desplazamiento vertical cuando el contenido exceda el tamaño de la pantalla.

---

# 7. Implementación de la pantalla principal

Abrir:

```text
ContentView.swift
```

Reemplazar todo el contenido por:

```swift
import SwiftUI

struct ContentView: View {

    var body: some View {

        NavigationStack {

            List(movies) { movie in

                NavigationLink {

                    MovieDetailView(movie: movie)

                } label: {

                    MovieRowView(movie: movie)
                }
            }
            .navigationTitle("Movies")
        }
    }
}

#Preview {
    ContentView()
}
```

### Explicación

Esta es la pantalla principal de la aplicación.

Se utiliza:

* `NavigationStack` para gestionar la navegación.
* `List` para mostrar todas las películas.
* `NavigationLink` para abrir la pantalla de detalle.

---

# 8. Ejecutar la aplicación

Verificar que el simulador seleccionado sea:

```text
iPhone Xʀ (iOS 18.x)
```

Si el simulador no existe, debe crearse previamente utilizando la aplicación Simulator incluida con Xcode.

Para ejecutar la aplicación:

1. Seleccionar el simulador iPhone Xʀ.
2. Presionar el botón Run.
3. Esperar a que el simulador inicie.
4. Esperar a que la aplicación sea instalada automáticamente.

La aplicación debe mostrar una lista de películas.

Al seleccionar una película, debe abrirse la pantalla de detalle correspondiente.

---

# 9. Pruebas de funcionamiento

Verificar que:

* La lista de películas se visualice correctamente.
* Las imágenes aparezcan correctamente.
* El título de cada película sea visible.
* La navegación funcione correctamente.
* La pantalla de detalle muestre toda la información.
* El desplazamiento vertical funcione correctamente.
