# Fase 5 — implementación

## Backend
- `ai-proactive`: genera recomendaciones a partir de huecos de hábitos, objetivos próximos a vencer, actividad financiera y tendencias positivas.
- Tablas `ai_persona_settings`, `ai_proactive_settings`, `ai_proactive_events`, `meal_plans`, `meal_plan_items`, `achievements`.
- RLS por usuario.

## Cliente
- Personalidad de IA e intensidad.
- Configuración de IA proactiva.
- Bandeja de recomendaciones.
- Plan semanal de comidas y cumplimiento.
- Hitos/logros conceptuales.
- Adaptador RevenueCat.

## Monetización
RevenueCat se inicializa por usuario cuando existe la dependencia y la API key. La compra/Paywall no se habilita automáticamente hasta configurar Offering + entitlement `impulse_premium`.
