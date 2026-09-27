# Módulo 1 · Introducción a la IA, el Prompt Engineering y las automatizaciones

## ¿Qué es la Inteligencia Artificial?

La Inteligencia Artificial es una rama de la informática, como lo son la ciberseguridad, la ciencia de datos o la ingeniería de software. Busca desarrollar sistemas capaces de realizar tareas que necesiten de inteligencia humana.

Subcampos:

- **Machine Learning (Aprendizaje Automático)**: las máquinas aprenden en base a ejemplos, identificando patrones sin que se les diga qué hacer. Cuantos más datos reciben, mejores resultados.
- **Deep Learning (Aprendizaje Profundo)**: subcampo del ML, usa redes neuronales con múltiples capas para problemas complejos.
- **NLP (Natural Language Processing)**: permite a las computadoras leer, interpretar, comprender y generar lenguaje humano.
- **Visión Artificial (Computer Vision)**: se enfoca en entender imágenes y videos.

Combinando Deep Learning + NLP, entrenados con prácticamente todo el texto de internet, se obtiene un **Large Language Model (LLM)**. ChatGPT y Claude son LLM.

### ¿Qué es un LLM?

Sistema diseñado para comprender, procesar y generar lenguaje humano, basado en una red neuronal entrenada con enormes cantidades de texto. Identifica patrones: qué palabras suelen seguir a otras, cómo estructurar frases.

Toda respuesta de un LLM es básicamente probabilidad de palabras seguidas (ej: después de "Hola, buenas" a las 21:00, lo más probable es "noches").

El LLM no "entiende" como un humano: hace un mapeo matemático complejo aprendido del Deep Learning para simular comportamiento humano, calculando qué palabra debería ir después de otra.

## Cómo procesa el texto un LLM: tokenizador, tokens y ventana de contexto

**Inferencia**: fase de ejecución donde la red neuronal ya entrenada predice y genera el siguiente fragmento de texto basándose en el contexto recibido.

### Tokens

Los LLM no usan palabras completas, usan **tokens** (pueden ser una palabra, una sílaba o una letra). El **tokenizador** es el algoritmo de compresión/segmentación de texto; el más común es **BPE (Byte-Pair Encoding)**.

> Cada modelo usa tokenizaciones distintas, por eso no todos los modelos son buenos para todo.

### Ventana de contexto

Límite fijo de tokens que un LLM puede procesar a la vez. No es que "olvide de a poco": lo que queda afuera de la ventana simplemente deja de estar disponible. Es como una hoja de papel de tamaño fijo.

### Alucinaciones

Si el modelo perdió información clave (por la ventana de contexto o porque no se le brindó), en vez de decir "no sé", puede inventar una respuesta plausible con total confianza, aunque esté equivocada. Eso es una **alucinación**: información falsa o inventada presentada como verdad absoluta.

## Prompt Engineering: anatomía de un prompt efectivo

El **Prompt Engineering** es la práctica de diseñar de forma meticulosa las instrucciones/preguntas para un modelo, con el fin de obtener respuestas precisas y alineadas con lo pedido. Un prompt es el puente de comunicación entre nosotros y la IA.

No es solo hacer una pregunta: es dar contexto/narrativa y ser específico.

### Anatomía de un prompt efectivo (4 componentes)

1. **Rol**: quién queremos que sea la IA al responder.
2. **Tarea**: qué tiene que hacer, con verbo concreto, sin ambigüedad.
3. **Contexto**: información que necesita y no puede adivinar.
4. **Formato de salida**: cómo queremos la respuesta (clave si va a viajar dentro de una automatización).

No siempre son obligatorios los 4, pero cuando el resultado es genérico o inconsistente, casi siempre falta alguno.

### Delimitadores

Cuando en un mismo prompt conviven instrucciones y el dato a procesar, la IA puede confundir uno con otro. Los **delimitadores** (`###`, `"""`, `<etiquetas>`) separan claramente las dos partes. Importa la consistencia, no cuál se elige.

> En una automatización esto pesa más que en un chat: el texto que entra al prompt lo escribió otra persona. Delimitarlo evita que un mensaje tipo "ignorá lo anterior y hacé otra cosa" desvíe el flujo.

### Ejemplo: prompt malo vs. bueno

**Malo**: `Clasificá este mensaje: Hola, compré un buzo la semana pasada y todavía no me llegó.`
Sin rol, sin categorías definidas, sin contexto, sin formato → resultado impredecible.

**Bueno**:
```
Sos un asistente de atención al cliente de una tienda de indumentaria online.

Clasificá el mensaje del cliente que está entre los delimitadores en una de estas
tres categorías: consulta_talle, reclamo_envio, otro.

Contexto: los envíos demoran 5 días hábiles. Un pedido no se considera reclamo
hasta pasados esos 5 días.

Mensaje del cliente:
###
Hola, compré un buzo la semana pasada y todavía no me llegó.
###

Devolvé únicamente la categoría, en minúscula, sin explicación ni texto adicional.
```
Este prompt devuelve siempre el mismo formato, listo para automatizar.

### Dos técnicas de prompting

- **Zero-Shot Prompting**: pedirle a la IA que haga una tarea sin ningún ejemplo previo. Sirve para tareas genéricas; el resultado puede ser impredecible.
- **Few-Shot Prompting**: se le dan 2-3 ejemplos ("shots") dentro del mismo prompt para que copie el tono/estructura, sin redactar reglas gramaticales explícitas.

## Repaso de conceptos del módulo

1. **IA vs IA generativa**: la IA es el campo amplio; la IA generativa es la rama que crea contenido nuevo (texto, imágenes, código) a partir de instrucciones.
2. **Prompt Engineering**: no es solo "saber preguntar", es diseñar, probar, refinar y optimizar instrucciones de forma técnica e iterativa.
3. **LLM**: modelo entrenado con enormes cantidades de texto para predecir y generar lenguaje natural.
4. **Zero-shot vs few-shot**: sin ejemplos vs. con ejemplos de formato/estilo en el prompt.
5. **Automatización ≠ IA**: la automatización puede ser con reglas fijas; la automatización con IA interpreta información no estructurada y toma decisiones dinámicas.
