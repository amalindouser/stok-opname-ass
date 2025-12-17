# Database Migration Guide

## Current Setup
SQLite database di local development. **Tidak cocok untuk Vercel** (ephemeral filesystem).

## Recommended: Vercel Postgres

### Step 1: Setup Vercel Postgres
1. Buka https://vercel.com/dashboard
2. Pilih project mu
3. Go to **Storage** → **Create Database** → **Postgres**
4. Copy environment variables (URL akan di `.env.local`)

### Step 2: Update app.py untuk PostgreSQL
Ganti SQLite dengan PostgreSQL:

```python
import psycopg2
from psycopg2 import sql

# Get DB URL dari environment
DATABASE_URL = os.getenv('POSTGRES_URL')

def init_db():
    """Initialize PostgreSQL database"""
    conn = psycopg2.connect(DATABASE_URL)
    c = conn.cursor()
    
    c.execute('''CREATE TABLE IF NOT EXISTS so_sessions (
        id TEXT PRIMARY KEY,
        nama_area TEXT,
        created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
        updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
    )''')
    
    c.execute('''CREATE TABLE IF NOT EXISTS so_items (
        id SERIAL PRIMARY KEY,
        session_id TEXT,
        kode_barang TEXT,
        nama_barang TEXT,
        stok_real INTEGER,
        nama_area TEXT,
        created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
        FOREIGN KEY(session_id) REFERENCES so_sessions(id)
    )''')
    
    conn.commit()
    conn.close()
```

### Step 3: Update requirements.txt
```
psycopg2-binary==2.9.9
```

### Step 4: Push ke GitHub & Deploy ke Vercel
```bash
git add .
git commit -m "Add PostgreSQL support"
git push
```

Vercel akan auto-deploy dan gunakan environment variables.

## Alternative: Supabase (Free PostgreSQL)
1. https://supabase.com/dashboard
2. Create new project
3. Copy connection string ke `.env`
4. Same migration steps above

## For Now (Local Only)
Gunakan SQLite. Untuk production, migrate ke PostgreSQL.
