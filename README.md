# HR Management System - Orel IT

A full-featured HR Management System with separate Admin and Employee portals built with React, Node.js, Express, and MySQL.

## 🎯 Features

### 👤 User Roles & Access Control
- **Admin Portal**: Full system access, employee management, approvals
- **Employee Portal**: Personal dashboard, leave requests, attendance, payslips
- Strict role-based access control on frontend and backend
- JWT-based authentication with token management

### 🔐 Authentication & Security
- Separate login pages for Admin and Employee
- JWT authentication with secure password hashing (bcrypt)
- Force password change on first login
- Role-based route protection
- Password change enforcement before system access

### 👥 Admin Features
- **Dashboard**: Real-time statistics, charts, overview
- **Employee Management**: CRUD operations, search, filter, pagination
- **Leave Management**: Approve/reject leave requests with remarks
- **Attendance Management**: Review and approve attendance issues
- **Payroll Management**: Generate and manage payslips

### 👤 Employee Features
- **Dashboard**: Personal statistics and charts
- **My Profile**: View and edit personal information
- **Leave Requests**: Submit and track leave applications
- **Attendance Issues**: Report missing or incorrect attendance
- **Payslips**: View and download monthly payslips

### 🎨 Modern UI/UX
- Professional enterprise design
- Light and Dark mode support
- Fully responsive (desktop + mobile)
- Tailwind CSS with custom theme
- Recharts for data visualization

## 📁 Project Structure

```
hr-management-system/
├── frontend/              # React + Vite + Tailwind CSS
│   ├── src/
│   │   ├── components/    # Reusable UI components
│   │   ├── context/       # React Context (Auth)
│   │   ├── pages/         # Page components
│   │   │   ├── auth/      # Login, Change Password
│   │   │   ├── admin/     # Admin pages
│   │   │   └── employee/  # Employee pages
│   │   ├── utils/         # API client, helpers
│   │   └── App.jsx        # Main app with routing
│   └── package.json
│
├── backend/               # Node.js + Express + MySQL
│   ├── config/            # Database configuration
│   ├── middleware/        # Auth & authorization middleware
│   ├── routes/            # API routes
│   │   ├── authRoutes.js
│   │   ├── adminRoutes.js
│   │   └── employeeRoutes.js
│   ├── server.js          # Express server
│   └── package.json
│
└── README.md
```

## 🚀 Setup Instructions

### Prerequisites
- Node.js (v16+)
- MySQL (v8.0+)
- npm or yarn

### 1. Database Setup

Create MySQL database:

```sql
CREATE DATABASE hr_management_db;
```

### 2. Backend Setup

```bash
cd backend

# Install dependencies
npm install

# Create .env file from example
copy .env.example .env

# Edit .env with your database credentials
# DB_HOST=localhost
# DB_USER=root
# DB_PASSWORD=your_password
# DB_NAME=hr_management_db
# JWT_SECRET=your_secret_key_here
# PORT=5000

# Start backend server
npm run dev
```

The backend will automatically:
- Create all required database tables
- Create a default admin account (admin@orelit.com / admin123)

### 3. Frontend Setup

```bash
cd frontend

# Install dependencies
npm install

# Start development server
npm run dev
```

Frontend will run on http://localhost:3000

## 🔑 Default Credentials

### Admin Login
- **URL**: http://localhost:3000/admin/login
- **Email**: admin@orelit.com
- **Password**: admin123

### Employee Login
Employees are created by admin. After creation, they receive temporary passwords.

## 📡 API Endpoints

### Authentication
- `POST /api/auth/admin/login` - Admin login
- `POST /api/auth/employee/login` - Employee login
- `POST /api/auth/change-password` - Change password (protected)

### Admin APIs (Protected - Admin Only)
- `GET /api/admin/dashboard/stats` - Dashboard statistics
- `GET /api/admin/employees` - Get all employees
- `POST /api/admin/employees` - Create employee
- `PUT /api/admin/employees/:id` - Update employee
- `DELETE /api/admin/employees/:id` - Delete employee
- `GET /api/admin/leaves` - Get all leave requests
- `PATCH /api/admin/leaves/:id` - Approve/reject leave
- `GET /api/admin/attendance` - Get all attendance issues
- `PATCH /api/admin/attendance/:id` - Approve/reject attendance
- `GET /api/admin/payslips` - Get all payslips
- `POST /api/admin/payslips` - Generate payslip

### Employee APIs (Protected - Employee Only)
- `GET /api/employee/dashboard/stats` - Personal dashboard stats
- `GET /api/employee/profile` - Get own profile
- `PUT /api/employee/profile` - Update own profile
- `GET /api/employee/leaves` - Get own leave requests
- `POST /api/employee/leaves` - Submit leave request
- `GET /api/employee/attendance` - Get own attendance issues
- `POST /api/employee/attendance` - Submit attendance issue
- `GET /api/employee/payslips` - Get own payslips

## 🎨 Theme Colors

### Light Mode
- Primary: #2563EB
- Background: #F8FAFC
- Cards: #FFFFFF
- Text: #0F172A
- Success: #16A34A
- Warning: #F59E0B
- Danger: #DC2626

### Dark Mode
- Background: #020617
- Cards: #0F172A
- Primary: #3B82F6
- Text: #E5E7EB

## 🗄️ Database Schema

### Tables
1. **users** - User accounts (admin, employee)
2. **employees** - Employee details
3. **leaves** - Leave requests
4. **attendance** - Attendance issues
5. **payslips** - Monthly payslips

### Entity Relationships
- users → employees (1:1)
- employees → leaves (1:N)
- employees → attendance (1:N)
- employees → payslips (1:N)

## 🔒 Security Features

- Passwords hashed with bcrypt
- JWT tokens with expiration
- Role-based authorization on all endpoints
- Protected routes on frontend
- SQL injection prevention (parameterized queries)
- XSS protection
- CORS enabled

## 📦 Tech Stack

### Frontend
- React 18
- Vite
- React Router DOM
- Tailwind CSS
- Axios
- Recharts
- Lucide React (icons)
- jsPDF (PDF generation)

### Backend
- Node.js
- Express.js
- MySQL2
- bcryptjs
- jsonwebtoken
- dotenv
- cors
- multer (file uploads)

## 🚀 Production Deployment

### Frontend Build
```bash
cd frontend
npm run build
```

### Backend Production
```bash
cd backend
npm start
```

### Environment Variables (Production)
- Set `NODE_ENV=production`
- Use strong `JWT_SECRET`
- Secure database credentials
- Enable HTTPS
- Configure CORS properly

## 📝 Development Workflow

### Adding New Employee (Admin)
1. Login as admin
2. Navigate to Employees section
3. Click "Add Employee"
4. Fill employee details
5. System generates temporary password
6. Share credentials with employee
7. Employee must change password on first login

### Employee Leave Request Flow
1. Employee logs in
2. Navigate to Leave Request
3. Fill leave form (type, dates, reason)
4. Submit request
5. Admin reviews and approves/rejects
6. Employee receives status update

## 🐛 Troubleshooting

### Database Connection Error
- Verify MySQL is running
- Check database credentials in .env
- Ensure database exists

### Frontend-Backend Connection
- Verify backend is running on port 5000
- Check API base URL in frontend/src/utils/api.js
- Ensure CORS is enabled

### Authentication Issues
- Clear browser localStorage
- Check JWT_SECRET matches
- Verify token expiration

## 📄 License

This project is created for Orel IT HR Management System.

## 👥 Support

For issues or questions, contact the development team.

---

**Built with ❤️ for Orel IT**
