# Bot Agencia de Viajes (n8n)

Bot de chat que capta los datos del cliente y los transfiere a vendedores.

## Flujo

```
Chat del cliente → Asistente de viajes (AI Agent) → respuesta al cliente
                      ├─ Modelo Claude (Anthropic)
                      ├─ Memoria de conversación (40 mensajes, por sesión)
                      └─ Herramienta: Transferir_cliente_a_vendedores (Gmail)
```

## Datos captados

- Obligatorios: nombre, teléfono, destino, fecha de salida, duración, adultos, niños y edades, ciudad de origen.
- Opcionales: correo, presupuesto, tipo de servicio, hospedaje, observaciones.

## Comportamiento

- Extrae datos del historial antes de preguntar. "Quiero ir a Margarita" fija el destino.
- No repite preguntas. Confirma datos ambiguos.
- Pide máximo 2 datos por mensaje.
- No da precios. Indica que el vendedor envía la cotización.
- Muestra un resumen y pide confirmación.
- Envía la ficha por correo al equipo de ventas tras la confirmación.
- Transfiere de inmediato si el cliente pide hablar con una persona.

## Instalación

1. Abre n8n y entra en la carpeta personal `demo`.
2. Crea un workflow nuevo.
3. Selecciona menú `...` → `Import from File`.
4. Elige `bot-agencia-viajes.json`.
5. Asigna la credencial Anthropic en el nodo `Modelo Claude`.
6. Asigna la credencial Gmail en el nodo `Transferir_cliente_a_vendedores`.
7. Reemplaza `ventas@tu-agencia.com` por el correo de ventas.
8. Ajusta la zona horaria `America/Caracas` si aplica.
9. Prueba con el botón `Open chat`.
10. Activa el workflow para publicar la URL del chat.

## Prueba sugerida

1. Escribe: "Hola, ¿en cuánto está un viaje a Margarita para mi esposa y yo?"
2. Verifica que el bot no pregunte destino ni número de adultos.
3. Completa fechas, origen, nombre y teléfono.
4. Confirma el resumen.
5. Verifica el correo en la bandeja de ventas.
