# Repaso Módulo 1 — Preguntas y respuestas trabajadas en el chat

Resumen de la sesión de repaso del Módulo 1 (IA, LLM y Prompt Engineering), hecha después de leer el material impreso.

## 1. IA vs. LLM

Claude y ChatGPT **no son "la IA"**, son ejemplos de **LLM (Large Language Model)**. La IA es el campo amplio de la informática; el LLM surge de combinar **Deep Learning** (redes neuronales de múltiples capas) + **NLP** (Natural Language Processing, la rama que permite a las máquinas interpretar y generar lenguaje humano), entrenados con enormes cantidades de texto.

## 2. Por qué un LLM responde lo que responde

Un LLM no "entiende" como una persona: **predice matemáticamente** cuál es la palabra más probable que sigue, en base a patrones estadísticos aprendidos del texto de entrenamiento y el contexto (ej. la hora del día favorece "noches" después de "buenas").

## 3. Por qué un prompt bien estructurado gana en automatización

Un prompt sin estructura (sin rol, categorías, contexto ni formato) puede devolver resultados distintos cada vez — sirve para chatear, pero no para un flujo automatizado, porque el paso siguiente no sabe qué formato esperar. Un prompt con **rol + tarea + contexto + formato de salida** garantiza **consistencia**: siempre devuelve lo mismo, listo para usar sin "limpiarlo".

## 4. Delimitadores — la duda principal

Los **delimitadores** (`###`, `"""`, `<etiqueta>`) marcan claramente dónde empieza y termina el **dato** dentro de un prompt, para que la IA no lo confunda con una instrucción.

- No es obligatorio usar `###` puntualmente — lo importante es la consistencia dentro del mismo prompt y avisarle a la IA qué hay adentro.
- Importan **más en automatización que en un chat**: en un chat vos controlás todo lo que escribís, pero en un flujo automatizado el dato lo escribe otra persona (un cliente, un formulario). Sin delimitadores, alguien podría meter una instrucción maliciosa dentro del dato (ej. "ignorá las instrucciones anteriores...") y desviar el comportamiento de la IA — esto se llama **prompt injection**.

## Ejercicio práctico: prompt de "secretario para mails"

Se armó un ejemplo comparando:

- **Prompt sin estructura**: mezcla instrucción y mail en la misma frase, tono ambiguo, sin formato de salida → resultados inconsistentes.
- **Prompt con anatomía completa**: rol (secretario), tarea (responder el mail), contexto (tono cercano pero respetuoso, no inventar información ni confirmar datos que no están en el mail original — conectado con el riesgo de **alucinaciones** visto en el módulo), mail delimitado con `###`, y formato de salida definido (solo el cuerpo, sin asunto ni firma, 1-2 párrafos).

## Próximo paso

Arrancar con la lectura del **Módulo 2 · Introducción a las automatizaciones y n8n** y retomar la dinámica de preguntas.
