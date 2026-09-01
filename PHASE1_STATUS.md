# Impulse Fase 1 — estado

## Implementado funcionalmente
- Onboarding obligatorio de perfil local antes de entrar.
- Home compacto con Score, progreso diario, hábitos, objetivos, agua, ejercicio y actividad.
- Barra principal limitada a 5 accesos y menú secundario.
- Reordenamiento de navegación.
- Home configurable por módulos.
- Áreas predeterminadas y áreas personalizadas.
- Hábitos: creación, tipos, positivo/negativo y registro diario.
- Objetivos: creación, progreso y tareas/subobjetivos/etapas como estructura extensible.
- Vicios: Tabaco, Cannabis, Alcohol y consumos personalizados; registro rápido.
- Finanzas: ingresos y gastos.
- Alimentación: comidas simples.
- Agua: registro en ml e histórico.
- Ejercicio: actividad + duración + histórico.
- Recordatorios: creación de recordatorios manuales.
- Registro rápido universal: parser local para agua, entrenamiento, gasto y hábitos existentes.
- Persistencia offline mediante IndexedDB en navegador.
- Exportación JSON.
- Eliminación de datos locales.
- PWA/service worker.
- Score 0–100 con desglose y factores explicables.

## Deliberadamente fuera de Fase 1
- Supabase/Auth real y sincronización nube.
- IA remota con tool calling.
- Memoria persistente de IA.
- Voz STT/TTS real.
- Push remoto y recordatorios inteligentes server-side.
- Biometría real.
- Compras reales/RevenueCat.
- Panel administrativo.

Esas capas están definidas para las fases siguientes en `IMPULSE_PLAN_ARQUITECTURA_v1.md`.
