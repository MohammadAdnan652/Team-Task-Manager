# Developer Setup Guide

Complete guide to set up the Team Task Manager application locally.

## 📋 Prerequisites

### System Requirements
- **OS**: Windows, macOS, or Linux
- **Node.js**: v16 or higher (Check with `node --version`)
- **npm**: v8 or higher (Installed with Node.js)
- **Git**: Latest version
- **MongoDB**: Local instance or Atlas account

### Accounts Needed
- MongoDB Atlas (free tier available): https://mongodb.com/atlas
- GitHub (for version control)

---

## 🔧 Installation Steps

### Step 1: Clone/Extract Project

If you have the code locally:
```bash
cd "Team Task Manager"
```

---

### Step 2: MongoDB Setup

#### Option A: Local MongoDB (Recommended for Development)

**Windows:**
1. Download: https://www.mongodb.com/try/download/community
2. Run installer
3. Choose "Install as a Service"
4. MongoDB runs on `localhost:27017`

**macOS:**
```bash
brew tap mongodb/brew
brew install mongodb-community
brew services start mongodb-community
```

**Linux (Ubuntu):**
```bash
curl https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
sudo apt-get update
sudo apt-get install -y mongodb-org
sudo systemctl start mongod
```

#### Option B: MongoDB Atlas (Cloud)

1. Go to: https://www.mongodb.com/cloud/atlas
2. Create free account
3. Create cluster (free tier)
4. Click "Connect" → "Connect your application"
5. Copy connection string
6. Save for later (use as `MONGODB_URI`)

---

### Step 3: Backend Setup

```bash
# Navigate to backend
cd backend

# Install dependencies
npm install

# Create .env file
cp .env.example .env
```

Edit `.env`:
```env
PORT=5000
NODE_ENV=development
MONGODB_URI=mongodb://localhost:27017/team-task-manager
JWT_SECRET=mysecretkeyfor2024development
JWT_EXPIRE=7d
FRONTEND_URL=http://localhost:3000
```

**If using MongoDB Atlas**, replace `MONGODB_URI` with:
```
mongodb+srv://username:password@cluster0.xxxxx.mongodb.net/team-task-manager?retryWrites=true&w=majority
```

Start backend:
```bash
npm run dev
```

Expected output:
```
Server running on port 5000
MongoDB Connected: localhost
```

---

### Step 4: Frontend Setup (New Terminal)

```bash
# Navigate to frontend
cd frontend

# Install dependencies
npm install

# Create .env.local file
cp .env.example .env.local
```

Edit `.env.local`:
```env
VITE_API_URL=http://localhost:5000/api
```

Start frontend:
```bash
npm run dev
```

Expected output:
```
VITE v5.0.0  ready in XXX ms

➜  Local:   http://localhost:3000/
➜  press h to show help
```

---

## ✅ Testing the Setup

1. Open browser: http://localhost:3000
2. You should see login page
3. Click "Sign up"
4. Create account with:
   - Name: John Doe
   - Email: john@example.com
   - Password: password123
   - Confirm: password123
5. Click dashboard after login
6. Create a project
7. Add tasks to project

---

## 🔑 Environment Variables Explained

### Backend (.env)

| Variable | Purpose | Example |
|----------|---------|---------|
| PORT | Server port | 5000 |
| NODE_ENV | Environment | development/production |
| MONGODB_URI | Database connection | mongodb://localhost:27017/... |
| JWT_SECRET | Token signing key | random string |
| JWT_EXPIRE | Token expiry | 7d, 24h |
| FRONTEND_URL | Allowed origin for CORS | http://localhost:3000 |

### Frontend (.env.local)

| Variable | Purpose | Example |
|----------|---------|---------|
| VITE_API_URL | Backend API URL | http://localhost:5000/api |

---

## 📝 Common Commands

### Backend
```bash
# Development mode (with auto-reload)
npm run dev

# Production mode
npm run build
npm start

# Install new package
npm install package-name
```

### Frontend
```bash
# Development mode
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview

# Install new package
npm install package-name
```

---

## 🐛 Troubleshooting

### Port Already in Use

**Backend (Port 5000):**
```bash
# Find process using port
netstat -ano | findstr :5000  # Windows
lsof -i :5000                 # macOS/Linux

# Kill process
taskkill /PID <PID> /F        # Windows
kill -9 <PID>                 # macOS/Linux
```

