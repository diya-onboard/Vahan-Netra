# Village Health Access - Deployment Notes

## Deployment Status

### ✅ Frontend Deployment (Fully Supported)
- **Technology**: React + Vite + Tailwind
- **Deploy Status**: ✅ Will deploy successfully on Vercel
- **Features**: All features will work including offline support, i18n, and Supabase integration

### ⚠️ Backend Deployment (Limited Features)
- **Original Backend**: Node.js + Express + Socket.io + Twilio
- **Serverless Limitation**: Socket.io and persistent connections not supported on Vercel serverless
- **Vercel-compatible Version**: Created `vercel-api.js` with core API functionality
- **Features Available**: ✅ CRUD operations, Supabase integration
- **Features NOT Available**: ❌ Real-time Socket.io, Twilio SMS notifications

## Required Environment Variables

### For Successful Deployment:
```
SUPABASE_URL=your_supabase_project_url
SUPABASE_SERVICE_KEY=your_supabase_service_key
```

### Optional (for enhanced features):
```
VITE_SUPABASE_URL=your_supabase_project_url
VITE_SUPABASE_ANON_KEY=your_supabase_anon_key
VITE_API_BASE=https://your-vercel-domain.vercel.app/api
```

## Deployment Commands

The deployment will be attempted with:
```bash
# Frontend deploy
cd frontend && npm install && npm run build

# Backend deploy (serverless API routes)
```

## Database Setup

Before deploying, ensure you have:
1. Created a Supabase project
2. Run the SQL from `backend/db/init.sql` in your Supabase SQL editor
3. Set up your environment variables

## Alternative Backend Solutions

If you need the full backend with Socket.io and Twilio features, consider:
- Railway (supports persistent Node.js servers)
- Heroku (supports full-stack applications)
- DigitalOcean App Platform
- AWS ECS/EKS
- Google Cloud Run

## Quick Fix After Deploy

After frontend deployment, update the API base URL in your frontend code to point to the deployed backend endpoints.