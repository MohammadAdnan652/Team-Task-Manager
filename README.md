# Team Task Manager

Team Task Manager is a full-stack web application designed to help teams manage their projects and tasks efficiently. In this system, users can create projects, assign tasks to team members, and track the progress of each task. The application includes a secure authentication system using JWT, where users can sign up and log in safely. It also has role-based access control, where admins can manage projects and tasks, while members can only view and update their assigned work. Each task has a status like To Do, In Progress, and Completed, which helps in tracking progress. Additionally, the dashboard provides an overview of total, completed, pending, and overdue tasks. This project is built using React for the frontend, Node.js and Express for the backend, and MongoDB as the database. Overall, it demonstrates a real-world team collaboration system with proper structure, security, and scalability.

<img width="807" height="404" alt="image" src="https://github.com/user-attachments/assets/9ed9d632-e82f-4bb7-8dc7-d98675a532b6" />    


<img width="1918" height="757" alt="image" src="https://github.com/user-attachments/assets/482a8696-50d0-4b91-b6dd-57544248893a" />



## Tech Stack

- Backend: Node.js, Express, MongoDB (Mongoose), JWT, bcrypt, Joi
- Frontend: React (hooks), React Router, Axios, Tailwind CSS, Vite
- Deployment: Railway (backend and frontend as separate services)

## Project Structure

```text
Team Task Manager/
  backend/
    src/
      config/
      controllers/
      middleware/
      models/
      routes/
      utils/
      server.js
  frontend/
    src/
      components/
      context/
      pages/
      services/
      App.jsx
      main.jsx
```

## Features

- Authentication: signup/login, bcrypt password hashing, JWT auth
- Roles: `admin` and `member`
- Projects:
  - Admin can create, update, delete
  - Members can only view assigned projects
- Tasks:
  - Create tasks within projects
  - Assign to users
  - Status workflow: `To Do` -> `In Progress` -> `Completed`
  - Update allowed only for admin or assigned user
- Dashboard:
  - Total, completed, pending, overdue counts
  - Filter by project and assigned user (admin)

## Backend Setup

1. Open `backend`:
   - `cd backend`
2. Install dependencies:
   - `npm install`
3. Create `.env` from `.env.example`:
   - `PORT=5000`
   - `MONGODB_URI=<your-mongodb-uri>`
   - `JWT_SECRET=<strong-secret>`
   - `JWT_EXPIRE=7d`
   - `FRONTEND_URL=http://localhost:3000`
4. Run:
   - Dev: `npm run dev`
   - Prod: `npm start`

## Frontend Setup

1. Open `frontend`:
   - `cd frontend`
2. Install dependencies:
   - `npm install`
3. Create `.env` from `.env.example`:
   - `VITE_API_URL=http://localhost:5000/api`
4. Run:
   - Dev: `npm run dev`
   - Build: `npm run build`
   - Preview: `npm run preview`

## API Endpoints

### Auth
- `POST /api/auth/signup`
- `POST /api/auth/login`
- `GET /api/auth/me` (private)

### Users
- `GET /api/users` (admin only)

### Projects
- `POST /api/projects` (admin)
- `GET /api/projects` (private)
- `GET /api/projects/:id` (private, assigned only)
- `PUT /api/projects/:id` (admin)
- `DELETE /api/projects/:id` (admin)

### Tasks
- `POST /api/projects/:projectId/tasks`
- `GET /api/projects/:projectId/tasks`
- `GET /api/projects/:projectId/tasks/:taskId`
- `PUT /api/projects/:projectId/tasks/:taskId`
- `DELETE /api/projects/:projectId/tasks/:taskId`

### Dashboard
- `GET /api/dashboard/stats`
  - Optional query params: `projectId`, `userId`

## Railway Deployment

1. Push project to GitHub.
2. Create two Railway services:
   - Backend service from `backend` folder
   - Frontend service from `frontend` folder
3. Backend environment variables:
   - `PORT=5000`
   - `MONGODB_URI`
   - `JWT_SECRET`
   - `JWT_EXPIRE=7d`
   - `FRONTEND_URL=<frontend-railway-url>`
4. Frontend environment variables:
   - `VITE_API_URL=<backend-railway-url>/api`
5. Deploy both services and verify:
   - Frontend can authenticate and call backend APIs
   - CORS is restricted to frontend URL

## Deployment Link

- Add your live URL here after Railway deploy:
  - Frontend: `https://<your-frontend>.up.railway.app`
  - Backend: `https://<your-backend>.up.railway.app/api/health`
# Team Task Manager

A production-ready full-stack web application for managing team projects and tasks with role-based access control.

