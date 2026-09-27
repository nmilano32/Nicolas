# Material complementario · Glosario, análisis y cierre del curso

## Palabras clave

- **n8n**: herramienta de automatización basada en nodos, conecta apps/servicios sin código complejo.
- **API**: reglas para que dos programas se comuniquen automáticamente.
- **Workflow**: secuencia de pasos automatizados desde un disparador hasta un resultado.
- **Webhook**: forma en que una app envía info en tiempo real a otra apenas ocurre un evento (sin polling constante).
- **Nodo**: elemento básico de un workflow; representa una acción o lógica específica.
- **LLM**: IA entrenada con grandes cantidades de texto para comprender/generar lenguaje.
- **Prompt Engineering**: diseñar y refinar instrucciones para obtener el mejor resultado de una IA.
- **Agente autónomo**: IA capaz de decidir, usar herramientas y actuar de forma independiente hacia un objetivo.
- **JSON**: formato estándar para organizar/transmitir datos como pares etiqueta-valor.
- **Ollama**: herramienta para correr modelos de IA en la propia computadora, sin nube.

## La transición de flujos lineales a agentes cognitivos

Un flujo lineal ("si pasa A, hacé B") se rompe ante lo inesperado. Un agente usa un LLM como "cerebro" para razonar: analogía tren (vías fijas) vs. conductor con GPS (decide la ruta). Un agente no es un chatbot: tiene **capacidad de agencia** (usa Tools) para leer, decidir, consultar en tiempo real y actuar sin intervención humana constante.

> La clave no es que el agente sea "inteligente" por sí solo, sino que sabe cuándo y cómo usar las herramientas que se le dan en n8n.

n8n es el sistema nervioso que conecta ese cerebro (OpenAI/Ollama) con las "manos" (Sheets, WhatsApp, APIs).

## El arte de la salida estructurada: por qué el JSON es el lenguaje de la libertad en IA

El texto libre es un problema para automatizar: si se le pide extraer datos de una factura y responde en párrafo, la base de datos no lo entiende. El **JSON** es el puente entre la creatividad de la IA y la precisión de las máquinas (etiquetas claras como `"precio": 150`).

- El prompt debe definir el esquema exacto esperado (como un molde).
- Hay que **validar**: incluso las mejores IAs pueden alucinar un JSON mal formado.

## IA local vs. cloud: privacidad, costo y potencia con Ollama

| | Cloud (OpenAI/Claude) | Local (Ollama) |
|---|---|---|
| Inteligencia | Más potente | Menor en tareas complejas |
| Costo | Por token/suscripción | Cero por ejecución (solo hardware) |
| Latencia | Mayor | Menor (local) |
| Privacidad | Menor (datos salen) | Total (nunca sale de la infraestructura) |
| Conexión | Requiere internet | Funciona offline |

Los modelos locales son excelentes para tareas específicas y repetitivas (clasificar correos, resumir); la nube conviene para razonamiento abstracto de alto nivel.

## Preguntas frecuentes (resumen)

- **¿Hace falta programar?** No, n8n es low-code. Más importante es el pensamiento lógico (descomponer problemas en pasos) que la sintaxis.
- **Prompt simple vs. agente**: el prompt simple es una instrucción directa y termina ahí; el agente puede usar herramientas, investigar y actuar antes de responder.
- **¿Por qué usar Ollama si tengo OpenAI?**: privacidad de datos sensibles + ahorro de costo por token. Usar modelos locales para procesamiento interno/privado y la nube para razonamiento creativo de alto nivel.
- **¿Cómo practicar sin gastar?**: armar un sandbox con flujos simples y n8n local con Docker.
- **¿Es obligatoria la Meta Cloud API para WhatsApp?**: sí en la práctica — las alternativas no oficiales son inestables y pueden bloquear el número.
- **¿Qué hacer si un flujo falla?**: el debugging es gran parte del trabajo; revisar el inspector de datos de n8n nodo por nodo (usualmente el problema es un mapeo JSON roto). Usar nodos "Error Trigger" para que el sistema avise antes de que lo note el cliente.

## Conclusiones del curso

1. **De la automatización lineal a la orquestación cognitiva**: saber cuándo aplicar lógica rígida vs. lógica probabilística (que la IA analice y decida).
2. **Arquitectura de sistemas resilientes y escalables**: resiliencia (fail-safe ante caídas externas) y modularidad (sub-workflows, evitar "espagueti").
3. **Soberanía tecnológica**: elegir entre IA privada (Ollama) y pública (nube) según privacidad, costo y latencia.
4. **El nuevo stack del profesional autónomo**: WhatsApp Business + APIs + agentes cognitivos permiten cerrar el ciclo intención → ejecución sin depender de desarrolladores para cada integración.
