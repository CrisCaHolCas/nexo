
# NEXO CRM — Web (Next.js 14 + Tailwind)

Starter funcional con páginas públicas y panel autenticado (placeholders) para NEXO.

## Requisitos
- Node.js 18+
- npm o pnpm

## Configuración
```bash
cp .env.example .env.local
npm install
npm run dev
```
Abre http://localhost:3000

## Estructura
- **/app**: App Router (Next.js)
- **/components**: UI reusable
- **/lib**: utilidades y estados (Zustand)
- **/app/(public)**: Landing, login, registro
- **/app/(app)**: Panel (protegido), Clientes, Campañas, Alertas, Configuración, Suscripción

## Notas
- Autenticación: placeholder con "demo login" local (sustituir por tu proveedor real).
- WhatsApp Cloud API: pendiente de integrar (incluye vistas, formularios y estados).
- Pagos: placeholders para Stripe/Mercado Pago y pantalla de suscripción.
- Multi-tenant: simulado con `tenantId` en cookie; back real deberá aplicar RLS por empresa.
- Textos y flujos están alineados con la Especificación Funcional v1.0 (2025-08-09).
