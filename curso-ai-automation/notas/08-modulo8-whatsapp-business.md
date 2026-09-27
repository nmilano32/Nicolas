# Módulo 8 · WhatsApp Business

## Cómo funciona la WhatsApp Business Platform (Cloud API)

Tres cosas que se confunden bajo el mismo nombre:

- **WhatsApp (app normal)**: mensajería personal, sin API.
- **WhatsApp Business (app)**: versión para pequeños negocios (catálogo, respuestas automáticas básicas), sigue siendo manual, sin forma oficial de conectarla a n8n.
- **WhatsApp Business Platform** (antes "WhatsApp Business API"): solución de Meta para enviar/recibir mensajes de forma programática vía API. **Esta es la que se conecta con n8n.**

### Jerarquía de cuentas de Meta

1. **Meta Business Account (Business Manager)**: agrupa activos de la empresa (Facebook, Instagram, WhatsApp).
2. **WhatsApp Business Account**: cuenta específica de WhatsApp dentro del Business Manager, asociada a uno o más números.
3. **App de Meta for Developers**: donde se generan las credenciales técnicas (tokens, IDs) que usa n8n.
4. **Número de teléfono verificado**: habilitado para enviar/recibir vía API (deja de poder usarse en la app normal).

Esta jerarquía explica por qué conectar WhatsApp no es tan directo como un webhook de formulario (hay configuración y aprobación de Meta de por medio).

### Casos de uso típicos en n8n
- Atención al cliente automatizada (clasificar consultas y responder o derivar).
- Notificaciones transaccionales (confirmaciones, recordatorios, avisos de envío con plantillas aprobadas).
- Captura de leads (mensaje entrante → contacto nuevo en CRM).
- Chatbots conversacionales (WhatsApp + AI Agent con memoria de contexto).
- Encuestas/confirmaciones (pausar el flujo hasta que el usuario responda).

## WhatsApp Business + AI Agent + Prompt Engineering

### El agente como motor de decisión
- **Autonomía y enrutamiento**: decide la acción basándose en el razonamiento del LLM.
- **Tool calling**: pregunta general → responde directo; pedido de consultar pedido/stock/agendar → invoca herramientas antes de responder.
- **Tolerancia a la ambigüedad**: infiere intención real aunque el mensaje tenga errores de tipeo o sea un audio transcripto.

### Reglas de prompt para mensajería
- **Rol y restricciones**: quién es, a qué negocio representa, qué tiene prohibido.
- **Formato y concisión**: párrafos cortos (máx. 2-3 líneas), evitar bloques densos.
- **Estilo visual**: formato nativo de WhatsApp (asteriscos para negritas, guiones para listas, emojis estratégicos).
- **Micro-cierres (CTA)**: terminar con una pregunta clara o el siguiente paso.

### Memoria: Session ID
> **Regla de oro**: para que el agente no mezcle chats de distintos clientes, el identificador de sesión (Session ID) en el nodo de memoria debe ser siempre el número de teléfono del remitente (`wa_id` o `from` del webhook de WhatsApp).

### Arquitectura del flujo (3 fases)
1. **Trigger**: escucha eventos entrantes de la API de WhatsApp (extrae `text.body`).
2. **Procesamiento**: nodo AI Agent con LLM + Memoria (aislada por teléfono) + Tools.
3. **Respuesta**: nodo nativo de WhatsApp Business que envía el texto final al usuario.

---

## 📌 Preentrega 4: Ensamblaje del asistente de WhatsApp e IA

**Consigna**:

1. Definir el caso de uso (atención al cliente, turnos, FAQ, calificación de leads, etc.) y qué mensajes va a recibir.
2. Decidir modelo local vs. nube, justificado (datos sensibles, volumen/costo, dependencia de proveedor). Si es local, indicar qué modelo de Ollama y por qué.
3. Planificar la conexión con WhatsApp Business (diagrama: entrada → AI Agent con memoria → respuesta).
4. Escribir el system prompt (rol, tono breve/informal propio de WhatsApp, qué hacer si no puede resolver algo, límites).
5. Reflexión (3-4 líneas): si el volumen se multiplica x10, ¿la decisión del punto 2 se sostiene? ¿Qué cambiaría?

**Entrega**: PDF con las consignas desarrolladas, diagrama, system prompt y capturas del prototipo (webhook simulando WhatsApp si no hay integración real). Aprobación: 70/100 pts.
