# Impulse Fase 2 — Backend, autenticación y sincronización

## Implementado en el código
- Cliente Supabase opcional por variables VITE_SUPABASE_URL / VITE_SUPABASE_ANON_KEY.
- Sesión persistente con Supabase Auth.
- Email + contraseña.
- Google OAuth.
- Apple OAuth.
- Teléfono + SMS OTP.
- Capa de biometría local para iOS/Android mediante Capacitor (Face ID / Touch ID / biometría equivalente cuando el dispositivo lo permite).
- IndexedDB local con cola `outbox` persistente.
- Cada escritura de dominio genera operaciones de sincronización.
- Sincronización automática al iniciar sesión, al recuperar conexión y periódicamente mientras hay sesión.
- Estados de registro preparados como pendiente/sincronizado/error.
- Backend Supabase normalizado, sin JSON gigante de usuario.
- RLS por usuario en todas las tablas de datos.
- Storage privado con carpeta por usuario.
- Edge Function `sync` con whitelist de tablas y autenticación por JWT.
- Pull incremental mediante `updated_at`.
- Upsert idempotente por UUID.
- Soft delete para no perder historial ante fallos de sync.
- Esquema preparado para perfil, layouts, dispositivos, suscripciones, memoria/IA, archivos y analítica futura.

## Configuración externa obligatoria
1. Crear proyecto Supabase.
2. Ejecutar `supabase/schema.sql`.
3. Configurar Email en Auth.
4. Configurar Google y Apple OAuth en Supabase y sus respectivas consolas.
5. Configurar Phone/SMS y el proveedor SMS en Supabase.
6. Instalar/usar Supabase CLI y desplegar `supabase/functions/sync`.
7. Crear `.env` desde `.env.example`.
8. Para iOS/Android: `npx cap sync` y configurar permisos de biometría según plataforma.

## Comandos
```bash
npm install
npm run typecheck
npm run build
npx cap sync
```

## Importante
Las credenciales reales de Supabase y la configuración de proveedores OAuth/SMS no pueden estar dentro del repositorio ni pueden ser inventadas. Sin esas credenciales la app arranca en modo local de desarrollo; con ellas se activa autenticación y nube real.
