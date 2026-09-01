# Impulse — Fase 4

Implementada desde Fase 3, sin usar el ZIP antiguo como base.

## Incluido
- Recordatorios locales: permiso, programación/cancelación y reprogramación desde preferencias.
- Push web real preparado con Web Push/VAPID: registro de suscripción, service worker y Edge Function de dispatch.
- Push nativo preparado mediante Capacitor Push Notifications; tokens quedan asociados al usuario.
- Preferencias anti-spam: activación, categorías, horario silencioso y máximo diario.
- Acciones frecuentes: aprendizaje de acciones repetidas, ranking por uso y ejecución en 1 toque desde Home.
- Analytics de producto agregada respetando RLS y sin exponer datos personales al panel.
- Panel Admin agregado: usuarios, activos, retención, IA/voz, hábitos, objetivos, recordatorios, errores, suscripciones, storage y Free/Premium. El RPC exige `app_metadata.role=admin`.
- Free/Premium: entitlements y UI preparadas; Premium queda desbloqueado en modo local/pruebas. No hay cobro real.
- Exportación completa cloud mediante Edge Function.
- Eliminación completa de cuenta mediante Edge Function con service role solo en servidor.
- Cuenta: exportación cloud + local, borrado local, borrado cloud, cierre de sesión.
- Analytics base para acciones frecuentes/notificaciones.

## Configuración externa pendiente
- VAPID_PUBLIC/PRIVATE/SUBJECT para Web Push.
- Credenciales FCM/APNs y configuración de las apps nativas para push nativo.
- Para Admin: asignar `app_metadata.role = admin` al usuario autorizado y, opcionalmente, agregar su email a `VITE_ADMIN_EMAILS` para mostrar el acceso en el menú.
- Monetización real queda fuera: esta fase prepara Free/Premium sin cobro, tal como indica la especificación.

## Verificación
El entorno no permitió una instalación npm completa durante las fases anteriores; por eso no se declara un build final limpio. Se revisaron sintaxis/estructura y se dejó documentada la configuración necesaria.
