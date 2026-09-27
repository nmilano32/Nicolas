# Módulo 3 · Conceptos básicos

## Anatomía de un workflow: nodos, conexiones y flujo de datos

Un workflow es una secuencia de pasos automatizados, representada como diagrama de nodos conectados.

### Nodos

Unidad mínima de trabajo. Tipos según su función:

- **Trigger (disparador)**: inicia la ejecución (webhook, evento de una app, ejecución manual). Siempre al principio.
- **Action (acción)**: ejecuta una tarea concreta (crear registro, enviar mensaje).
- **Transform (transformación/lógica)**: procesa/modifica datos (Set, Function/Code, Merge, IF, Switch), sin conectarse necesariamente a un servicio externo.

Anatomía visual: cuerpo (ícono + nombre), conectores de entrada (izquierda), conectores de salida (derecha, pueden ser múltiples), estado visual (no ejecutado / éxito / error).

### Conexiones

Líneas que unen salida de un nodo con entrada de otro. Definen orden de ejecución y camino de los datos.

## Nodos principales en n8n

### Edit Field (Set)
Crea, modifica o elimina campos de cada item. Usarlo para: dejar datos prolijos, combinar campos (ej. nombre completo), adaptar estructura para el nodo siguiente.

### IF
Evalúa una condición y deriva por dos ramas: `true`/`false`. Cada item se evalúa individualmente (algunos pueden ir por una rama y otros por otra en la misma ejecución).

### Switch
Evolución del IF para 3+ caminos posibles (evita anidar múltiples IF).

### Aggregate
Agrupa varios items en uno solo (ej. un email con todos los pedidos del día en vez de uno por pedido). Útil cuando el paso siguiente necesita "todo junto".

### Merge
Combina datos de dos ramas distintas en una sola salida — "cierra" una bifurcación o cruza datos de dos fuentes (ej. CRM + planilla).

### Wait
Pausa la ejecución (tiempo fijo, fecha/hora específica, o hasta cumplir una condición externa como un webhook). No modifica datos, solo detiene el avance y después continúa igual.
