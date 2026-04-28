# Netlify Deployment Guide

## Changes Made for Netlify Deployment

### Frontend Configuration Files Created:

1. **.env.production** - Production environment variables
   - `VITE_API_URL=https://wmtlabtest-production-fbfe.up.railway.app/api`
   - This tells the frontend to use your Railway backend in production

2. **netlify.toml** - Netlify configuration file
   - Build command: `npm run build`
   - Publish directory: `dist`
   - Redirect rules for SPA routing (all routes redirect to index.html)

### Backend Updates:

- Enhanced CORS configuration in `backend/server.js` to accept requests from:
  - Local development (http://localhost:5173, http://localhost:5174)
  - Netlify production (https://wmtlabtest.netlify.app)

### API Configuration:

The frontend `src/api/itemApi.js` already uses environment variables:
- Development: Uses local backend (http://localhost:5000/api)
- Production: Uses Railway backend (https://wmtlabtest-production-fbfe.up.railway.app/api)

---

## Deployment Steps to Netlify

### Prerequisites:
1. GitHub account with your repository pushed
2. Netlify account (sign up at netlify.com)

### Step-by-Step Deployment:

1. **Push your changes to GitHub:**
   ```bash
   git add .
   git commit -m "Add Netlify deployment configuration and update CORS"
   git push origin main
   ```

2. **Deploy to Netlify:**
   - Go to [netlify.com](https://netlify.com)
   - Click "Add new site" → "Import an existing project"
   - Select GitHub and authorize Netlify
   - Choose your repository (WMT_Lab_Test)
   - Basic build settings will auto-detect:
     - Build command: `npm run build`
     - Publish directory: `dist`
   - Click "Deploy site"

3. **Configure Custom Domain (Optional):**
   - In Netlify dashboard, go to Site settings → Domain management
   - Add your custom domain or use the provided netlify.app domain

### Environment Variables in Netlify (if needed):

If you want to use different API URLs, set in Netlify:
1. Go to Site settings → Build & deploy → Environment
2. Add `VITE_API_URL` variable (optional, .env.production handles this)

---

## Testing the Deployment

### Local Testing:
```bash
# Test production build locally
cd frontend
npm run build
npm run preview
```

### After Deployment:
1. Visit your Netlify URL
2. Test Add Item functionality
3. Test viewing items with Model Number
4. Test Edit and Delete operations
5. Verify all requests go to your Railway backend

---

## Troubleshooting

### CORS Errors:
- Check that your Netlify domain is in the `allowedOrigins` in `backend/server.js`
- If you have a custom domain, add it to the CORS configuration

### API Connection Issues:
- Verify Railway backend is running: Visit https://wmtlabtest-production-fbfe.up.railway.app/
- Check network tab in browser DevTools to see actual API calls
- Ensure MongoDB Atlas IP whitelist includes Railway's IP

### Build Failures:
- Check Netlify build logs in the deploy section
- Ensure all dependencies are in package.json
- Run `npm install` and `npm run build` locally to test

---

## After Deployment URL:
Once deployed, your frontend will be available at:
- **Netlify Default URL:** https://wmtlabtest.netlify.app (or similar)
- **Your Railway Backend:** https://wmtlabtest-production-fbfe.up.railway.app
