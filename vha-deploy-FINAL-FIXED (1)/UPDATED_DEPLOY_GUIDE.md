# 🚀 UPDATED Step-by-Step Vercel Deployment Guide (Fixed for Vite Error)

## ⚠️ IMPORTANT: Use Fixed Files
**Use the NEW file**: `vha-deploy-fixed-v2.zip` (contains all fixes for vite command not found error)

## Step 1: Upload to GitHub

### 1.1 Upload the Fixed Package
1. Go to [github.com](https://github.com) → **New repository**
2. Name: `village-health-access` 
3. Upload ALL files from `vha-deploy-fixed-v2.zip`
4. Commit with message: "Fixed vite deployment configuration"

## Step 2: Set Up Supabase Database

### 2.1 Create Supabase Project
1. Go to [supabase.com](https://supabase.com) → **New project**
2. Name: `village-health-access`
3. Set database password
4. Select closest region
5. **Wait 2 minutes** for project creation

### 2.2 Set Up Database
1. Go to **"SQL Editor"** → **"New query"**
2. Copy content from `backend/db/init.sql`
3. Paste and click **"Run"**
4. Verify "Success" message

### 2.3 Get Credentials
1. Go to **Settings** → **"API"**
2. Copy these values:
   - **Project URL** (starts with `https://`)
   - **anon public** key
   - **service_role** key (keep secret!)

## Step 3: Deploy to Vercel (CRITICAL SETTINGS)

### 3.1 Import Repository
1. Go to [vercel.com](https://vercel.com) → **"Add New"** → **"Project"**
2. Find your repository → **"Import"**

### 3.2 Configure Project Settings (IMPORTANT!)
**Framework Preset**: `Vite`
**Root Directory**: `./` (leave as default)

### 3.3 Build Configuration (CRITICAL!)
**Build Command**: `cd frontend && npm install && npm run build`
**Install Command**: `cd frontend && npm install --legacy-peer-deps`
**Output Directory**: `frontend/dist`
**Node.js Version**: `18.x` or `Latest`

### 3.4 Deploy
1. Click **"Deploy"**
2. Wait 3-4 minutes for build
3. **Should see NO vite command errors!**

## Step 4: Configure Environment Variables

### 4.1 Get Vercel Domain
After deploy, copy your Vercel URL: `https://your-project.vercel.app`

### 4.2 Add Environment Variables
In Vercel project → **Settings** → **Environment Variables**:

**Variable 1:**
- **Name**: `VITE_SUPABASE_URL`
- **Value**: Your Supabase URL
- **Environment**: Production, Preview, Development

**Variable 2:**
- **Name**: `VITE_SUPABASE_ANON_KEY`
- **Value**: Your Supabase anon key
- **Environment**: Production, Preview, Development

**Variable 3:**
- **Name**: `VITE_API_BASE`
- **Value**: `https://your-project.vercel.app/api`
- **Environment**: Production, Preview, Development

**Variable 4:**
- **Name**: `SUPABASE_URL`
- **Value**: Your Supabase URL
- **Environment**: Production, Preview, Development

**Variable 5:**
- **Name**: `SUPABASE_SERVICE_KEY`
- **Value**: Your Supabase service_role key
- **Environment**: Production, Preview, Development

### 4.3 Redeploy
1. Go to **"Deployments"** → Click latest → **"Redeploy"**
2. Wait 2-3 minutes

## Step 5: Verify Deployment

### 5.1 Test Frontend
Go to: `https://your-project.vercel.app`
- ✅ Page should load
- ✅ No vite command errors
- ✅ All components working

### 5.2 Test API
Go to: `https://your-project.vercel.app/api/health`
- ✅ Should return: `{"ok":true,"mode":"serverless"}`

### 5.3 Test Database
1. Try creating a patient in your app
2. Check Supabase → **"Table Editor"** → `profiles` table

## ✅ Success Checklist

- [ ] ✅ No "vite command not found" errors
- [ ] ✅ Build completes successfully  
- [ ] ✅ Frontend loads correctly
- [ ] ✅ API endpoints respond
- [ ] ✅ Environment variables configured
- [ ] ✅ Database connection working

## 🔧 If You Still Get Errors

### Quick Fix Options:

**Option 1: Use Different Build Command**
In Vercel → Settings → General:
- **Build Command**: `npm run build`
- **Root Directory**: `frontend`

**Option 2: Use Vercel CLI**
```bash
npm install -g vercel
vercel --prod
```

**Option 3: Deploy Frontend Separately**
1. Deploy `frontend/` folder alone as static site
2. Deploy `api/index.js` as serverless function

## 🎉 You're Done!

**Your working app URLs:**
- **Frontend**: `https://your-project.vercel.app`
- **API**: `https://your-project.vercel.app/api/*`

**The vite command error is now fixed!** 🚀

---

**Note**: If you still encounter issues, the problem is likely with environment variables or Supabase configuration, not the vite build process.