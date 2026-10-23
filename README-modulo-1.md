# Módulo 1 · Coordinador de Agenda

**Clínica:** CLINICA ODONTOLOGICA AUTOMATION  
**Workflow:** `checkpoint1_paulo_flores.json`

## Qué hay en el lienzo

| Nodo | Configuración / rol | Requisito que cumple |
| --- | --- | --- |
| **When chat message received** | Chat Trigger | Disparador con mensaje libre del paciente |
| **AI Agent** | Tools Agent, máximo 5 iteraciones; devuelve `intermediateSteps` | Cerebro del flujo y guardrail de 5 a 10 vueltas |
| **OpenAI Chat Model** | `gpt-4o`, temperatura `0.2` | Modelo conectado de forma nativa |
| **Memoria de la conversación** | Simple Memory; últimos 10 mensajes por sesión de chat | Permite que el agente recuerde las 3 opciones que ofreció cuando el paciente elige una. Es memoria corta de n8n, no la memoria de Airtable del Módulo 3 |
| **Consultar_disponibilidad_turnos** | Google Calendar Tool, operación Availability (free/busy) | Tool lateral con descripción extensa del negocio |
| **Log de observabilidad (Gmail)** | Envía un correo con el mensaje, los pasos del agente y la respuesta | Observabilidad / Execution Log |
| **Respuesta al paciente** | Devuelve al chat la respuesta del agente | El chat muestra la respuesta al paciente y no la salida de Gmail |

## System Message

El mensaje del sistema está dividido en estas secciones:

**Rol → Contexto → Ámbito → Objetivo → Reglas → Restricciones → Escalamiento**

Usa masculino genérico y, por ahora, no reserva turnos.

## Flujo de turnos

- Ante cualquier pedido de turno, responde en un solo mensaje con el horario de atención y **3 opciones libres numeradas**.
- Si el paciente no elige ninguna opción, pide día y fecha y consulta la disponibilidad de ese día.
- Cada vez que deriva a la clínica, proporciona el teléfono **341-602288**.

