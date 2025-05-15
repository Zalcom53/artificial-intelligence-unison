---
title: ¿Qué es la Inteligencia Artificial?
created: '2025-01-20T23:09:18.401Z'
modified: '2025-01-21T02:28:00.152Z'
---

# ¿Qué es la Inteligencia Artificial?

La **Inteligencia Artificial (IA)** se basa en el desarrollo de agentes inteligentes inspirados en el razonamiento humano.  

Un agente interactúa con el entorno según las **percepciones** disponibles y, en base a esto, toma acciones o reacciona dependiendo de su modelo.  

- **Percepciones:** Son las entradas que el agente recibe del entorno.
- **Agente racional:** Toma decisiones basadas en lógica y razonamiento.

---

# Lo que debe saber el agente del entorno

## Elementos clave:

1. **Medida de desempeño:** Cómo se evalúa el éxito del agente.  
2. **Características del entorno:** Propiedades que describen el contexto en el que opera el agente.  
3. **Actuadores:** Dispositivos que permiten al agente ejecutar acciones en el entorno.  
4. **Sensores:** Herramientas para recopilar datos del entorno.  

## Aspectos importantes para el diseño del agente:

- **Tarea:** Se debe saber qué objetivo o tarea va a realizar el agente.  
- **Opciones de acción:** ¿Qué acciones puede ejecutar el agente? *(Actuadores)*  
- **Sensores:** ¿Qué puede percibir o detectar el agente?  
- **Información procesada:** ¿Qué puede leer y actuar el agente con base en las percepciones?  

## Representación matemática:

- **X:** Conjunto de posibles estados del agente.  
- **A:** Conjunto de posibles acciones que puede realizar el agente.  
- **P:** Conjunto de percepciones que el agente recibe.  

## Ejemplos:

### 1. Dron:  
- **Estados:** Altitud, velocidad de los rotores, nivel de batería, inclinación, etc.  
- Con **X**, **A** y **P**, se puede construir un historial de estados anteriores que ayuden al dron a razonar.  

### 2. Primer agente: Aspiradora inteligente (*Vacuum Cleaner*):  
- **Estados (Pₜ):** Localización y situación actual (e.g., sucio, limpio).  
- **Acciones (A):**  
  - Limpiar.  
  - Moverse hacia la izquierda (<-).  
  - Moverse hacia la derecha (->).  
  - No hacer nada (NO).  

### Consideraciones:  
- Verificar si una acción es posible.  
- Evaluar la siguiente acción y el costo de pasar de un estado a otro.  

