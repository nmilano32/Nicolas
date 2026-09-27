# Módulo 9 · Proyecto Final: despliegue de agente autónomo cognitivo

Objetivo: integrar todos los componentes del curso en un agente autónomo funcional desplegado.

## 🏁 Entrega Final: asistente autónomo de WhatsApp desplegado

Escenario: una empresa (real, ficticia o propia) necesita automatizar un proceso que consume tiempo humano, con datos de más de una fuente, que se beneficia de un agente de IA con criterio propio.

### Requisitos mínimos del sistema

1. **Caso de negocio con ROI justificado**: proceso manual, tiempo/costo/frecuencia actual, por qué automatizarlo escala mejor y dónde dejaría de tener sentido.
2. **Al menos dos fuentes de entrada distintas**: combinación de webhook, API externa por HTTP (con API Key u OAuth2), y/o un servicio de Google.
3. **Lógica de control y transformación con criterio**: cada nodo debe tener una razón identificable (se puede documentar con sticky notes).
4. **Un AI Agent (no un nodo de IA simple)** que:
   - Tenga system prompt completo (rol, alcance, tono, límites, manejo de ambigüedad).
   - Tome una decisión real dentro del flujo (elegir acción, clasificar, derivar), no solo generar texto.
   - Esté justificado: por qué hace falta un agente y no alcanzaba un nodo simple.
5. **Decisión de modelo local vs. nube**, justificada por costo/volumen, privacidad y dependencia de proveedores. Se pueden combinar modelos distintos en distintos pasos, cada uno justificado.
6. **Canal de salida orientado a un caso real**: WhatsApp, mail, fila en Sheets, evento en Calendar, etc. Si es WhatsApp, el prompt debe reflejar tono breve/informal y derivación a humano si corresponde.
7. **Manejo de errores y casos límite**: identificar al menos dos puntos donde algo puede fallar (API caída, dato ambiguo, mala interpretación del agente) y cómo el diseño lo contempla (nodos If con status codes, límites en el prompt, validaciones antes de ejecutar sobre datos reales).

### Cómo armar el repositorio de entrega

La entrega es un **repositorio** (GitHub/GitLab), no un archivo suelto:

1. **Workflow exportado en `.json`** (menú de 3 puntos → Download en n8n). Nombre claro, ej. `workflow-agente-whatsapp.json`.
2. **README.md** con: caso de negocio y ROI estimado, justificación del modelo (local vs. nube), por qué se necesita un AI Agent y no un nodo simple, y los dos puntos de posible fallo contemplados.
3. **System Prompt completo** del agente, en un bloque de código dentro del README.
4. **Capturas** del canvas del workflow y de una ejecución de prueba exitosa (carpeta `/capturas`).

> ⚠️ **Aviso importante**: revisar antes de entregar que el `.json` no tenga credenciales pegadas a mano en algún nodo (n8n no exporta las credenciales guardadas, pero sí valores escritos directo, como una API Key en un header). Borrarlas del archivo si aparecen.

### Checklist de entrega
- [ ] `.json` del workflow exportado desde n8n.
- [ ] README explica caso de negocio, ROI y por qué se automatiza.
- [ ] README justifica elección de modelo (local vs. nube).
- [ ] System Prompt completo y visible en el README.
- [ ] Capturas del canvas y de una ejecución.
- [ ] Al menos dos entradas distintas, un AI Agent y un camino de manejo de errores.

### Rúbrica (100 pts, aprobación 70)

| Criterio | Peso |
|---|---|
| Implementación del workflow en n8n | 50% |
| Caso de negocio, ROI y justificación | 10% |
| Configuración del AI Agent y del modelo | 25% |
| Manejo de excepciones y robustez del flujo | 15% |
