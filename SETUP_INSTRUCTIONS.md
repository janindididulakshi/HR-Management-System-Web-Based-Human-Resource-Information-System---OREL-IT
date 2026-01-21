# Setup Instructions for New Features

## Database Migration

Run the following SQL migration to add the required columns and tables:

```bash
# Connect to your database and run:
psql -U your_username -d your_database_name -f backend/migrations/add_notifications_and_profile_pictures.sql
```

Or if using Supabase, you can:
1. Go to your Supabase dashboard
2. Navigate to SQL Editor
3. Copy and paste the contents of `backend/migrations/add_notifications_and_profile_pictures.sql`
4. Execute the SQL

## Features Added

### 1. Profile Picture Upload
- **Backend**: Multer middleware configured for file uploads
- **Endpoints**: 
  - `POST /api/employee/profile/picture` - Upload employee profile picture
  - `POST /api/admin/profile/picture` - Upload admin profile picture
- **Storage**: Profile pictures are stored in `backend/uploads/` directory
- **Frontend**: Both employee and admin profile pages now have profile picture upload functionality

### 2. Notification System
- **Backend**: 
  - New `notifications` table created
  - Notification endpoints at `/api/notifications`
  - Automatic notifications sent when:
    - Leave request approved/rejected
    - Attendance issue approved/rejected
    - Payslip released
- **Frontend**: 
  - Notification dropdown in top bar
  - Real-time unread count badge
  - Mark as read functionality
  - Auto-refresh every 30 seconds

### 3. Clickable Profile Icons
- Profile icons in the top bar now navigate to the appropriate profile page
- Admin icon goes to `/admin/profile`
- Employee icon goes to `/employee/profile`

### 4. Admin Profile Page
- New admin profile page created at `/admin/profile`
- Allows admin to:
  - Upload profile picture
  - Edit name
  - View email

### 5. Enhanced Payslip PDF
- Payslip PDFs now include:
  - Complete employee information (name, ID, designation, department, email, join date)
  - Professional formatting with color-coded sections
  - Detailed earnings and deductions breakdown
  - Company branding and headers
  - Automatic filename: `Payslip_{EmpID}_{Month}_{Year}.pdf`

## Environment Variables

Make sure you have the following in your `.env` file:

```env
# Backend
PORT=5000
NODE_ENV=development
SUPABASE_URL=your_supabase_url
SUPABASE_KEY=your_supabase_key
JWT_SECRET=your_jwt_secret

# Frontend (create .env in frontend directory)
VITE_API_URL=http://localhost:5000
```

## Running the Application

### Backend
```bash
cd backend
npm install
npm start
```

### Frontend
```bash
cd frontend
npm install
npm run dev
```

## Testing Notifications

To test the notification system:

1. Login as admin
2. Navigate to Leave Management or Attendance Management
3. Approve or reject a request
4. Login as the employee whose request you modified
5. Check the notification icon - you should see a badge with unread count
6. Click the bell icon to view notifications

## Known Issues & Notes

1. **Email Notifications**: The notification system creates in-app notifications. Email notifications require additional setup with an email service provider (e.g., SendGrid, AWS SES).

2. **File Upload Size**: Current limit is 5MB per file. To change this, modify the limit in `backend/middleware/upload.js`.

3. **Supported Image Formats**: jpeg, jpg, png, gif

4. **Profile Picture Path**: Profile pictures are served from `/uploads/` endpoint on the backend server.

## Troubleshooting

### Profile Pictures Not Showing
- Ensure the `backend/uploads/` directory exists and has write permissions
- Check that the backend server is serving static files from `/uploads/`
- Verify the `VITE_API_URL` is correctly set in frontend `.env`

### Notifications Not Working
- Verify the `notifications` table was created successfully
- Check browser console for any API errors
- Ensure the employee has an email address in the database

### PDF Download Issues
- Clear browser cache
- Check that jsPDF is installed: `npm list jspdf`
- Verify employee profile data is loading correctly
