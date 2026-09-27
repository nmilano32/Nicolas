# Módulo 5 · Creando workflows con aplicaciones y servicios externos

## Planificar un workflow antes de construirlo: entrada, proceso y salida

Antes de abrir n8n conviene pasar por una fase de diseño estratégico, para evitar reconstruir el workflow varias veces.

### 1. Entender el problema de negocio, no solo la tarea
¿Qué proceso manual se automatiza y por qué (tiempo, errores, costo, escalabilidad)? ¿Cuál es el resultado esperado en términos de negocio?

### 2. Diseñar el proceso
Dibujar el flujo real con todos sus pasos, planificando qué herramientas externas hacen falta. Anticipa errores e improvisaciones.

### 3. Sistemas, credenciales y permisos
¿Qué APIs/servicios hace falta conectar? ¿Tienen límites de rate, cuotas, requieren OAuth? Verificar accesos **antes** de construir.

### 4. Manejo de errores y casos límite
¿Qué pasa si una API falla o responde lento? ¿Datos duplicados, vacíos o mal formateados? ¿Hacen falta reintentos, alertas, revisión humana?

### 5. Idempotencia y reejecución
Si el workflow corre dos veces con el mismo dato (reintento o fallo), ¿duplica registros o emails?

### 6. Logging, monitoreo y alertas
¿Cómo se sabe si falló en producción sin que alguien avise? ¿Dónde quedan los logs? ¿Hay alertas a Slack/email?

### 7. Escalabilidad y mantenimiento
¿Quién mantiene el workflow si el autor se va? ¿Está documentado? ¿Cómo se versiona (n8n permite exportar JSON, útil para git)? ¿El diseño modular permite reutilizar sub-workflows?

## Conectando servicios de Google

Ejemplo de todo el módulo: workflow que completa datos faltantes en un Google Sheet (columna ID siempre completa; Nombre, Edad y Cargo vacías hasta completarlas).

```
Manual Trigger → Google Sheets (leer) → Filter → HTTP Request → Google Sheets (actualizar) → Aggregate → Gmail
```

- **Manual Trigger**: correcto en fase de desarrollo, para no dispararse solo mientras se prueba.
- **Filter**: resuelve idempotencia (evita reprocesar información ya completa).
- **HTTP Request**: trae datos de una API que completa los IDs solicitados.
- **Aggregate antes de Gmail**: evita disparar un correo por cada item (5 correos en vez de uno).
- **Gmail final**: confirma que el proceso terminó bien.
