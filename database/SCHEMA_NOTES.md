# Authentication Schema Initialization

This database container has been provisioned with a minimal `users` table and a seeded test user.

## Connection Information

Preferred environment variable:
- DATABASE_URL

If not set, you can read the helper file for the exact connection:
- Path: database/db_connection.txt
- Current content example:
  psql postgresql://appuser:dbuser123@localhost:5000/myapp

Note: The preview may expose the database on port 5001, while some scripts reference 5000. The db_connection.txt is the authoritative local connection helper. For the backend, standardize by setting:
- DATABASE_URL=postgresql://appuser:dbuser123@localhost:5000/myapp

## Schema

Created with:
CREATE TABLE IF NOT EXISTS users (
  id SERIAL PRIMARY KEY,
  username VARCHAR(255) UNIQUE NOT NULL,
  password_hash VARCHAR(255) NOT NULL,
  created_at TIMESTAMPTZ DEFAULT NOW(),
  updated_at TIMESTAMPTZ DEFAULT NOW()
);

## Seeded User

Inserted:
- username: testuser
- password: testpass
- password_hash: bcrypt

A valid bcrypt hash for "testpass" was used and inserted.

## Backend Usage

Configure your FastAPI app (SQLAlchemy/psycopg) to read:
- First: DATABASE_URL (recommended)
- Fallback: Read and parse database/db_connection.txt and extract the `postgresql://...` URI.

Example:
postgresql://appuser:dbuser123@localhost:5000/myapp

## Operations Method

Per project rules:
- SQL executed using psql -c "..." one statement at a time.
- No .sql files were created.
