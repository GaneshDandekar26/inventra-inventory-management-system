# 🔧 Render Deployment Settings

## Backend Service Settings (Web Service)

### Basic Settings
```
Name: inventra-backend
Environment: Node
Region: Oregon (US West)
Plan: Free
Branch: main
Root Directory: backend
```

### Build & Deploy
```
Build Command: npm install
Start Command: node src/server.js
```

### Environment Variables
```
NODE_ENV = production
PORT = 5000
MONGODB_URI = mongodb+srv://username:password@cluster.mongodb.net/inventra
JWT_SECRET = (generate with: openssl rand -base64 32)
FRONTEND_URL = https://inventra-frontend.onrender.com
```

---

## Frontend Service Settings (Static Site)

### Basic Settings
```
Name: inventra-frontend
Environment: Static Site
Region: (not applicable for static sites)
Branch: main
Root Directory: (leave empty - blank)
```

### Build & Deploy
```
Build Command: npm install && npm run build
Publish Directory: dist
```

### Environment Variables
```
VITE_API_URL = https://inventra-backend.onrender.com/api
```

---

## Step-by-Step Configuration

### 1. Backend Web Service

**Step 1:** Go to https://dashboard.render.com
- Click **"New +"** button
- Select **"Web Service"**

**Step 2:** Connect Repository
- Click **"Connect GitHub"**
- Select your repository
- Click **"Connect"**

**Step 3:** Configure Service
```
Name: inventra-backend
Region: Oregon
Branch: main (or your main branch name)
Runtime: Node
Root Directory: backend
```

**Step 4:** Build Settings
```
Build Command: npm install
Start Command: node src/server.js
```

**Step 5:** Add Environment Variables
Click "Advanced" → "Add Environment Variable"

Add each variable:
1. **NODE_ENV**
   - Key: `NODE_ENV`
   - Value: `production`
   
2. **PORT**
   - Key: `PORT`
   - Value: `5000`
   
3. **MONGODB_URI**
   - Key: `MONGODB_URI`
   - Value: `mongodb+srv://your-username:your-password@cluster.mongodb.net/inventra`
   - *Get this from MongoDB Atlas*
   
4. **JWT_SECRET**
   - Key: `JWT_SECRET`
   - Value: *Generate using: `openssl rand -base64 32`*
   
5. **FRONTEND_URL**
   - Key: `FRONTEND_URL`
   - Value: `https://inventra-frontend.onrender.com`
   - *Update this after frontend deploys*

**Step 6:** Create Service
- Review settings
- Click **"Create Web Service"**
- Wait for deployment (3-5 minutes)
- Note the URL (e.g., `https://inventra-backend.onrender.com`)

---

### 2. Frontend Static Site

**Step 1:** Go to Render Dashboard
- Click **"New +"** button
- Select **"Static Site"**

**Step 2:** Connect Repository
- Select the same GitHub repository

**Step 3:** Configure Service
```
Name: inventra-frontend
Branch: main
Root Directory: (leave blank)
```

**Step 4:** Build Settings
```
Build Command: npm install && npm run build
Publish Directory: dist
```

**Step 5:** Add Environment Variable
- Scroll to "Environment" section
- Click **"Add Environment Variable"**
- Key: `VITE_API_URL`
- Value: `https://inventra-backend.onrender.com/api`
- *Replace with your actual backend URL*

**Step 6:** Create Site
- Click **"Create Static Site"**
- Wait for deployment (2-3 minutes)
- Note the URL (e.g., `https://inventra-frontend.onrender.com`)

---

### 3. Update Backend Environment Variable

After frontend is deployed:

**Step 1:** Go to Backend Service
- Click on `inventra-backend` service
- Click **"Environment"** tab

**Step 2:** Update FRONTEND_URL
- Find `FRONTEND_URL` variable
- Click **"Edit"**
- Value: `https://inventra-frontend.onrender.com`
- *Use your actual frontend URL*

**Step 3:** Save
- Scroll to bottom
- Click **"Save Changes"**
- Service will automatically redeploy

---

## Quick Setup Command

Generate JWT Secret:
```bash
openssl rand -base64 32
```

Test Backend Locally:
```bash
cd backend
npm install
node src/server.js
```

Build Frontend Locally:
```bash
npm install
npm run build
```

---

## Verification Steps

1. **Backend Health Check**
   - Visit: `https://inventra-backend.onrender.com/api/health`
   - Should return: `{"status":"ok","message":"Inventra API is running"}`

2. **Frontend Access**
   - Visit your frontend URL
   - Landing page should load

3. **Test Login/Signup**
   - Try creating a new account
   - Try logging in
   - Check browser console for errors

4. **Check Logs**
   - In Render dashboard
   - Click on service → "Logs" tab
   - Check for any errors

---

## Common Issues & Solutions

### Issue: Build Fails
**Solution:** Check logs for specific error
- Common: Missing dependencies → Add to package.json
- Common: Wrong Node version → Specify in .node-version

### Issue: CORS Error
**Solution:** 
- Verify `FRONTEND_URL` in backend matches exact frontend URL
- Check for trailing slashes
- Make sure protocol is `https://`

### Issue: Database Connection Failed
**Solution:**
- Check MongoDB Atlas network access (allow 0.0.0.0/0)
- Verify `MONGODB_URI` is correct
- Check credentials in connection string

### Issue: Frontend Shows API Errors
**Solution:**
- Verify `VITE_API_URL` includes `/api` at the end
- Check backend is running (visit health endpoint)
- Clear browser cache and hard refresh

---

## Free Tier Limitations

⚠️ **Important Notes:**
- Services spin down after 15 minutes of inactivity
- First request may take 30-60 seconds to wake up
- Limited bandwidth (~100GB/month)
- Auto-paused during free tier limits

**Recommendation:** Upgrade to paid plan for production use

---

## Next Steps After Deployment

1. ✅ Test all functionality
2. ✅ Update any hardcoded URLs
3. ✅ Set up custom domain (optional)
4. ✅ Enable monitoring/alerting
5. ✅ Set up database backups

---

## Support

If you encounter issues:
1. Check Render documentation: https://render.com/docs
2. Review logs in Render dashboard
3. Test locally first before deploying
4. Check MongoDB Atlas connection

