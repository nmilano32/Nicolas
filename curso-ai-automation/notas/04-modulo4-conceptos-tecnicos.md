# Módulo 4 · Conceptos técnicos

## ¿Qué es una API? Modelo cliente-servidor y endpoints

**API (Application Programming Interface)**: la forma en que dos programas se hablan entre sí.

Analogía del mozo de restaurante: uno (cliente) no entra a la cocina, le pide al mozo (API), el mozo lleva el pedido a la cocina y trae la respuesta.

En n8n, cada nodo de servicio (Gmail, Slack, Sheets) usa por dentro la API de ese servicio. Si un servicio no tiene nodo propio, se puede usar el nodo genérico **HTTP Request** hablando directo a su API.

Qué viaja en un pedido a una API: qué queremos hacer, a dónde (URL), con qué datos, y quiénes somos (autenticación). Responde: si funcionó o no, y los datos (o el error).

## ¿Qué es HTTP?

**HTTP (HyperText Transfer Protocol)**: idioma/protocolo que usan las APIs (y navegadores) para comunicarse. Define cómo se arma un pedido y una respuesta.

### Request (lo que mandamos)
- **URL**: dirección exacta.
- **Método**: qué acción.
- **Headers**: info adicional (formato, credenciales).
- **Body**: los datos, cuando aplica.

### Response (lo que devuelven)
- **Status code**: número que indica qué pasó.
- **Headers**: info adicional.
- **Body**: datos devueltos (generalmente JSON).

### Métodos HTTP

| Método | Qué significa | Ejemplo |
|---|---|---|
| GET | Leer, sin modificar | Traer lista de clientes |
| POST | Crear algo nuevo | Crear un cliente |
| PUT | Reemplazar/actualizar completo | Actualizar todos los datos |
| PATCH | Actualizar parcialmente | Cambiar solo el teléfono |
| DELETE | Eliminar | Borrar un cliente |

### Status codes

| Rango | Significado | Ejemplos |
|---|---|---|
| 200-299 | Éxito | 200 OK, 201 Created |
| 300-399 | Redirección | (poco frecuente) |
| 400-499 | Error del cliente | 400 Bad Request, 401 Unauthorized, 404 Not Found |
| 500-599 | Error del servidor | 500 Internal Server Error |

## Credenciales y autenticación: API Keys y OAuth2

La **autenticación** responde: ¿quién sos y tenés permiso?

- **API Key**: código único que da la plataforma, va en headers o parámetro de URL. Como tarjeta de acceso.
- **Basic Auth**: usuario + contraseña codificados. Simple, poco usada hoy.
- **Bearer Token**: similar a API Key pero temporal, va en el header `Authorization`. Como pulserita de evento con vencimiento.
- **OAuth2**: el más robusto (Google, Microsoft, Slack). Inicia sesión con cuenta real y da permiso temporal y renovable.

### Credenciales en n8n

Se configuran una vez en **Credentials**, quedan encriptadas (no en texto plano), se reutilizan en varios workflows/nodos. Cada tipo de nodo pide el tipo de credencial que su servicio requiere.

### HTTP Request

Nodo genérico, no atado a ningún servicio. Permite armar a mano una petición completa (método, URL, headers, body, autenticación). Se usa cuando: el servicio no tiene nodo propio, el nodo nativo no cubre algo específico, o se está explorando una API antes de automatizar algo más grande. Los nodos "de marca" son básicamente HTTP Requests preconfigurados.

---

## 📌 Preentrega 2: Infraestructura de integración técnica

**Consigna**: construir un workflow funcional en n8n.

1. Elegir un disparador (Webhook o consumo de API pública vía HTTP; alcanza con API Key simple).
2. Procesar datos con lógica de control/transformación (Wait, Merge, Aggregate, Switch, If, Edit Fields, etc.) donde realmente aporten valor.
3. Mapear la anatomía del workflow (trigger → nodos intermedios → output).
4. Entregar un output final claro (respuesta HTTP, archivo, o JSON visible).
5. Reflexión (3-4 líneas): ¿qué pasa si la API cae o da error? ¿dónde iría el manejo de error?

**Entrega**: un único PDF con capturas del workflow, del output, diagrama y reflexión. Aprobación: 70/100 pts.
