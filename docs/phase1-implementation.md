# Fase 1 — contrato de implementación

## Modelo
Las entidades principales están tipadas en `src/domain/types.ts`: Profile, Area, Habit, HabitLog, Objective, ObjectiveItem, Consumption, ConsumptionLog, Meal, WaterLog, Workout, Income, Expense, Budget, FinancialGoal, FrequentAction, Reminder, ScoreSnapshot, HomeLayout y NavLayout.

## Persistencia
`src/db/localDb.ts` encapsula la persistencia. En navegador usa IndexedDB y conserva todo el estado entre recargas. La interfaz queda aislada para poder sustituirse por SQLite nativo mediante Capacitor sin cambiar las vistas.

## Score
`src/domain/score.ts` produce un valor 0–100 y un breakdown por área/factores. Es una primera implementación explicable de Fase 1, no el algoritmo comercial definitivo.

## Principios UX aplicados
- Registro rápido.
- Profundidad opcional.
- Sin sección independiente de pasos.
- Agua integrada en Alimentación/Bienestar.
- Sin sexta pestaña de recomendaciones.
- Estados compactos y responsive.
- Acceso al registro rápido desde un botón flotante.
