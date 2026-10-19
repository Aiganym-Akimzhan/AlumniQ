# AlumniConnect

Single page Kazakh language MVP with an Express API and PostgreSQL storage.

## Run locally

1. Install Node.js 18 or newer and PostgreSQL.
2. Create a database, for example `createdb alumniconnect`.
3. Copy `.env.example` to `.env`, set the PostgreSQL connection values, and replace `SESSION_SECRET`, `ADMIN_EMAIL`, `ADMIN_PASSWORD`, and `TRANSFER_PHONE` with real values.
4. Run `npm install`, then `npm start` and open `http://localhost:3000`.

The server creates its tables and three starter projects at first launch. It creates the initial administrator only if `ADMIN_EMAIL` and `ADMIN_PASSWORD` are configured and that email is not already registered. Keep `.env` private. The transfer phone shown in donation details is configured with `TRANSFER_PHONE`.

## API

- `POST /api/auth/register`, `POST /api/auth/login`, `GET /api/me`
- `GET /api/projects`, `GET /api/projects/:id`; administrator-only project creation and editing at `POST /api/projects` and `PATCH /api/projects/:id`
- `POST /api/donations`; authenticated donation history at `GET /api/dashboard`
- Public reports at `GET /api/transparency`; administrator-only create and verification at `POST /api/reports` and `PATCH /api/reports/:id/verify`
- Administrator donation reconciliation at `GET /api/admin/donations` and `PATCH /api/admin/donations/:id`

API sessions are signed bearer tokens held in browser local storage. Donations are recorded as `pledged`; staff must reconcile transfers before marking them confirmed. No payment processor is connected, and the shown phone transfer is an instruction for a manual transfer.
