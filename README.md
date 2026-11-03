# Doctor Chamber Management — Frontend

Next.js 15 frontend for a doctor-chamber (private clinic) management system, branded **MedCore**. It gives each of the three people who run a chamber their own portal: an admin who manages doctors and subscriptions, an assistant who registers patients and runs the queue, and a doctor who sees patients and writes prescriptions.

> This repository is the frontend only. It talks to a separate REST + Socket.IO backend at `NEXT_PUBLIC_API_URL`.

## Features

| Portal | What it does |
|---|---|
| **Admin** (`/admin`) | Dashboard, create and manage doctors and assistants, doctor subscriptions, settings |
| **Assistant** (`/assistant`) | Patient search and registration, pre-assessment (vitals), appointment booking, live patient queue with printable tokens, PDF reports |
| **Doctor** (`/doctor`) | Dashboard, today's queue, appointments, patient history, prescription builder, settings |

- **Role-based routing** — `middleware.ts` reads the auth cookies and keeps each role inside its own portal.
- **Real-time queue** — assistants and doctors join Socket.IO rooms and receive `queue-update` events, so the doctor's queue changes the moment a patient is checked in.
- **Forms** — React Hook Form + Zod schemas for login, doctors and prescriptions.
- **State and data** — TanStack Query for server state, Zustand for auth/queue/UI state, Axios API client.
- **Printing** — jsPDF for queue tokens and reports.

## Tech stack

Next.js 15 (App Router) · React 19 · TypeScript · Tailwind CSS 4 · TanStack Query · Zustand · React Hook Form · Zod · Socket.IO client · jsPDF · Lucide icons

## Getting started

```bash
cp .env.local.example .env.local   # point NEXT_PUBLIC_API_URL / NEXT_PUBLIC_SOCKET_URL at your backend
npm install
npm run dev                        # http://localhost:3000
```

| Script | Description |
|---|---|
| `npm run dev` | Start the dev server |
| `npm run build` | Production build |
| `npm run start` | Serve the production build |
| `npm run lint` | Lint with ESLint |

## Project structure

```
app/
  (admin)/admin/…      admin portal
  (doctor)/doctor/…    doctor portal
  assistant/…          assistant portal
  auth/…               login, forgot password
components/            portal-specific and shared UI components
lib/
  api.ts               Axios instance
  services/            patient, appointment, prescription, admin API calls
  store/               Zustand stores (auth, queue, UI)
  hooks/useSocket.ts   Socket.IO connection and room joins
  validations/         Zod schemas
middleware.ts          role-based route protection
```

## License

[MIT](LICENSE) © Md. Rakib
