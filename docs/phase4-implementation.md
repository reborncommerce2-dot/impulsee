# Implementación Fase 4

La Fase 4 sigue el plan arquitectónico: `Recordatorios/push, acciones frecuentes, panel admin, Free/Premium (sin cobro real), exportación/eliminación de cuenta.`

## Arquitectura
- Cliente React + Capacitor continúa siendo la base.
- Supabase conserva RLS por usuario.
- Push web usa Service Worker + Web Push/VAPID.
- Push nativo usa Capacitor Push Notifications y persiste el token en `push_subscriptions`.
- Recordatorios normales no dependen de la red: se programan con Local Notifications.
- `admin_metrics()` es una función `security definer` que exige `app_metadata.role=admin` y devuelve agregados, no registros personales.
- Exportación consulta solo datos autorizados por RLS.
- Eliminación de cuenta usa `auth.admin.deleteUser` exclusivamente en Edge Function.
- Free/Premium se resuelve por `profiles.plan` y entitlements, sin proveedor de pagos todavía.

## Edge Functions
- `account-export`
- `account-delete`
- `push-dispatch`
- `admin-metrics`

## SQL
Ejecutar `supabase/schema.sql` completo en el proyecto Supabase. Incluye las tablas y políticas nuevas de Fase 4.
