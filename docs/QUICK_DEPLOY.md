# Quick Deployment Steps - Choose Your Path

## ⚡ **Fastest Path (15 minutes)**

### Step 1: Deploy Backend to Heroku

```bash
# 1. Login to Heroku
heroku login

# 2. Go to backend folder
cd backend

# 3. Create Heroku app
heroku create bondiour-collections-api

# 4. Create Procfile
echo "web: node index.js" > Procfile

# 5. Set environment variables
heroku config:set MONGODB_URI="mongodb+srv://user:pass@cluster.mongodb.net/bondiour"
heroku config:set JWT_SECRET="your-super-secret-key-12345"
heroku config:set STRIPE_SECRET_KEY="sk_test_xxxx"
heroku config:set NODE_ENV="production"
heroku config:set PORT="5000"

# 6. Deploy
git push heroku main

# 7. View live API
heroku open
# Your API is now at: https://bondiour-collections-api.herokuapp.com/api
```

---

### Step 2: Deploy Frontend to Vercel

```bash
# 1. Go to vercel.com and sign in with GitHub

# 2. Click "New Project"

# 3. Import your GitHub repository

# 4. Select "frontend" as root directory

# 5. Add environment variable:
#    REACT_APP_API_URL = https://bondiour-collections-api.herokuapp.com/api

# 6. Click Deploy

# Your frontend is now at: https://your-project-name.vercel.app
```

---

### Step 3: Setup MongoDB Atlas (Database)

```bash
# 1. Go to mongodb.com/cloud/atlas

# 2. Create free account

# 3. Click "Create a Deployment" → Choose Free Tier

# 4. Create username and password

# 5. Click "Connect" → "Drivers" → Copy connection string

# 6. Replace in connection string:
mongodb+srv://USERNAME:PASSWORD@cluster0.xxxxx.mongodb.net/bondiour-collections?retryWrites=true&w=majority

# 7. Add to Heroku:
heroku config:set MONGODB_URI="your-full-connection-string"

# 8. In MongoDB Atlas, go to "Network Access"
# 9. Add your Heroku IP (or 0.0.0.0/0 for testing)
```

---

## ✅ **Verification**

### Test Backend
```bash
curl https://bondiour-collections-api.herokuapp.com/api/health
# Should return: {"status":"ok","message":"API is running",...}
```

### Test Frontend
```
Visit: https://your-project.vercel.app
Should load without errors
```

---

## 🔧 **Setup Custom Domain (Optional)**

### Connect Domain to Frontend (Vercel)

1. Buy domain from GoDaddy/Namecheap
2. Go to Vercel Dashboard
3. Select your project → Settings → Domains
4. Add your domain
5. Copy nameservers Vercel provides
6. Go to domain registrar
7. Update nameservers
8. Wait 24 hours for DNS propagation

---

## 🚀 **Alternative: One-Click Deploy (Even Easier!)**

### Deploy to Railway.app (Recommended!)

```bash
# 1. Go to railway.app

# 2. Click "New Project"

# 3. Click "Deploy from GitHub Repo"

# 4. Select your Bondiour-collections repo

# 5. Railway auto-detects and deploys both frontend and backend

# 6. Add environment variables in Railway dashboard

# 7. Add MongoDB database service from Railway marketplace

# That's it! Everything is deployed and connected!
```

---

## 📊 **Cost Comparison**

| Method | Backend | Frontend | Database | Total/Month |
|--------|---------|----------|----------|-------------|
| **Heroku + Vercel + Atlas** | Free* | Free | Free | $0-15 |
| **Railway.app** | Free | Free | $7 | $7 |
| **DigitalOcean** | $5 | $5 | $5 | $15 |
| **AWS** | $5-20 | $0 | $0-15 | $5-35 |

*Heroku free tier has limitations. Upgrade to $7/month for production.

---

## 🆘 **Common Issues & Solutions**

### Issue: "Cannot find module"
```bash
# Solution:
cd backend
npm install
heroku config:set NODE_ENV="production"
git push heroku main
```

### Issue: "Connection refused" to MongoDB
```bash
# Solution:
# 1. Check MongoDB Atlas connection string
# 2. Verify IP whitelist (0.0.0.0/0)
# 3. Verify username/password match
heroku config:set MONGODB_URI="new-connection-string"
```

### Issue: Frontend can't reach API
```bash
# Solution:
# 1. Check REACT_APP_API_URL in Vercel
# 2. Ensure it's the full URL: https://xxx.herokuapp.com/api
# 3. Check CORS on backend
# Redeploy frontend
```

### Issue: Stripe errors
```bash
# Solution:
# 1. Use test keys first (sk_test_)
# 2. Verify keys are set:
heroku config | grep STRIPE
# 3. Restart app:
heroku restart
```

---

## 📱 **Environment Variables Needed**

### For Backend (.env)
```
NODE_ENV=production
PORT=5000
MONGODB_URI=mongodb+srv://user:pass@cluster.mongodb.net/bondiour
JWT_SECRET=your-long-secret-key-minimum-32-characters
STRIPE_SECRET_KEY=sk_live_xxxxx
FRONTEND_URL=https://your-frontend-url.vercel.app
```

### For Frontend (.env.local / Vercel)
```
REACT_APP_API_URL=https://your-backend.herokuapp.com/api
```

---

## 🎯 **Next Steps After Deployment**

1. **Test All Features**
   - Create account
   - Browse products
   - Add to cart
   - Complete checkout
   - Check admin dashboard

2. **Setup Monitoring**
   ```bash
   # Heroku logs
   heroku logs --tail
   
   # MongoDB Atlas monitoring
   # Dashboard → Monitoring
   ```

3. **Enable SSL/HTTPS**
   - Vercel: ✅ Automatic
   - Heroku: ✅ Automatic
   - Custom domain: Use Let's Encrypt

4. **Configure Stripe**
   - Get production keys
   - Switch from test mode
   - Enable webhook notifications

5. **Setup Email Notifications**
   - Add SendGrid API key
   - Configure transactional emails

---

## 📞 **Support Contacts**

| Issue | Help |
|-------|------|
| **Heroku** | heroku.com/support |
| **Vercel** | vercel.com/support |
| **MongoDB** | mongodb.com/support |
| **Stripe** | stripe.com/support |

---

## ✨ **You're Live!**

Congratulations! Your website is now deployed! 🎉

- 🌐 Frontend: `https://your-domain.vercel.app`
- 🔌 Backend API: `https://your-api.herokuapp.com/api`
- 📊 Database: `MongoDB Atlas`
- 💳 Payments: `Stripe`

**Share your link and start selling! 🚀**