## 🌟 Features

- **Authentication & Authorization**
  - User signup & login with JWT
  - Role-based access (Admin & Member)
  - Secure password hashing with bcrypt

- **Project Management**
  - Admins can create, update, and delete projects
  - Assign team members to projects
  - Project overview with member list

- **Task Management**
  - Create tasks within projects
  - Assign tasks to team members
  - Track status (To Do, In Progress, Completed)
  - Set due dates and priorities
  - Update task status in real-time

- **Dashboard**
  - View total, completed, pending, and overdue tasks
  - Project overview
  - Filter tasks by status
  - Real-time statistics

##  Tech Stack

### Backend
- **Node.js + Express.js** - REST API framework
- **MongoDB** - NoSQL database
- **Mongoose** - ODM for MongoDB
- **JWT** - Authentication
- **Bcrypt** - Password hashing
- **Joi** - Input validation
- **CORS** - Cross-origin requests

### Frontend
- **React 18** - UI framework
- **Vite** - Build tool
- **React Router** - Client-side routing
- **Axios** - HTTP client
- **Tailwind CSS** - Utility-first CSS framework
- **date-fns** - Date utilities

##  API Endpoints

### Authentication
- `POST /api/auth/signup` - Register new user
- `POST /api/auth/login` - User login
- `GET /api/auth/me` - Get current user (Protected)

### Projects
- `GET /api/projects` - Get all projects (Protected)
- `POST /api/projects` - Create project (Admin only)
- `GET /api/projects/:id` - Get project details (Protected)
- `PUT /api/projects/:id` - Update project (Admin only)
- `DELETE /api/projects/:id` - Delete project (Admin only)

### Tasks
- `GET /api/projects/:projectId/tasks` - Get project tasks (Protected)
- `POST /api/projects/:projectId/tasks` - Create task (Protected)
- `GET /api/projects/:projectId/tasks/:taskId` - Get task details (Protected)
- `PUT /api/projects/:projectId/tasks/:taskId` - Update task (Protected)
- `DELETE /api/projects/:projectId/tasks/:taskId` - Delete task (Protected)
- `GET /api/projects/tasks/dashboard/stats` - Get dashboard statistics (Protected)

##  Getting Started

### Prerequisites
- Node.js (v16+)
- MongoDB (local or Atlas)
- npm or yarn

### Backend Setup

1. Navigate to backend folder:
```bash
cd backend
```

2. Install dependencies:
```bash
npm install
```

3. Create `.env` file from `.env.example`:
```bash
cp .env.example .env
```

4. Update `.env` with your MongoDB URI and JWT secret:
```env
PORT=5000
NODE_ENV=development
MONGODB_URI=mongodb://localhost:27017/team-task-manager
JWT_SECRET=your_random_secret_key_here
JWT_EXPIRE=7d
FRONTEND_URL=http://localhost:3000
```

5. Start backend in development mode:
```bash
npm run dev
```

The backend will be running on `http://localhost:5000`

### Frontend Setup

1. Navigate to frontend folder:
```bash
cd frontend
```

2. Install dependencies:
```bash
npm install
```

3. Create `.env.local` file:
```bash
cp .env.example .env.local
```

4. Start frontend development server:
```bash
npm run dev
```

The frontend will be running on `http://localhost:3000`

## Security Features

-  JWT-based authentication
- Bcrypt password hashing (10 salt rounds)
-  Role-based access control middleware
-  Protected routes (only authenticated users)
-  Authorization checks (admin-only operations)
-  Input validation with Joi
-  CORS configuration
-  Environment variables for sensitive data

## 🏃 Running the Application

### Development

Terminal 1 - Backend:
```bash
cd backend
npm run dev
```

Terminal 2 - Frontend:
```bash
cd frontend
npm run dev
```

### Production Build

Backend:
```bash
cd backend
npm run build
npm start
```

Frontend:
```bash
cd frontend
npm run build
npm run preview
```

## Database Schema

### User
```javascript
{
  name: String,
  email: String (unique),
  password: String (hashed),
  role: 'admin' | 'member',
  avatar: String,
  createdAt: Date,
  updatedAt: Date
}
```

### Project
```javascript
{
  name: String,
  description: String,
  admin: ObjectId (User),
  members: [ObjectId] (Users),
  status: 'active' | 'archived',
  createdAt: Date,
  updatedAt: Date
}
```

### Task
```javascript
{
  title: String,
  description: String,
  project: ObjectId (Project),
  assignedTo: ObjectId (User),
  createdBy: ObjectId (User),
  status: 'To Do' | 'In Progress' | 'Completed',
  dueDate: Date,
  priority: 'low' | 'medium' | 'high',
  createdAt: Date,
  updatedAt: Date
}
```

