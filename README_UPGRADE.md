
# NEXO Patch (Login real + Ensure Tenant + Header + Guard)

## Qué incluye
- `lib/supabaseServer.ts`: cliente server-side que lee la sesión desde cookies.
- `app/api/tenant/ensure/route.ts`: crea tenant + vínculo si el usuario no los tiene (idempotente).
- `app/auth/login/page.tsx`: login real con Supabase y llamada a `/api/tenant/ensure`.
- `app/app/page.tsx`: protección de ruta (redirige a `/auth/login` si no hay sesión).
- `components/UserMenu.tsx`: muestra Iniciar/Probar si no hay sesión y Cerrar sesión si hay.
- `app/layout.tsx`: integrado `<UserMenu />` en el header.
- `.env.example`: variables necesarias.

## Variables
Crea `.env.local` con:
```
NEXT_PUBLIC_SUPABASE_URL=...
NEXT_PUBLIC_SUPABASE_ANON_KEY=...
SUPABASE_SERVICE_ROLE_KEY=...   # opcional si usas supabaseAdmin
```

## SQL necesario (ya aplicado en Supabase)
- Función `create or replace function public.is_member(uuid)`
- Políticas: `tenants_insert_self`, `tenants_select_contact_owner`, `ut_insert_self_scoped`, `clients_update_member with check`

## Prueba
1. Registro con correo nuevo → llega verificación.
2. Login → ejecuta `/api/tenant/ensure` → redirige a `/app`.
3. Verifica en Supabase que `user_tenants` tenga `tenant_id` para el usuario.

## Notas
- Deja el archivo mal escrito `lib/supabaseseServer.ts` sin uso o elimínalo.
- Si usas TypeScript alias `@/*`, asegúrate de tener `baseUrl`/`paths` configurados (ya lo tenías).
