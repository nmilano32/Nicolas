# Módulo 7 · Instalando IA local con Ollama

## Por qué ejecutar un modelo local: costo, privacidad e independencia

Alternativa a la API en la nube (OpenAI, Anthropic, Google): correr el modelo en la propia máquina/servidor con **Ollama**.

### Costo
Las APIs cloud cobran por token; escala linealmente con el uso. Un modelo local no tiene costo por request (una vez descargado, las inferencias son gratis; el único costo es el hardware). Ideal para prototipado/testing sin gastar en tokens.

### Privacidad
Los datos nunca salen de la infraestructura propia — crítico con historias clínicas, contratos, datos de clientes, código propietario. Permite cumplir regulaciones sin depender de términos de servicio de terceros. Natural para entornos sin internet o con políticas estrictas.

### Independencia
No depende de disponibilidad de un proveedor externo (caídas, cambios de precio, deprecación de modelos, límites de rate). Permite operar sin conexión a internet.

> **Contrapartida**: en hardware de consumo, los modelos locales suelen ser más chicos y rendir por debajo de los modelos de punta en la nube (GPT-4o, Claude, Gemini) en razonamiento complejo. Es un trade-off entre costo/privacidad y capacidad bruta.

## Ollama y descarga de modelos

**Ollama** es el motor que descarga, guarda y ejecuta modelos de IA en la propia computadora, sin depender de internet ni de una empresa externa. Analogía: el modelo es la canción, Ollama es el reproductor.

Un **modelo** es un archivo pesado (varios GB) con todo lo aprendido en el entrenamiento. Se mide en **parámetros** (más grande = más capaz, pero más pesado) y tiene una especialidad (generalista, código, conversación, etc.).

### Elegir el modelo según hardware

| Tamaño del modelo | RAM/VRAM necesaria | Hardware típico | Ejemplos |
|---|---|---|---|
| ~1-3B parámetros | 4-8 GB | Laptop sin GPU dedicada, Raspberry Pi de gama alta | Qwen2.5 1.5B/3B, Phi-3 mini, Gemma2 2B |
| ~7-8B parámetros | 8-16 GB | Laptop 16GB RAM, GPU consumo 8GB VRAM | Llama 3.1/3.2 8B, Mistral 7B, Qwen2.5 7B |
| ~13-14B parámetros | 16-24 GB | Desktop con GPU media (RTX 4070/4080) | Qwen2.5 14B |
| ~32-34B parámetros | 24-40 GB | GPU gama alta o varias GPUs | Qwen2.5 32B, Mixtral |
| 70B+ parámetros | 48GB+ (o multi-GPU) | Servidor con GPU datacenter (A100, H100) | Llama 3.3 70B |

Detalles clave:
1. Ollama = motor local, no un modelo en sí mismo.
2. Los modelos se descargan por separado.
3. Modelo más grande = mejores respuestas, pero más memoria/potencia necesaria.
4. Ollama queda "escuchando" para que apps como n8n le pidan respuestas.
5. No hace falta internet una vez descargado el modelo.
