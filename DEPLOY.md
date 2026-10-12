# Paint Stock Manager - Deployment Guide

## Option 1: Run on your own computer (no internet needed after setup)

### Requirements
- Docker Desktop installed: https://www.docker.com/products/docker-desktop

### Steps
1. Open a terminal in this project folder.
2. Run:
   ```bash
   docker compose up --build
   ```
3. Wait for it to finish.
4. Open your browser to: http://localhost:3000

The app and database will keep running until you stop Docker. Your data is saved even if you restart the computer.

---

## Option 2: Deploy to Render.com (no GitHub needed)

### Steps
1. Go to https://render.com and sign up.
2. Click **New** → **Web Service**.
3. Choose **Deploy from existing image** OR **Deploy existing image**.
4. Upload this project folder as a ZIP, or use the Dockerfile path.
5. Add environment variable:
   - `DATABASE_URL` = your database connection string
6. Click **Deploy**.

### Database on Render
1. Click **New** → **PostgreSQL**.
2. Create a free PostgreSQL database.
3. Copy the **Internal Database URL**.
4. Paste it as `DATABASE_URL` in your Web Service settings.

---

## Option 3: Deploy to Railway.app (no GitHub needed)

### Steps
1. Go to https://railway.app and sign up.
2. Click **New Project**.
3. Choose **Deploy from Local** or **Upload**.
4. Upload this project folder as a ZIP file.
5. Railway will detect the Dockerfile automatically.
6. Add a PostgreSQL database:
   - Click **New** → **Database** → **Add PostgreSQL**
7. Railway will automatically connect the database and set `DATABASE_URL`.

---

## Option 4: Deploy to Fly.io

### Requirements
- Fly.io CLI installed: https://fly.io/docs/hands-on/install-flyctl/

### Steps
1. Run in terminal:
   ```bash
   fly launch
   ```
2. Follow the prompts.
3. Add a PostgreSQL database:
   ```bash
   fly postgres create
   ```
4. Attach the database to your app:
   ```bash
   fly postgres attach --app your-app-name
   ```
5. Deploy:
   ```bash
   fly deploy
   ```

---

## Environment Variables

Only one variable is required:

```
DATABASE_URL=postgresql://username:password@host:port/database
```

---

## Important Notes

- The app automatically creates tables and seeds the 20 paint products on first run.
- Keep your `DATABASE_URL` secret. Do not share it.
- The PDF download feature uses a headless browser (Chromium) on the server. It works on most cloud platforms, but very small free tiers may have memory limits.

---

## Quick Test After Deploy

1. Open the deployed URL.
2. Add stock quantities for a paint product.
3. Click **Save**.
4. Click **Download PDF**.
5. If the PDF downloads, everything is working.
