# Aarogya360

A full-stack patient lifecycle platform that brings care teams, patients, and families into one connected workflow. Aarogya360 combines clinical timelines, care coordination, document intelligence, and role-based portals in a single application.

## What it does

- **Follow the patient journey:** manage lifecycle stages, transitions, clinical events, tasks, and alerts.
- **Coordinate care:** track orders, medications, referrals, prior authorizations, and care team work.
- **Give each role a focused view:** portals for admins, doctors, specialists, patients, and family members.
- **Work with medical documents:** upload reports, run OCR, extract metadata, and use AI-assisted summaries and questions.
- **Keep families informed:** consent-based access, questions, messages, and notifications.

## Tech stack

| Layer | Technology |
| --- | --- |
| Frontend | React, TypeScript, Vite, Tailwind CSS, shadcn/ui |
| API | NestJS, TypeScript, JWT authentication |
| Data | PostgreSQL, Prisma ORM |
| Supporting services | Redis, Tesseract.js OCR, configurable LLM endpoint |

## Repository layout

```text
backend/       NestJS API, Prisma schema and migrations, tests
landing_page/  Marketing site and role-based portal
api_docs/      API reference
documentation/  Architecture and deployment guides
```

## Run locally

You need Node.js 20+, npm 10+, and Docker Compose. The included Compose file starts PostgreSQL, Redis, and pgAdmin. Its database credentials are for local development only.

```bash
cd backend
docker compose up -d
npm install
```

Create `backend/.env` with the minimum local settings:

```env
DATABASE_URL=postgresql://postgres:password@localhost:5432/medlifecycle
PORT=3100
JWT_SECRET=replace-with-a-long-random-secret
CORS_ALLOWED_ORIGINS=http://localhost:8080
```

Apply the database migrations and start the API:

```bash
npx prisma migrate deploy
npm run start:dev
```

In another terminal, start the frontend:

```bash
cd landing_page
npm install
npm run dev
```

Open [http://localhost:8080](http://localhost:8080). The frontend proxies `/api` to `http://localhost:3100` by default. The API is available at [http://localhost:3100/api](http://localhost:3100/api). AI and document processing features may need additional configuration; see the [backend setup guide](backend/README.md) and [frontend setup guide](landing_page/README.md).

## Checks

```bash
cd backend && npm run build && npm test -- --runInBand
cd ../landing_page && npm run build && npm test
```

## Documentation

- [Backend setup and configuration](backend/README.md)
- [Frontend setup and portal routes](landing_page/README.md)
- [API documentation](api_docs/api_documentation.txt)
- [Deployment guides](documentation/)

## Security note

This project processes sensitive health information. Use strong secrets, appropriate access controls, encrypted storage, and a privacy review before handling real patient data. Do not commit `.env` files or patient records.
