# TaskMaster - Multi-User Todo Application

TaskMaster is a full-stack web application that allows users to create, manage, and track their personal tasks with secure authentication and user isolation.

## 🚀 Quick Start

### First Time Setup

```bash
# Run the development setup script
.\start-dev.bat
```

This will automatically:
- Set up Python virtual environment
- Install all dependencies (backend + frontend)
- Start both servers

### Subsequent Runs

```bash
# Quick start (dependencies already installed)
.\start.bat
```

### Access the Application

- **Frontend:** http://localhost:3000
- **Backend API:** http://localhost:8000
- **API Documentation:** http://localhost:8000/docs

---

## 📖 Complete Setup Guide

For detailed instructions, troubleshooting, and manual setup, see [SETUP_GUIDE.md](SETUP_GUIDE.md).

## Features

- **User Authentication**: Secure registration and login with JWT tokens
- **Task Management**: Create, read, update, and delete tasks
- **User Isolation**: Users can only access their own tasks
- **Responsive Design**: Works on desktop, tablet, and mobile devices
- **Real-time Updates**: Tasks update immediately after changes
- **Filtering**: Filter tasks by status (all, active, completed)

## Tech Stack

### Backend
- **Framework**: FastAPI
- **Database**: PostgreSQL (with Neon Serverless)
- **ORM**: SQLModel
- **Authentication**: JWT with custom middleware
- **Dependencies**: 
  - fastapi==0.104.1
  - sqlmodel==0.0.16
  - pydantic==2.5.0
  - passlib[bcrypt]==1.7.4
  - python-jose[cryptography]==3.3.0

### Frontend
- **Framework**: Next.js 16+
- **Styling**: Tailwind CSS
- **State Management**: React Context API
- **Animations**: Framer Motion
- **Authentication**: Better Auth
- **Dependencies**:
  - react, react-dom
  - next
  - tailwindcss
  - better-auth
  - framer-motion

## Getting Started

### Prerequisites

- Node.js 18+
- Python 3.11+
- Docker (for database)

### Installation

1. Clone the repository:
```bash
git clone https://github.com/your-org/todo-fullstack-app.git
cd todo-fullstack-app
```

2. Set up environment variables:
```bash
cp .env.example .env
```
Then update the values in `.env` with your specific configuration.

3. Install backend dependencies:
```bash
cd backend
pip install -r requirements.txt
```

4. Install frontend dependencies:
```bash
cd ../frontend
npm install
```

### Running the Application

1. Start the database with Docker:
```bash
docker-compose up -d
```

2. Start the backend:
```bash
cd backend
uvicorn src.main:app --reload --port 8000
```

3. In a new terminal, start the frontend:
```bash
cd frontend
npm run dev
```

4. Access the application:
   - Frontend: http://localhost:3000
   - Backend API: http://localhost:8000
   - Backend Docs: http://localhost:8000/docs

## API Endpoints

### Authentication
- `POST /auth/register` - Register a new user
- `POST /auth/login` - Authenticate a user
- `POST /auth/logout` - Log out a user

### Tasks
- `GET /users/{user_id}/tasks` - Get user's tasks
- `POST /users/{user_id}/tasks` - Create a new task
- `GET /users/{user_id}/tasks/{task_id}` - Get a specific task
- `PUT /users/{user_id}/tasks/{task_id}` - Update a task
- `PATCH /users/{user_id}/tasks/{task_id}/complete` - Toggle task completion
- `DELETE /users/{user_id}/tasks/{task_id}` - Delete a task

## Project Structure

```
todo-fullstack-app/
├── backend/
│   ├── src/
│   │   ├── models/      # Database models
│   │   ├── api/         # API routes
│   │   ├── services/    # Business logic
│   │   ├── middleware/  # Authentication, etc.
│   │   └── utils/       # Utility functions
│   ├── tests/           # Backend tests
│   └── requirements.txt # Python dependencies
├── frontend/
│   ├── src/
│   │   ├── app/         # Next.js app router pages
│   │   ├── components/  # Reusable UI components
│   │   ├── providers/   # Context providers
│   │   ├── lib/         # Utilities and API client
│   │   ├── hooks/       # Custom React hooks
│   │   └── styles/      # Global styles
│   ├── tests/           # Frontend tests
│   ├── package.json     # Node.js dependencies
│   └── tailwind.config.js # Tailwind CSS config
├── docker-compose.yml   # Docker configuration
└── .env.example         # Environment variables example
```

## Security

- All API endpoints require authentication via JWT tokens
- User isolation is enforced at the API level - users can only access their own tasks
- Passwords are hashed using bcrypt
- Input validation is performed on both frontend and backend

## Testing

To run backend tests:
```bash
cd backend
pytest
```

To run frontend tests:
```bash
cd frontend
npm test
```

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License.