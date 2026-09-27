# Módulo 6 · Implementación del AI Agent

## ¿Qué es un AI Agent? Diferencias con un nodo de IA simple

Un **AI Agent** es un sistema autónomo que recibe información, toma decisiones racionales y actúa en un entorno para cumplir un objetivo. En n8n, conecta un modelo de lenguaje (Chat Model) y una o más herramientas (Tools), y decide en tiempo de ejecución qué herramienta usar y en qué orden.

A diferencia de un flujo tradicional (nosotros definimos paso a paso), acá el LLM "razona" sobre la petición, decide si usar una herramienta, la ejecuta, analiza el resultado y repite hasta llegar a una respuesta final. Ese ciclo de razonar-actuar es lo que le da autonomía.

### Basic LLM Chain

Secuencia fija: se arma un prompt, se envía al modelo, se recibe texto. Siempre el mismo camino sin importar la entrada.

> Si la tarea es simple y predecible → **Basic LLM Chain**. Si requiere decidir, usar herramientas o mantener conversación con contexto → **AI Agent**.

### Chat Model
El "cerebro" del agente: LLM que interpreta el mensaje, razona y redacta respuestas. Sin él, el AI Agent no funciona. Se configura: credencial/API Key, modelo específico, parámetros de generación (temperatura, máx. tokens).

### Memoria
Permite recordar mensajes anteriores en la misma conversación. Sin memoria, cada mensaje se procesa aislado.

- Es **por sesión** (session ID), no persiste entre sesiones sin almacenamiento externo.
- Tipos: memoria RAM simple (pruebas) o respaldada por bases de datos externas (persistencia robusta).
- Se puede limitar cuántos mensajes anteriores se conservan, para no saturar tokens.

### Tools
Le dan al agente capacidad de actuar: consultar info externa, ejecutar acciones, acceder a datos que el LLM no conoce por sí mismo. El agente analiza nombre/descripción/parámetros de cada tool y decide si, cuál y cómo usarla (**tool calling**): el modelo indica la intención, n8n ejecuta el nodo y devuelve el resultado.

Tipos comunes: HTTP Request Tool, Workflow Tool (ejecuta otro flujo como herramienta), Code Tool (JS/Python), nodos nativos como Tool (Gmail, Sheets, Slack, BD), Calculator (para cálculos precisos).

Buenas prácticas: nombre y descripción claros por tool, no conectar más tools de las necesarias, definir bien parámetros de entrada, usar el system prompt para orientar cuándo usar cada una.

## El system prompt del agente: instrucciones y límites

El **System Prompt** son las instrucciones que recibe el agente antes de cualquier mensaje del usuario. Es fijo durante toda la ejecución y tiene **mayor prioridad** que lo que pida el usuario si entran en conflicto.

Qué suele incluir:
- **Rol/identidad**: quién es y para qué existe.
- **Tono y estilo**: formal/cercano, idioma, emojis o no.
- **Alcance y límites**: qué temas trata y cuáles evita o deriva a un humano.
- **Instrucciones sobre tools**: cuándo y cómo usar cada una.
- **Formato de salida**: texto plano, JSON, estructura específica.
- **Reglas de seguridad**: qué no revelar, cómo manejar pedidos fuera de política.

Ejemplo:
> "Sos un asistente virtual de la tienda 'Fulanito Shop'. Respondé siempre en español y de forma amable. Tu tarea es ayudar a los clientes a consultar el estado de sus pedidos usando la herramienta 'Consultar Pedido'. Si no encontrás el pedido, pedile amablemente el número de orden. No inventes información sobre stock ni precios: siempre consultá la herramienta correspondiente."

Se configura en el campo "System Message" del nodo AI Agent, admite expresiones dinámicas (llaves dobles) para insertar datos de nodos anteriores (nombre del usuario, fecha, datos de una BD).

**Resumen**: el AI Agent es el orquestador; el Chat Model razona; la Memoria da contexto conversacional; las Tools dan capacidad de actuar; el System Prompt fija el reglamento interno.

---

## 📌 Preentrega 3: Planificá y construí tu primer AI Agent

**Consigna**:

1. Planificar antes de construir: entrada (qué dispara y qué trae), proceso (qué decide/hace el agente), salida (resultado y dónde queda).
2. Justificar AI Agent vs. Basic LLM Chain (2-3 líneas).
3. Conectar al menos un servicio de Google (Sheets, Gmail, Calendar, Drive) como parte del flujo.
4. Escribir el system prompt (rol, límites, comportamiento ante ambigüedad, formato de salida).
5. Reflexión (3-4 líneas): ¿qué pasa si el agente interpreta mal una instrucción y actúa sobre un dato real? ¿Qué límite/chequeo agregar?

**Entrega**: un único PDF con planificación + system prompt, captura del workflow, captura de ejecución de prueba, y reflexión. Aprobación: 70/100 pts.
