# Quick Start Guide - HR Management System

Get the HR Management System running in 5 minutes!

## Prerequisites

Before starting, ensure you have:
- ✅ Node.js v16+ installed
- ✅ MySQL 8.0+ installed and running
- ✅ A terminal/command prompt open

## Step 1: Database Setup (2 minutes)

Open MySQL and create the database:

```sql
CREATE DATABASE hr_management_db;
```

That's it! The backend will create all tables automatically.

## Step 2: Backend Setup (2 minutes)

```bash
# Navigate to backend directory
cd backend

# Install dependencies
npm install

# Create environment file
copy .env.example .env

# Edit .env with your MySQL credentials (use notepad or any text editor)
# Update these lines:
# DB_PASSWORD=your_mysql_password
# JWT_SECRET=any_random_string_here

# Start the backend server
npm run dev
```

You should see:
```
✅ Database connected successfully
✅ Database tables created successfully
✅ Default admin created
🚀 Server running on port 5000
```

## Step 3: Frontend Setup (1 minute)

Open a NEW terminal/command prompt:

```bash
# Navigate to frontend directory
cd frontend

# Install dependencies
npm install

# Start the frontend
npm run dev
```

The app will open at http://localhost:3000

## Step 4: Login & Test

### Admin Login
- **URL**: http://localhost:3000/admin/login
- **Email**: admin@orelit.com
- **Password**: admin123

### Test the System:

1. **Add an Employee**:
   - Go to "Employees" → Click "Add Employee"
   - Fill the form (all fields with * are required)
   - Save - you'll get a temporary password
   - **Important**: Save this password for employee login!

2. **Employee Login**:
   - Open http://localhost:3000/employee/login in a new incognito/private window
   - Use the email and temporary password from step 1
   - You'll be forced to change the password
   - Access the employee dashboard

3. **Test Features**:
   - **As Employee**: Submit a leave request
   - **As Admin**: Go to Leave Management and approve it
   - **As Admin**: Generate a payslip for the employee
   - **As Employee**: View the payslip

## Common Issues & Solutions

### Issue: "Cannot connect to database"
**Solution**: 
- Make sure MySQL is running
- Check DB_PASSWORD in backend/.env matches your MySQL password
- Ensure database `hr_management_db` exists

### Issue: "Port 3000 already in use"
**Solution**: 
- Stop any other apps running on port 3000
- Or change the port in frontend/vite.config.js

### Issue: "Port 5000 already in use"
**Solution**: 
- Change PORT=5001 in backend/.env
- Also update frontend/src/utils/api.js baseURL to http://localhost:5001

### Issue: Frontend shows connection errors
**Solution**: 
- Make sure backend is running first (npm run dev in backend folder)
- Check http://localhost:5000/health in browser - should return {"status":"OK"}

## What's Next?

### Explore Admin Features:
- ✅ Employee Management (CRUD operations)
- ✅ Leave Approvals
- ✅ Attendance Issues Management
- ✅ Payroll Generation
- ✅ Dashboard with statistics

### Explore Employee Features:
- ✅ Personal Dashboard
- ✅ Profile Management
- ✅ Leave Requests
- ✅ Attendance Issue Reporting
- ✅ Payslip Viewing

### Customize:
1. **Change Theme**: Edit `frontend/tailwind.config.js`
2. **Add Departments**: Hardcoded options can be made dynamic
3. **Email Notifications**: Implement email service for credentials
4. **PDF Payslips**: Integrate jsPDF for actual PDF generation

## System Architecture

```
┌──────────────┐         ┌──────────────┐         ┌──────────────┐
│   Browser    │────────▶│  React App   │────────▶│  Express API │
│  (Frontend)  │         │  (Port 3000) │         │  (Port 5000) │
└──────────────┘         └──────────────┘         └──────────────┘
                                                           │
                                                           ▼
                                                   ┌──────────────┐
                                                   │    MySQL     │
                                                   │   Database   │
                                                   └──────────────┘
```

## Security Notes

⚠️ **For Production Deployment**:
1. Change JWT_SECRET to a strong random value
2. Change default admin password immediately
3. Use environment variables for all secrets
4. Enable HTTPS
5. Add rate limiting
6. Implement proper logging
7. Use secure session storage

## Need Help?

- Check the full README.md for detailed documentation
- Review API endpoints in the main README
- Check database schema in backend/config/database.js

## Default Credentials

**Admin:**
- Email: admin@orelit.com
- Password: admin123
- ⚠️ Change this immediately after first login!

**Employees:**
- Created by admin with temporary passwords
- Must change password on first login

---

**🎉 Congratulations! Your HR Management System is now running!**

For detailed documentation, see README.md
