# API Documentation

## Base URL
- Development: `http://localhost:5000/api`
- Production: Your Railway backend URL

---

## Authentication

All protected endpoints require JWT token in header:
```
Authorization: Bearer YOUR_JWT_TOKEN
```

---

## Endpoints

### 1. Authentication

#### Signup
```http
POST /auth/signup
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "password123",
  "confirmPassword": "password123"
}
```

**Response:**
```json
{
  "message": "User registered successfully",
  "user": {
    "_id": "user_id",
    "name": "John Doe",
    "email": "john@example.com",
    "role": "member",
    "createdAt": "2024-01-01T00:00:00Z"
  },
  "token": "eyJhbGc..."
}
```

#### Login
```http
POST /auth/login
Content-Type: application/json

{
  "email": "john@example.com",
  "password": "password123"
}
```

**Response:**
```json
{
  "message": "Login successful",
  "user": {
    "_id": "user_id",
    "name": "John Doe",
    "email": "john@example.com",
    "role": "member"
  },
  "token": "eyJhbGc..."
}
```

#### Get Current User
```http
GET /auth/me
Authorization: Bearer YOUR_TOKEN
```

**Response:**
```json
{
  "user": {
    "_id": "user_id",
    "name": "John Doe",
    "email": "john@example.com",
    "role": "member"
  }
}
```

---

### 2. Projects

#### Get All Projects
```http
GET /projects
Authorization: Bearer YOUR_TOKEN
```

**Response:**
```json
{
  "projects": [
    {
      "_id": "project_id",
      "name": "Project Alpha",
      "description": "First project",
      "admin": { "_id": "admin_id", "name": "Admin Name", "email": "admin@example.com" },
      "members": [
        { "_id": "member_id", "name": "Member Name", "email": "member@example.com" }
      ],
      "status": "active",
      "createdAt": "2024-01-01T00:00:00Z"
    }
  ]
}
```

#### Create Project (Admin Only)
```http
POST /projects
Authorization: Bearer YOUR_TOKEN
Content-Type: application/json

{
  "name": "Project Beta",
  "description": "New project",
  "members": ["member_id_1", "member_id_2"]
}
```

**Response:**
```json
{
  "message": "Project created successfully",
  "project": {
    "_id": "new_project_id",
    "name": "Project Beta",
    "description": "New project",
    "admin": { "_id": "your_id", "name": "Your Name", "email": "you@example.com" },
    "members": [...],
    "status": "active",
    "createdAt": "2024-01-01T00:00:00Z"
  }
}
```

#### Get Project Details
```http
GET /projects/:projectId
Authorization: Bearer YOUR_TOKEN
```

#### Update Project (Admin Only)
```http
PUT /projects/:projectId
Authorization: Bearer YOUR_TOKEN
Content-Type: application/json

{
  "name": "Updated Project Name",
  "description": "Updated description",
  "members": ["member_id_1"]
}
```

#### Delete Project (Admin Only)
```http
DELETE /projects/:projectId
Authorization: Bearer YOUR_TOKEN
```

---

### 3. Tasks

#### Get All Tasks in Project
```http
GET /projects/:projectId/tasks
Authorization: Bearer YOUR_TOKEN

Query Parameters:
- status: "To Do" | "In Progress" | "Completed" (optional)
- assignedTo: user_id (optional)
```

**Response:**
```json
{
  "tasks": [
    {
      "_id": "task_id",
      "title": "Design homepage",
      "description": "Create wireframes and mockups",
      "project": "project_id",
      "assignedTo": {
        "_id": "user_id",
        "name": "John Doe",
        "email": "john@example.com"
      },
      "createdBy": { "_id": "creator_id", "name": "Creator", "email": "creator@example.com" },
      "status": "In Progress",
      "dueDate": "2024-02-01T00:00:00Z",
      "priority": "high",
      "createdAt": "2024-01-01T00:00:00Z"
    }
  ]
}
```

#### Create Task
```http
POST /projects/:projectId/tasks
Authorization: Bearer YOUR_TOKEN
Content-Type: application/json

{
  "title": "Setup database",
  "description": "Configure MongoDB",
  "assignedTo": "user_id",
  "dueDate": "2024-02-15",
  "priority": "high"
}
```

#### Update Task
```http
PUT /projects/:projectId/tasks/:taskId
Authorization: Bearer YOUR_TOKEN
Content-Type: application/json

{
  "status": "Completed",
  "priority": "medium"
}
```

#### Delete Task
```http
DELETE /projects/:projectId/tasks/:taskId
Authorization: Bearer YOUR_TOKEN
```

#### Get Dashboard Statistics
```http
GET /projects/tasks/dashboard/stats
Authorization: Bearer YOUR_TOKEN
```

**Response:**
```json
{
  "stats": {
    "totalTasks": 15,
    "completedTasks": 8,
    "inProgressTasks": 4,
    "todoTasks": 3,
    "overdueTasks": 1
  }
}
```

---

## Error Responses

### 400 Bad Request
```json
{
  "message": "Validation error",
  "errors": ["Email is required", "Password must be at least 6 characters"]
}
```

### 401 Unauthorized
```json
{
  "message": "Invalid token"
}
```

### 403 Forbidden
```json
{
  "message": "Only admin can perform this action"
}
```

### 404 Not Found
```json
{
  "message": "Project not found"
}
```

### 409 Conflict
```json
{
  "message": "Email already exists"
}
```

### 500 Internal Server Error
```json
{
  "message": "Internal server error"
}
```

---

## Status Codes

- `200` - OK
- `201` - Created
- `400` - Bad Request (validation error)
- `401` - Unauthorized (no/invalid token)
- `403` - Forbidden (insufficient permissions)
- `404` - Not Found
- `409` - Conflict (duplicate email)
- `500` - Internal Server Error

---

## Rate Limits

None implemented yet, but recommended for production:
- 100 requests per 15 minutes per user

---

## Authentication Token

The JWT token contains:
```json
{
  "userId": "user_id",
  "iat": 1609459200,
  "exp": 1610064000
}
```

Default expiry: 7 days

---

## Sorting & Filtering

Tasks support:
- `GET /projects/:projectId/tasks?status=Completed`
- `GET /projects/:projectId/tasks?assignedTo=user_id`
- Response is sorted by `createdAt: -1` (newest first)

---

## Testing with Curl

### Save token to variable
```bash
TOKEN=$(curl -X POST http://localhost:5000/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email":"test@example.com","password":"password"}' \
  | jq -r '.token')
```

### Use token in request
```bash
curl -H "Authorization: Bearer $TOKEN" \
  http://localhost:5000/api/projects
```

---

## Common Issues

### "No token provided"
- Missing Authorization header
- Fix: Add `Authorization: Bearer YOUR_TOKEN` header

### "Invalid token"
- Token expired or corrupted
- Fix: Login again to get new token

### "Only admin can perform this action"
- User role is not "admin"
- Fix: Login as admin or request admin privileges

---

## Pagination (Future Feature)

Implementation planned:
```http
GET /projects?page=1&limit=10
```

---

**Last Updated:** January 2024
