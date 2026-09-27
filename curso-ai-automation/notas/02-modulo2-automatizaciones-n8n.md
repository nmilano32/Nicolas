# Módulo 2 · Introducción a las automatizaciones y n8n

## ¿Qué es una automatización?

Uso de tecnología para realizar tareas repetitivas sin intervención humana. Transforma el trabajo operativo en costo fijo: un servidor que procesa 100 webhooks/minuto cuesta y tarda lo mismo que procesando 10.000, permitiendo escalar sin colapsar la logística.

A nivel corporativo, automatizar es **integrar y orquestar sistemas**. Analogía de la orquesta: cada aplicación (WhatsApp, Sheets, Gmail) es un instrumento; la orquestación coordina esas herramientas para que funcionen como un solo mecanismo.

- **Automatizaciones lineales**: orden fijo y predecible, sin IA tomando decisiones ("si pasa A, hacé B y después C").
- **Automatizaciones cognitivas**: en algún paso se delega interpretación/razonamiento/generación a un modelo de IA, que "entiende" el contenido y decide con cierto criterio.

## ROI, escalabilidad y estandarización de procesos

**ROI (Return on Investment)**: métrica de rentabilidad. En automatización se mide también en tiempo recuperado, no solo dinero.

```
ROI = (Beneficio neto / Costo de la inversión) × 100
```

- **Costo de inversión**: horas de desarrollo, licencias, hosting, mantenimiento.
- **Beneficio neto**: ahorro en horas manuales, más ventas por respuestas rápidas, menos errores.

Es rentable cuando el ROI es positivo y supera el costo de oportunidad.

> **ROI oculto**: aunque el ahorro monetario directo sea $0, liberar tiempo del dueño del negocio para vender o mejorar el producto puede hacer la inversión muy rentable a largo plazo.

Umbrales a considerar:

- **Break-even**: momento en que el ahorro acumulado iguala el costo de implementación.
- **Regla 80/20**: automatizar procesos de alta frecuencia y bajo juicio humano (algo que se hace 1 vez al año siempre da ROI negativo).
- **Costo de oportunidad**: lo que se deja de ganar por hacer tareas manuales (ej. un vendedor perdiendo horas copiando datos en Excel).

## ¿Qué es n8n? Instancias, ejecución local y en la nube

n8n es una herramienta **low-code y fair-code** para conectar aplicaciones/servicios y automatizar tareas sin escribir código (aunque se puede si hace falta).

- **No code**: todo por interfaz visual, con bloques prearmados (limitado si el bloque no alcanza).
- **Low code**: interfaz visual + posibilidad de código cuando se necesita.

Cada nodo es código ya escrito por n8n o su comunidad; solo se configuran parámetros.

### Instancia

Copia en ejecución de n8n corriendo en algún lado.

1. **n8n Cloud**: hospedada y gestionada por n8n (SaaS), sin infraestructura propia que administrar.
2. **Self-hosted**: uno mismo administra la infraestructura (redes, bases de datos, Docker). Requiere Node o Docker.

### JSON

Formato estándar de intercambio de datos entre nodos: `"Llave": "Valor"`, entre llaves `{}`. Todo lo que viaja entre nodos de n8n es JSON.

```json
{
  "nombre": "Juan",
  "apellido": "Perez",
  "id_cliente": 10
}
```

### Workflow

Secuencia organizada de pasos automatizados, guardada como archivo JSON. Define: cuándo empieza, qué acciones hace, cómo se conectan, qué decisiones toma. Es el mapa completo de la automatización.

## Importar y reutilizar templates

Un **template** es un workflow completo prearmado por alguien para un caso de uso específico. n8n tiene biblioteca pública (app o n8n.io/workflows).

**Importar**: traerlo a la propia instancia, desde la interfaz o manualmente con un archivo `.json` (Import from File/URL).

**Reutilizar**: una vez importado se puede modificar libremente:
- Adaptar credenciales propias.
- Ajustar lógica (condiciones, campos, filtros).
- Guardarlo como plantilla interna para duplicar en otros proyectos.

---

## 📌 Preentrega 1: De la idea al prompt

**Consigna**: diseñar (sin construir) una automatización simple con un paso de IA.

1. Elegir un proceso manual y repetitivo.
2. Justificar el ROI (2-3 líneas: tiempo actual, frecuencia, escalabilidad).
3. Bocetar el flujo (trigger → pasos intermedios → paso de IA → output).
4. Escribir el prompt del nodo de IA (rol, tarea, contexto, formato de salida — no vale "resumime esto").
5. Reflexión (3-4 líneas): ¿qué podría salir mal? (alucinaciones, límites de contexto, ambigüedad) y cómo mitigarlo.

**Entrega**: un único PDF con las partes tituladas. Aprobación: 70/100 pts.
