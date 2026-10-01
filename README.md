# Nichewick Founder Match (MVP)

Token-based founder matching module for the Nichewick growth ecosystem.

## Stack

- Next.js (App Router) + TypeScript
- Tailwind CSS v4
- Prisma + SQLite (swap `DATABASE_URL` for PostgreSQL in production)
- Auth.js (NextAuth v5) credentials auth

## Setup

```bash
npm install
npm run db:push
npm run db:seed
npm run dev
```

Open [http://localhost:3000](http://localhost:3000).

### Demo accounts

| Role | Email | Password |
|------|-------|----------|
| Admin | admin@nichewick.com | password123 |
| Founder | alex@startup.io | password123 |
| Founder | priya@build.co | password123 |
| Founder | jordan@health.app | password123 |

## Routes

- `/founders` — dashboard
- `/founders/profile` — founder profile
- `/founders/matches` — compatibility matches
- `/founders/connections` — requests & chat
- `/founders/tokens` — wallet & ledger
- `/founders/settings` — account & referral code
- `/admin` — token costs, packages, overview (admin only)

## Token ledger

All balance changes go through `applyTokenTransaction()` in `src/lib/tokens.ts` with optional idempotency keys.

## Razorpay (India, under ₹200)

Token packs are sold via **Razorpay Checkout** (UPI, cards, netbanking, wallets). Tokens are credited only after server-side signature verification.

1. Add keys to `.env` (see `.env.example`).
2. Reseed packages: `npm run db:seed` (3 tokens ₹9 · 10 tokens ₹19 · 25 tokens ₹30).
3. Open `/founders/tokens` → **Pay with Razorpay**.

Test cards: [Razorpay test docs](https://razorpay.com/docs/payments/payments/test-card-details/).

## Matching

Weighted scoring in `src/lib/matching.ts` (industry 25%, needs/offer 25%, stage 15%, skills 15%, goals 10%, location 5%, other 5%).
