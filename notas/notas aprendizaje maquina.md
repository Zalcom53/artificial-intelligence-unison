 # Aprendizaje máquina

## Plan de la presentación:
1. ¿Qué es el aprendizaje máquina?  
2. Todo es sobre generalización  
3. Ejemplo ilustrativo: Los vecinos próximos  
4. Scikit-learn: Biblioteca de aprendizaje máquina en Python  

---

## Motivación:
* Es **muy difícil escribir programas** que resuelvan problemas complejos.  
  * Ejemplos incluyen reconocer objetos en tres dimensiones desde diferentes perspectivas y condiciones de luz.  
  * No sabemos cómo nuestro cerebro procesa ese tipo de información. Un programa escrito a mano sería "terrorífico".  
  * Otro ejemplo es calcular la probabilidad de que una transacción en línea sea fraudulenta. No existen reglas simples y confiables. Se necesitarían muchas reglas, y el fraude es dinámico, requiriendo actualizaciones continuas.  

---

## La solución:
* En lugar de escribir un programa específico para cada tarea, se pueden **recolectar muchos ejemplos** con la respuesta correcta.  
* Se envían estos datos a un **algoritmo de aprendizaje máquina**.  
* El algoritmo **devuelve un programa**.  
* Este programa es muy diferente a uno hecho a mano. Si está bien hecho, debería **funcionar para casos nuevos con cierto margen de confianza**.  
* Si los datos cambian, es posible cambiar el programa producido.  
* Actualmente, **grandes cantidades de datos y capacidad masiva de cómputo** son más económicas que tener expertos en tareas específicas.  

---

## Definiciones de Aprendizaje Máquina:
* **A. Samuel (1959):**  
  "Field of study that gives computers the ability to learn without being explicitly programmed".  
  (Campo de estudio que da a las computadoras la habilidad de aprender sin ser explícitamente programadas).  
* **T. Mitchell (1998):**  
  "Well–posed Learning Problem" (Problema de aprendizaje bien planteado):  
  Un programa de computadora se dice que aprende de la experiencia *E* con respecto a alguna tarea *T* y alguna medida de rendimiento *P*, si su rendimiento en *T*, medido por *P*, mejora con la experiencia *E*.  

---

## Generalización:
* El aprendizaje máquina se trata fundamentalmente de la **generalización**.  
* **Error en muestra (Ein):**  
  Error calculado sobre los datos de entrenamiento. Se define como la suma de errores para cada dato de entrenamiento dividida por el número total de datos.  
* **Error fuera de muestra (Eout):**  
  Error calculado sobre datos nuevos, no vistos durante el entrenamiento. Se define como el valor esperado del error sobre todas las posibles entradas.  
* El **aprendizaje existe si y solo si Eout ≈ 0**.  
* Esto solo es posible si:  
  * **Ein ≈ 0**  
  * **Ein ≈ Eout**  
* (Las fuentes incluyen ejemplos simples de generalización mostrando puntos y cómo se podría trazar una función *f(x)* para representarlos).  

---

## El método del vecino más próximo (k-NN):
* Es un **ejemplo ilustrativo** de aprendizaje máquina.  
* Es un método **no paramétrico**.  
* **Requiere guardar todos los datos** del conjunto de entrenamiento.  
* Para clasificar un dato desconocido, se calcula una **medida de similaridad con TODOS los datos** del conjunto de entrenamiento.  
* Se selecciona la clase del dato **más cercano**.  
* Conceptualmente, **no hay un método más simple**.  
* (Las fuentes incluyen un ejemplo gráfico que parece distinguir entre terremotos y explosiones usando características x1 y x2, mostrando cómo se clasificaría un punto usando un vecino o cinco vecinos próximos).  

---

## La maldición de la dimensionalidad:
* Se menciona como un problema en el contexto del aprendizaje máquina.  
* (La fuente incluye un gráfico que muestra cómo la proporción de puntos en la "capa exterior" de un espacio aumenta rápidamente con el número de dimensiones, lo que implica que en altas dimensiones, la mayoría de los puntos están "lejos" de otros puntos, afectando métodos basados en distancia como el vecino más próximo).  

---

## Otros métodos de aprendizaje máquina:
* Modelos descriptivos  
* Modelos lineales generalizados  
* Árboles de decisión  
* Redes neuronales  
* Métodos de ensemble  
* La fuente señala que **"El algoritmo es lo menos importante"**.  

---

## Scikit-learn:
* Es una **biblioteca de aprendizaje máquina en Python**.  
* Ofrece **herramientas simples y eficientes** para aprendizaje máquina.  
* Es **accesible, reusable y personalizable**.  
* Tiene licencia **BSD**, lo que la hace **usable comercialmente**.  
* Está construida a partir de **numpy y matplotlib**, e interactúa muy bien con **Pandas**.  
* (Se menciona la existencia de un "acordeón" o cheat sheet para scikit-learn).  
* ¡Cuidado!  
  (Este punto no se explica más en las fuentes proporcionadas, solo aparece como un título).  

