Módulo 1 · Coordinador de Agenda (**CLINICA** **ODONTOLOGICA** **AUTOMATION**)

Workflow: checkpoint1_paulo_flores.json 
Qué hay en el lienzo
Nodo	Rol	Requisito que cumple
When chat message received	Chat Trigger	Disparador con mensaje libre del paciente
AI Agent	Tools Agent, máx. 5 iteraciones, devuelve intermediateSteps	Cerebro + guardrail de 5 a 10 vueltas
OpenAI Chat Model	gpt-4o, temperatura 0.2	Modelo conectado de forma nativa
Memoria de la conversación	Simple Memory, últimos 10 mensajes por sesión de chat	Que el agente recuerde las 3 opciones que ofreció cuando el paciente elige una (memoria corta de n8n, no es la de Airtable de M3)
Consultar_disponibilidad_turnos	Google Calendar Tool, operación Availability (free/busy)	Tool lateral con descripción de negocio extensa
Log de observabilidad (Gmail)	Mail con mensaje, pasos del agente y respuesta	Observabilidad / Execution Log
Respuesta al paciente	Devuelve la respuesta del agente al chat	Que el chat muestre la respuesta y no la salida de Gmail
El System Message está dividido en Rol → Contexto → Ámbito → Objetivo → Reglas → Restricciones → Escalamiento, usa masculino genérico y no reserva turnos, por ahora.
Flujo de turnos: ante cualquier pedido de turno responde en un solo mensaje con el horario de atención y 3 opciones libres numeradas. Si el paciente no elige ninguna, le pide día y fecha y consulta ese día. Cada vez que deriva a la clínica da el teléfono **341**-**602288**.