**Frontend (Port 3000):**
```bash
# Same process as above, replace 5000 with 3000
```

### MongoDB Connection Error

**Error:** `connect ECONNREFUSED 127.0.0.1:27017`

**Solutions:**
1. Check MongoDB is running: `mongosh` or `mongo`
2. Verify connection string in .env
3. If using Atlas, check whitelist IP address
4. Ensure password is correct if using authentication

### CORS Error in Browser

**Error:** `Access to XMLHttpRequest blocked by CORS policy`

**Solutions:**
1. Check backend .env: `FRONTEND_URL=http://localhost:3000`
2. Ensure backend is running
3. Clear browser cache
4. Restart both servers

### 502 Bad Gateway

**Solutions:**
1. Check backend logs for errors
2. Verify database connection
3. Restart backend: Stop and run `npm run dev` again

### Module Not Found Error

```bash
# Clear node_modules and reinstall
rm -rf node_modules package-lock.json  # macOS/Linux
rmdir /s node_modules                  # Windows
npm install
```

### Token Expired

1. Clear localStorage in browser DevTools (F12 → Application)
2. Logout and login again
3. Or modify JWT_EXPIRE in backend .env

---

## 📚 Project Structure Quick Reference

```
backend/
├── src/
│   ├── controllers/      ← Business logic
│   ├── models/           ← Database schemas
│   ├── routes/           ← API endpoints
│   ├── middleware/       ← Auth & errors
│   ├── utils/            ← Helpers (JWT, validation)
│   └── server.js         ← Main file
├── package.json
├── .env                  ← Your config
└── .gitignore

frontend/
├── src/
│   ├── pages/            ← Full page components
│   ├── components/       ← Reusable components
│   ├── services/         ← API calls
│   ├── context/          ← Auth state
│   ├── App.jsx           ← Main app
│   └── index.css         ← Global styles
├── index.html            ← HTML template
├── package.json
└── vite.config.js        ← Build config
```

---

## 🚀 Development Workflow

1. **Create feature branch:**
   ```bash
   git checkout -b feature/new-feature
   ```

2. **Make changes in code editor**
   - Backend changes reload with nodemon
   - Frontend changes refresh automatically

3. **Test changes locally:**
   - Backend: Use Postman or curl
   - Frontend: Use browser DevTools

4. **Commit changes:**
   ```bash
   git add .
   git commit -m "Add new feature"
   git push origin feature/new-feature
   ```

5. **Create Pull Request on GitHub**

---

## 💡 Useful Tools

### API Testing
- **Postman**: https://www.postman.com/
- **Thunder Client**: VS Code extension
- **curl**: Command line

### Database Management
- **MongoDB Compass**: GUI for MongoDB
- **MongoDB Atlas UI**: Web interface

### Code Editor
- **VS Code**: https://code.visualstudio.com/
  - Recommended Extensions:
    - ES7+ React/Redux/React-Native snippets
    - MongoDB for VS Code
    - Thunder Client

---

## 🔒 Security Notes

- Never commit `.env` file
- Don't share JWT_SECRET
- Change default passwords
- Use strong MongoDB passwords
- Enable MongoDB IP whitelist (if Atlas)

---

## 📞 Getting Help

1. Check error logs in terminal
2. Review API.md for endpoint documentation
3. Check browser console (F12)
4. Review MongoDB logs: `mongosh` → db.logs.find()
5. Ask on GitHub Issues

---

## ✨ Next Steps

After successful setup:

1. ✅ Create test account
2. ✅ Create test project
3. ✅ Add tasks
4. ✅ Test all features
5. ✅ Explore codebase
6. ✅ Make code changes
7. ✅ Deploy to Railway

---

## 📋 Setup Checklist

- [ ] Node.js v16+ installed
- [ ] MongoDB installed/Atlas account
- [ ] Backend .env configured
- [ ] Frontend .env configured
- [ ] `npm install` completed (both)
- [ ] Backend running on port 5000
- [ ] Frontend running on port 3000
- [ ] Can access http://localhost:3000
- [ ] Can create account and login
- [ ] Can create projects and tasks

---

**Happy Coding! 🎉**

Need help? Check the README.md or DEPLOYMENT.md files.
