# **Taller: Desarrollo de una Android App Standalone para Detección de Daltonismo**  

## **Curso:** Programación para Dispositivos Móviles  
## **Objetivo:**  
Desarrollar una **Android App Standalone (basada en Views)** que evalúe la percepción del color de una persona y determine si presenta algún tipo de **daltonismo rojo-verde, azul-amarillo o total**.  

---

## **1. Descripción del Taller**  
El daltonismo es una condición que afecta la percepción de ciertos colores. En este taller, los estudiantes deberán desarrollar una aplicación Android que:  
- Presente una serie de colores en pantalla.  
- Permita al usuario seleccionar el nombre del color percibido.  
- Analice las respuestas para detectar posibles patrones de daltonismo.  

La aplicación **no debe requerir conexión a internet ni almacenamiento persistente**.  

**📌 Nota:**  
- **El idioma base de la aplicación debe ser inglés.**  
- **Se debe agregar soporte adicional para español (es).**  

---

## **2. Funcionalidades Requeridas**  
La aplicación debe implementar las siguientes funcionalidades:  

### **Pantalla de Inicio**
- Debe contener una breve explicación de la prueba.  
- Botón para iniciar la evaluación.  
- La interfaz debe mostrarse en inglés, con opción de cambiar a español.  

### **Pantalla de Evaluación**
- Se muestra un **color de fondo** que cambia en cada pregunta.  
- Se presentan **4 opciones** de nombres de color como botones.  
- El usuario selecciona la opción que considera correcta.  
- Botón "Siguiente" para pasar a la siguiente pregunta.  
- Las respuestas se registran en **memoria temporal**.  
- Todos los textos deben tener soporte para inglés y español.  

### **Pantalla de Resultados**
- Se muestra un **puntaje de precisión (% de respuestas correctas)**.  
- Se presenta un **análisis basado en los errores cometidos**.  
- Se indica si hay patrones que sugieran un posible **tipo de daltonismo**.  
- Si hay patrones claros, se muestra un mensaje recomendando **consulta con un especialista**.  
- Botón para **reiniciar la prueba**.  

---

## **3. Categorías de Evaluación y Valores RGB**  
Cada pregunta debe mostrar un color de fondo con valores RGB específicos.  

### **Evaluación Rojo ↔ Verde (Daltonismo Rojo-Verde)**
#### **Colores mostrados y errores esperados**  

| Color (RGB) | Nombre Correcto | Opciones Incorrectas (Errores esperados) |
|------------|----------------|--------------------------------|
| (255, 0, 0) | Rojo / Red | Verde, Marrón, Amarillo |
| (200, 0, 0) | Rojo / Red | Verde, Marrón, Amarillo |
| (150, 0, 0) | Rojo / Red | Verde, Marrón, Amarillo |
| (0, 255, 0) | Verde / Green | Rojo, Marrón, Amarillo |
| (0, 200, 0) | Verde / Green | Rojo, Marrón, Amarillo |
| (0, 150, 0) | Verde / Green | Rojo, Marrón, Amarillo |
| (255, 255, 0) | Amarillo / Yellow | Verde, Marrón, Blanco |
| (200, 200, 0) | Amarillo / Yellow | Verde, Marrón, Blanco |
| (150, 150, 0) | Amarillo / Yellow | Verde, Marrón, Blanco |
| (139, 69, 19) | Marrón / Brown | Rojo, Verde, Amarillo |
| (120, 50, 10) | Marrón / Brown | Rojo, Verde, Amarillo |
| (100, 40, 5) | Marrón / Brown | Rojo, Verde, Amarillo |

### **Errores comunes:**  
- Un daltónico rojo-verde confunde **rojo con marrón** o **verde con amarillo**.  

---

### **Evaluación Azul ↔ Amarillo (Daltonismo Azul-Amarillo)**
#### **Colores mostrados y errores esperados**  

| Color (RGB) | Nombre Correcto | Opciones Incorrectas (Errores esperados) |
|------------|----------------|--------------------------------|
| (0, 0, 255) | Azul / Blue | Violeta, Verde, Negro |
| (0, 0, 200) | Azul / Blue | Violeta, Verde, Negro |
| (0, 0, 150) | Azul / Blue | Violeta, Verde, Negro |
| (255, 255, 0) | Amarillo / Yellow | Verde, Blanco, Rojo |
| (200, 200, 0) | Amarillo / Yellow | Verde, Blanco, Rojo |
| (150, 150, 0) | Amarillo / Yellow | Verde, Blanco, Rojo |
| (128, 0, 128) | Violeta / Violet | Azul, Gris, Negro |
| (100, 0, 100) | Violeta / Violet | Azul, Gris, Negro |
| (75, 0, 75) | Violeta / Violet | Azul, Gris, Negro |
| (0, 255, 255) | Cian / Cyan | Azul, Verde, Blanco |
| (0, 200, 200) | Cian / Cyan | Azul, Verde, Blanco |
| (0, 150, 150) | Cian / Cyan | Azul, Verde, Blanco |

### **Errores comunes:**  
- Un daltónico azul-amarillo confunde **azul con violeta** y **amarillo con verde**.  

---

### **Evaluación de Percepción General (Daltonismo Total)**
#### **Colores mostrados y errores esperados**  

| Color (RGB) | Nombre Correcto | Opciones Incorrectas (Errores esperados) |
|------------|----------------|--------------------------------|
| (255, 255, 255) | Blanco / White | Amarillo, Gris, Azul |
| (200, 200, 200) | Blanco / White | Amarillo, Gris, Azul |
| (150, 150, 150) | Blanco / White | Amarillo, Gris, Azul |
| (0, 0, 0) | Negro / Black | Azul, Gris, Marrón |
| (50, 50, 50) | Negro / Black | Azul, Gris, Marrón |
| (100, 100, 100) | Negro / Black | Azul, Gris, Marrón |
| (128, 128, 128) | Gris / Gray | Blanco, Azul, Negro |
| (100, 100, 100) | Gris / Gray | Blanco, Azul, Negro |
| (75, 75, 75) | Gris / Gray | Blanco, Azul, Negro |

### **Errores comunes:**  
- Una persona con **acromatopsia (daltonismo total)** ve todo en **escala de grises** y responde al azar.  

---

## **4. Criterios de Evaluación del Daltonismo**  
Después de completar todas las preguntas, la aplicación debe analizar la cantidad de errores en cada categoría.  

| **Tipo de Daltonismo** | **Patrón de Errores Identificado** |
|------------------|--------------------------------|
| **Protanomalía/Protanopía** (Déficit o ausencia de rojo) | Confunde rojo con marrón o verde con amarillo. |
| **Deuteranomalía/Deuteranopía** (Déficit o ausencia de verde) | Confunde verde con rojo o amarillo con marrón. |
| **Tritanomalía/Tritanopía** (Déficit o ausencia de azul) | Confunde azul con violeta o amarillo con blanco/gris. |
| **Acromatopsia (daltonismo total)** | No distingue colores y responde al azar. |

---

**📌 Nota:**  
Se debe implementar **soporte de idiomas** usando `res/values/strings.xml` para inglés y `res/values-es/strings.xml` para español.  