## 🚢 Deployment on Railway

### Backend Deployment

1. Push code to GitHub
2. Create new Railway project
3. Connect GitHub repository
4. Configure environment variables in Railway:
   - `MONGODB_URI` - MongoDB Atlas connection string
   - `JWT_SECRET` - Random secret key
   - `NODE_ENV` - Set to "production"
   - `FRONTEND_URL` - Your deployed frontend URL

5. Railway automatically detects `package.json` and deploys

### Frontend Deployment

1. Set `VITE_API_URL` to your Railway backend URL
2. Create new Railway project for frontend
3. Build settings:
   - Build Command: `npm run build`
   - Start Command: `npm run preview`
   - Node Version: 18+

4. Deploy with Railway

### Environment Variables Checklist

Backend (.env):
- [ ] `MONGODB_URI` - MongoDB connection string
- [ ] `JWT_SECRET` - Complex random string
- [ ] `FRONTEND_URL` - Frontend deployment URL
- [ ] `PORT` - 5000 (Railway will set this)

Frontend (.env):
- [ ] `VITE_API_URL` - Backend API URL

## 🧪 Testing API

Use Postman or cURL to test endpoints:

```bash
# Signup
curl -X POST http://localhost:5000/api/auth/signup \
  -H "Content-Type: application/json" \
  -d '{
    "name": "John Doe",
    "email": "john@example.com",
    "password": "password123",
    "confirmPassword": "password123"
  }'

# Login
curl -X POST http://localhost:5000/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "john@example.com",
    "password": "password123"
  }'

# Create Project (with token)
curl -X POST http://localhost:5000/api/projects \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Project Alpha",
    "description": "First project"
  }'
```

## 📁 Project Structure
https://team-collab-69.preview.emergentagent.com/dashboard
https://bf1d3f6e-93db-4bf1-ae6d-0dc9d816203e.preview.emergentagent.com/login

```
Team Task Manager/
├── backend/
│   ├── src/
│   │   ├── config/
│   │   │   └── database.js
│   │   ├── controllers/
│   │   │   ├── authController.js
│   │   │   ├── projectController.js
│   │   │   └── taskController.js
│   │   ├── middleware/
│   │   │   ├── auth.js
│   │   │   └── errorHandler.js
│   │   ├── models/
│   │   │   ├── User.js
│   │   │   ├── Project.js
│   │   │   └── Task.js
│   │   ├── routes/
│   │   │   ├── authRoutes.js
│   │   │   ├── projectRoutes.js
│   │   │   └── taskRoutes.js
│   │   ├── utils/
│   │   │   ├── jwt.js
│   │   │   └── validation.js
│   │   └── server.js
│   ├── package.json
│   ├── .env.example
│   └── .gitignore
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   │   └── ProtectedRoute.jsx
│   │   ├── context/
│   │   │   └── AuthContext.jsx
│   │   ├── pages/
│   │   │   ├── Login.jsx
│   │   │   ├── Signup.jsx
│   │   │   ├── Dashboard.jsx
│   │   │   └── ProjectPage.jsx
│   │   ├── services/
│   │   │   └── api.js
│   │   ├── App.jsx
│   │   ├── main.jsx
│   │   └── index.css
│   ├── index.html
│   ├── package.json
│   ├── vite.config.js
│   ├── tailwind.config.js
│   ├── postcss.config.js
│   ├── .env.example
│   └── .gitignore
├── .gitignore
└── README.md
```

## 🐛 Troubleshooting

**CORS Error**: Make sure `FRONTEND_URL` in backend `.env` matches your frontend URL

**MongoDB Connection Error**: Verify MongoDB is running and `MONGODB_URI` is correct

**Token Expired**: Clear localStorage and login again

**404 on API calls**: Ensure backend is running on correct port

## 📝 Environment Setup Tips

1. **MongoDB Atlas**: Use free tier for development
   - Create cluster
   - Get connection string
   - Whitelist IP address

2. **JWT Secret**: Generate with:
   ```javascript
   require('crypto').randomBytes(32).toString('hex')
   ```

3. **CORS**: Configure origin URL to match frontend

## 🤝 Contributing

1. Create feature branch: `git checkout -b feature/new-feature`
2. Commit changes: `git commit -m 'Add new feature'`
3. Push to branch: `git push origin feature/new-feature`
4. Open pull request

## 📄 License

MIT License - feel free to use for personal and commercial projects

## 👨‍💻 Support

For issues or questions, please open an issue on GitHub or contact the development team.

---
