# Deploy to Vercel from Your Phone

## Quick note
Vercel needs your code to be in a Git repository (GitHub, GitLab, or Bitbucket) before it can deploy. On mobile, the easiest way is to use GitHub's website.

---

## Option 1: Using GitHub Mobile Website (works on any phone)

### Step 1: Create a GitHub account
1. Open your phone browser.
2. Go to https://github.com/signup.
3. Sign up with email, Google, or phone.

### Step 2: Create a new repository
1. Go to https://github.com/new.
2. Repository name: `paint-stock-manager`.
3. Make it **Public**.
4. Click **Create repository**.

### Step 3: Upload your project files
1. In your new repo, click **"uploading an existing file"** link.
2. You need to upload these files/folders:
   - `.env` (without DATABASE_URL value, or leave it empty)
   - `.env.example`
   - `docker-compose.yml`
   - `drizzle.config.json`
   - `eslint.config.mjs`
   - `next.config.ts`
   - `package.json`
   - `postcss.config.mjs`
   - `tsconfig.json`
   - `vercel.json`
   - `src/` folder (all files inside)
3. Click **Commit changes**.

> Note: Uploading many files on mobile is slow. If possible, ask someone with a computer to help, or use Option 2 below.

### Step 4: Create a database
1. Go to https://neon.tech on your phone.
2. Sign up and create a free PostgreSQL database.
3. Copy the connection string.

### Step 5: Deploy on Vercel
1. Go to https://vercel.com/new on your phone.
2. Sign up with the same GitHub account.
3. Select your `paint-stock-manager` repo.
4. In the settings, add environment variable:
   - Name: `DATABASE_URL`
   - Value: your Neon connection string
5. Click **Deploy**.

### Step 6: Seed the database
1. After Vercel gives you a URL (like `https://paint-stock-manager.vercel.app`).
2. Open `https://your-url.vercel.app/api/seed` in your phone browser.
3. Wait for "Products seeded successfully" message.

---

## Option 2: Using Termux on Android (faster)

If you are on Android, you can use Termux to deploy directly without uploading files one by one.

1. Install **Termux** from F-Droid or Play Store.
2. Open Termux and run:
   ```bash
   pkg install nodejs git
   npm install -g vercel
   ```
3. If you have the project files on your phone, navigate to the folder:
   ```bash
   cd /path/to/paint-stock-manager
   ```
4. Run:
   ```bash
   vercel
   ```
5. Login to Vercel and follow the prompts.
6. Add your database URL:
   ```bash
   vercel env add DATABASE_URL
   ```
7. Deploy again:
   ```bash
   vercel --prod
   ```
8. Seed the database by visiting `/api/seed`.

---

## Option 3: Easier alternative for mobile — Railway

If Vercel is too complicated on your phone, **Railway.app** is easier:

1. Go to https://railway.app on your phone.
2. Sign up.
3. Create new project → choose **Upload**.
4. Upload your project ZIP file.
5. Add a PostgreSQL database with one click.
6. Railway will automatically set everything up.

---

## Need help?

If you can use a computer even for 10 minutes, deployment will be much faster. Otherwise, Option 1 with GitHub mobile website will work but takes longer.
