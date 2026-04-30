# Quick Reference Guide

## 🚀 Quick Start (30 seconds)

```bash
# Terminal 1 - Backend
cd backend
npm install
cp .env.example .env
npm run dev

# Terminal 2 - Frontend (new terminal window)
cd frontend
npm install
npm run dev
```

Then open http://localhost:3000

---

## 📍 Important URLs

- **Frontend**: http://localhost:3000
- **Backend API**: http://localhost:5000/api
- **MongoDB Local**: localhost:27017

---

## 👤 Test User Credentials (After Signup)

- Email: test@example.com
- Password: password123

---

## 🔨 Common Tasks

### Create Admin User
1. Sign up normally
2. Manually update role in MongoDB:
   ```javascript
   db.users.updateOne({email:"admin@example.com"},{$set:{role:"admin"}})
   ```

### Reset Database
```bash
# Connect to MongoDB
mongosh
# Use database
use team-task-manager
# Clear collections
db.users.deleteMany({})
db.projects.deleteMany({})
db.tasks.deleteMany({})
```

### View Database
```bash
mongosh
use team-task-manager
db.users.find()
db.projects.find()
db.tasks.find()
```

---

## 📂 Key Files to Edit

### Backend
- `backend/src/server.js` - Main server file
- `backend/.env` - Configuration
- `backend/src/server.js` - Add new routes here

### Frontend
- `frontend/src/App.jsx` - Main app structure
- `frontend/src/pages/` - Add new pages
- `frontend/src/services/api.js` - API client

---

## 🧪 Test API Endpoints

### Signup
```bash
curl -X POST http://localhost:5000/api/auth/signup \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Test User",
    "email": "test@example.com",
    "password": "password123",
    "confirmPassword": "password123"
  }'
```

### Login
```bash
curl -X POST http://localhost:5000/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "test@example.com",
    "password": "password123"
  }'
```

Copy the token from response, then:

### Get Projects (with token)
```bash
curl -X GET http://localhost:5000/api/projects \
  -H "Authorization: Bearer YOUR_TOKEN"
```

---

## 🐛 Debug Tips

### View Logs
- Backend logs: Check terminal where you ran `npm run dev`
- Frontend logs: Open DevTools (F12 → Console)
- Database logs: Run `mongosh` and check collections

### Common Issues & Fixes

| Issue | Solution |
|-------|----------|
| Port 5000 in use | Change PORT in .env or kill process |
| MongoDB error | Start MongoDB service |
| CORS error | Check FRONTEND_URL in backend .env |
| Token invalid | Clear localStorage, login again |
| Can't connect to DB | Verify MONGODB_URI in .env |

---

## 📦 Installing Packages

### Backend
```bash
cd backend
npm install package-name
```

### Frontend
```bash
cd frontend
npm install package-name
```

---

## 🔄 Workflow

1. Edit code
2. Save file (auto-reload in browsers)
3. Test in browser
4. Check console for errors
5. Fix and repeat

---

## 📝 Directory Tree

```
Team Task Manager/
├── backend/
│   ├── src/server.js          ← Start here
│   ├── .env                   ← Configure this
│   └── package.json
├── frontend/
│   ├── src/App.jsx            ← Start here
│   └── package.json
└── README.md
```

---

## 🎯 Most Used Commands

Backend:
```bash
npm run dev        # Start development
npm install        # Install dependencies
npm start          # Production start
```

Frontend:
```bash
npm run dev        # Start development
npm install        # Install dependencies
npm run build      # Build production
npm run preview    # Preview build
```

---

## 💾 Saving Files

Both backend and frontend have file watchers:
- **Backend**: nodemon reloads automatically
- **Frontend**: Vite refreshes automatically

Just save and F5 to refresh!

---

## 🚨 If Something Breaks

1. **Check terminal errors** - Read the error message
2. **Restart servers** - Ctrl+C and `npm run dev`
3. **Clear cache** - Delete node_modules, run `npm install`
4. **Check .env** - All variables set?
5. **Verify connections** - Is MongoDB running?

---

## ✅ Deployment Preview

When ready to deploy:

```bash
# Build frontend
cd frontend
npm run build
# Creates dist/ folder

# Ready backend
cd backend
# Already production-ready
```

Then follow DEPLOYMENT.md

---

## 📞 Need Help?

1. Check README.md (overview)
2. Check SETUP.md (detailed setup)
3. Check API.md (endpoints)
4. Check logs in terminal
5. Check browser DevTools

---

**Last Updated: January 2024**
**Version: 1.0.0**
