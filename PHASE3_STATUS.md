# Impulse — Fase 3

## Implementado

### IA agente operativo
- Edge Function `supabase/functions/ai-agent` con OpenAI Responses API.
- Tool calling tipado y whitelist de herramientas.
- El modelo no tiene acceso directo a SQL.
- Las herramientas usan el mismo dominio de datos de Impulse y validan el usuario mediante JWT + RLS.
- Soporta múltiples tool calls en una sola petición.
- Diferencia acciones ejecutadas y propuestas.
- Registra acciones en `ai_action_audit`.

### Herramientas
- Perfil.
- Hábitos: consultar, crear, editar, registrar.
- Objetivos: consultar, crear, crear subobjetivos/etapas/tareas, completar tareas.
- Consumos.
- Alimentación.
- Agua.
- Ejercicio.
- Gastos e ingresos.
- Recordatorios.
- Estadísticas.
- Comparación de períodos.
- Score y desglose.
- Home.
- Navegación.
- Memoria.

### Autonomía
- Asistente.
- Copiloto.
- Autónomo.
- Permisos granulares para registros, objetivos, recordatorios, Home, navegación, historial, memoria y voz.
- Las acciones no autorizadas quedan como propuestas.
- Las propuestas se pueden confirmar desde la interfaz.

### Memoria
- Persistente en Supabase.
- Vinculada al usuario.
- Fuente explícita.
- Editable/eliminable.
- Pantalla dentro del módulo IA.
- Separada de estadísticas.

### Contexto
- Conversaciones persistentes.
- Últimos mensajes recuperados de forma selectiva.
- Memoria relevante.
- Resumen estadístico de los últimos 7 días cuando el usuario autoriza historial.
- No se envía todo el historial bruto al modelo.

### Voz
- Botón de micrófono desde Home mediante el FAB.
- SpeechRecognition/Web Speech para STT cuando el navegador lo soporta.
- SpeechSynthesis para respuesta hablada.
- Lenguaje `es-AR`.
- Fallback claro cuando el navegador no ofrece reconocimiento.

### UI
- Chat accesible desde cualquier pantalla mediante el botón flotante.
- Pestañas Chat / Memoria / Autonomía.
- Propuestas de acciones con confirmación.
- No se agrega una sexta pestaña principal.

## Configuración necesaria fuera del código

En Supabase Edge Functions:

```bash
supabase secrets set OPENAI_API_KEY=...
supabase secrets set OPENAI_MODEL=gpt-5.6-luna
supabase functions deploy ai-agent
```

El proyecto Supabase de Fase 2 debe tener ejecutado `supabase/schema.sql`, incluyendo las nuevas tablas `ai_settings` y `ai_action_audit`.

## Deliberadamente fuera de Fase 3

- Push server-side.
- IA proactiva.
- Personalidades avanzadas.
- RevenueCat / cobro real.
- Panel administrativo.
- Planificación alimentaria avanzada.
- Acciones externas.

Esas capacidades pertenecen a fases posteriores según los documentos fuente.

## Verificación

No se pudo ejecutar `npm install` completo en este entorno porque el registro de paquetes agotó el tiempo de espera. Por eso el build final debe ejecutarse en un entorno con acceso al registro:

```bash
npm install
npm run typecheck
npm run build
```
