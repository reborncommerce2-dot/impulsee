# Fase 3 — implementación técnica

La Fase 3 convierte a Impulse de una app con funciones separadas en un agente operativo conectado a los datos de la cuenta.

## Flujo

1. Cliente obtiene la sesión Supabase.
2. Cliente envía el mensaje a `ai-agent` con el JWT de Supabase.
3. Edge Function valida al usuario mediante `auth.getUser()`.
4. Recupera configuración de autonomía, memoria permitida y contexto reciente.
5. Recupera un resumen estadístico selectivo si el historial está autorizado.
6. Envía al modelo instrucciones + conversación reciente + tools.
7. El modelo devuelve tool calls tipadas.
8. La Edge Function decide ejecutar o proponer según autonomía + permisos.
9. Las acciones ejecutadas pasan por funciones de dominio y RLS.
10. Cada acción queda auditada.
11. Los resultados de las tools vuelven al modelo.
12. El modelo produce la respuesta final.
13. El cliente muestra acciones propuestas y permite confirmarlas.

## Seguridad

La API key de OpenAI vive únicamente en Supabase Edge Functions. Nunca se usa una variable `VITE_*` para secretos.

El modelo no recibe acceso directo a Postgres ni puede ejecutar SQL. Cada herramienta conoce explícitamente qué tabla y qué campos puede modificar.

## Acciones de alto riesgo

No se incluyen eliminación de cuenta, eliminación masiva ni cambios de seguridad como tools automáticas de esta fase. Las funciones estructurales requieren permisos granulares.

## Voz

La implementación usa Web Speech API como capa de voz para el prototipo multiplataforma. La arquitectura queda desacoplada en `src/ai/voice.ts`, permitiendo sustituirla por una integración nativa/realtime posterior sin cambiar el modelo de conversación.
