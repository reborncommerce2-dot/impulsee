# Impulse — Fase 2

Fase 2 de la reconstrucción de Impulse desde cero. Esta entrega parte de Fase 1 y agrega backend seguro, autenticación y sincronización offline-first.

## Qué agrega
- Supabase Auth: email/password, Google, Apple y teléfono/SMS.
- Sesión persistente.
- Perfil vinculado al `auth.users.id`.
- IndexedDB con outbox persistente.
- Sync automático al iniciar sesión, recuperar conexión y cada 10 segundos mientras hay sesión.
- Pull incremental por `updated_at`.
- Edge Function `sync` con whitelist y JWT.
- PostgreSQL normalizado + RLS.
- Storage privado por usuario.
- Soporte de biometría local para desbloquear una sesión ya autenticada en dispositivos compatibles.
- Estados de sincronización y modo local de desarrollo cuando no hay variables Supabase.

## Arranque local

```bash
npm install
cp .env.example .env
# completar VITE_SUPABASE_URL y VITE_SUPABASE_ANON_KEY
npm run typecheck
npm run build
npm run dev
```

## Backend

Leer `supabase/README.md` y ejecutar `supabase/schema.sql` en el proyecto Supabase. Después desplegar la Edge Function:

```bash
supabase functions deploy sync
```

## Arquitectura de sync

La app escribe primero en local. Cada cambio genera una operación en `outbox`. La Edge Function autentica al usuario, valida la tabla, fuerza `user_id` desde el JWT, aplica upsert/soft-delete y devuelve cambios remotos. Los registros históricos son append-friendly por UUID e idempotencia; la configuración se actualiza por usuario.

## Seguridad

- No hay service-role keys en el cliente.
- Todas las tablas de datos de usuario tienen RLS.
- Storage es privado y las rutas se restringen a la carpeta del usuario.
- La biometría solo desbloquea el acceso local; no sustituye Supabase Auth.

## Estado

Ver `PHASE2_STATUS.md` para el alcance exacto y las configuraciones externas necesarias.

## Fase 3 — IA agente

La Fase 3 agrega `supabase/functions/ai-agent`, memoria persistente, autonomía granular, tool calling, auditoría y chat/voz. Ver `PHASE3_STATUS.md` y `docs/phase3-implementation.md`.

Configurar en Supabase:

```bash
supabase secrets set OPENAI_API_KEY=TU_CLAVE
supabase secrets set OPENAI_MODEL=gpt-5.6-luna
supabase functions deploy ai-agent
```

Nunca pongas la clave del modelo en una variable `VITE_*` ni en el código del cliente.


## Fase 4
Push y recordatorios, acciones frecuentes, Free/Premium sin cobro, panel admin agregado y exportación/eliminación de cuenta. Ver `PHASE4_STATUS.md` y `docs/phase4-implementation.md`.


## Fase 5 — configuración de producción
1. Ejecutar el SQL completo actualizado en Supabase.
2. Configurar secretos `OPENAI_API_KEY` y `OPENAI_MODEL`.
3. Deploy `ai-agent` y `ai-proactive`.
4. Configurar VAPID/FCM/APNs según plataforma si se desea push real.
5. Crear proyecto RevenueCat, apps iOS/Android, entitlement `impulse_premium` y Offerings; colocar `VITE_REVENUECAT_API_KEY` y `VITE_REVENUECAT_ENTITLEMENT_ID`.
6. Configurar productos en App Store Connect y Google Play Console y asociarlos a RevenueCat.
7. Configurar URLs/redirects OAuth de Supabase para Google/Apple.
8. Ejecutar `npm ci && npm run build` en un entorno con acceso al registry y luego `npx cap sync`.
