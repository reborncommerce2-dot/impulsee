# Fase 2 — Implementación

La Fase 2 sigue `IMPULSE_PLAN_ARQUITECTURA_v1.md` y `IMPULSE_MASTER_SPEC_v1.md`.

### Arquitectura
- Cliente: React + TypeScript + Vite.
- Local: IndexedDB compatible con la PWA actual; la interfaz nunca espera a la red.
- Cloud: Supabase Postgres + Auth + Storage + Edge Functions.
- Sync: outbox local + pull incremental por `updated_at`.
- Seguridad: RLS `user_id = auth.uid()`.

### Autenticación
La aplicación no muestra el contenido de Impulse sin una cuenta cuando Supabase está configurado. Soporta email/password, Google, Apple y teléfono/SMS. La biometría no reemplaza la autenticación de servidor: desbloquea la sesión local ya autenticada.

### Conflictos
Los UUID permiten idempotencia. Los registros históricos se conservan como entradas independientes; la edición/eliminación se representa mediante `deleted_at`. Las entidades de configuración usan upsert por usuario.

### Sincronización
La cola se persiste en IndexedDB. La Edge Function valida usuario y tabla, asigna `user_id` desde el JWT, descarta campos no permitidos y devuelve cambios posteriores a `since`. El cliente integra esos cambios en su estado local.

### Limitaciones reales
OAuth, SMS, Supabase y biometría requieren configuración de proveedores/capacidades de plataforma. El código no contiene secretos ni intenta simular esas integraciones como si fueran reales.
