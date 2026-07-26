# Stellar Insights

**Real-time payment analytics for Stellar.**

A lean, production-grade stack for measuring and improving cross-border payment reliability.

- Backend: Rust analytics engine
- Frontend: Next.js dashboard
- Contracts: Soroban smart contracts (optional)
- DB: SQLite (WAL mode) — see [Database](#database) below

## 🔧 Quick start

No database server to install — SQLite runs in-process and the file is created
on first start.

1. Run backend

```bash
cd backend
cp .env.example .env
# DATABASE_URL already defaults to sqlite:./stellar_insights.db
# set STELLAR_RPC_URL etc. as needed
cargo run
```

2. Run frontend

```bash
cd frontend
npm install
npm run dev
```

## Database

**SQLite only.** This is a compile-time property, not a configuration one:
`sqlx` is built with only the `sqlite` feature, `backend/src/database.rs` uses
`SqlitePool`/`SqliteConnectOptions` directly, and every migration is written in
SQLite-flavoured SQL.

Setting a `postgresql://` `DATABASE_URL` does **not** switch databases — it
fails to parse as `SqliteConnectOptions` and the backend refuses to start.
Adding Postgres support is a code change. Whether to make it is being tracked
in issue #1876.

## 🧪 Local safety checks (already built)

- `scripts/check_folder_size.sh` (fails if any folder >200MB)
- [`.github/workflows/enforce-folder-size.yml`](.github/workflows/enforce-folder-size.yml)

## 📁 Structure

- `backend/` Rust services
- `frontend/` Next.js dashboard
- `mobile/` React Native mobile app — [current status](mobile/README.md#current-status)
- `contracts/` Soroban contracts
- `docs/` additional docs

## 📌 Notes

- History has been cleaned to reduce clone size.
- Use `git lfs` for large binaries.
- For full operational details, see `docs/` and module READMEs.
