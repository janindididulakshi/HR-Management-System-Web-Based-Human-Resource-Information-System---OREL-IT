# Supabase Setup Guide

This guide will help you set up the Supabase database for the HR Management System.

## Step 1: Access Your Supabase Project

1. Go to [https://supabase.com/dashboard](https://supabase.com/dashboard)
2. Navigate to your project: **hr-management-system**
3. Your Project URL: `https://izcvlqpdwjfdpilpmvvb.supabase.co`

## Step 2: Execute the Database Schema

1. In your Supabase dashboard, click on **"SQL Editor"** in the left sidebar
2. Click **"New query"**
3. Open the file `backend/supabase-schema.sql` from your project
4. Copy the entire SQL content and paste it into the Supabase SQL Editor
5. Click **"Run"** or press `Ctrl+Enter`

This will create:
- ✅ All required tables (users, employees, leaves, attendance, payslips)
- ✅ PostgreSQL ENUM types
- ✅ Foreign key relationships
- ✅ Automatic updated_at triggers
- ✅ Performance indexes
- ✅ Row Level Security (RLS) policies

## Step 3: Verify Database Setup

After running the schema, verify the tables were created:

1. Click on **"Table Editor"** in the left sidebar
2. You should see all these tables:
   - `users`
   - `employees`
   - `leaves`
   - `attendance`
   - `payslips`

## Step 4: Start the Backend Server

The backend is already configured with your Supabase credentials.

```bash
cd backend
npm run dev
```

You should see:
```
✅ Supabase connected successfully
⚠️  Note: Please run the SQL schema from backend/supabase-schema.sql in your Supabase SQL Editor if you haven't already
✅ Default admin created (if not already existing)
🚀 Server running on port 5000
```

## Step 5: Test the Connection

1. The backend will automatically create a default admin account with:
   - Email: `admin@orelit.com`
   - Password: `admin123`

2. You can test the connection by accessing: `http://localhost:5000/api/health`

## Step 6: Start the Frontend

```bash
cd frontend
npm run dev
```

The frontend will run on `http://localhost:3000`

## Troubleshooting

### Error: "relation does not exist"
**Solution**: You forgot to run the SQL schema. Go back to Step 2 and execute `backend/supabase-schema.sql` in the Supabase SQL Editor.

### Error: "Missing Supabase credentials"
**Solution**: Check that your `backend/.env` file contains:
```
SUPABASE_URL=https://izcvlqpdwjfdpilpmvvb.supabase.co
SUPABASE_SERVICE_KEY=your_service_role_key_here
```

### Error: "Invalid API key"
**Solution**: Your service_role key might be incorrect. Get it from:
1. Supabase Dashboard → Settings → API
2. Copy the **service_role** key (click "Reveal" to see it)
3. Update it in your `backend/.env` file

### RLS Policies Error
**Solution**: The schema includes RLS policies that allow the service_role (backend) full access. If you're having permission issues, ensure:
1. You're using the **service_role** key in the backend (not the anon key)
2. The RLS policies were created correctly (check the SQL editor output)

## What's Different from MySQL?

### Database Connection
- **Before**: MySQL connection pool with host/user/password
- **Now**: Supabase client with URL and API key

### Query Syntax
- **Before**: `pool.query('SELECT * FROM users WHERE id = ?', [id])`
- **Now**: `supabase.from('users').select('*').eq('id', id)`

### Joins
- **Before**: SQL JOIN syntax
- **Now**: Supabase nested selects, e.g., `.select('*, users(email)')`

### Transactions
- **Before**: `connection.beginTransaction()` and `connection.commit()`
- **Now**: Handled through proper error handling and rollback on failure

## Key Benefits of Supabase

✅ **Cloud-hosted**: No local MySQL installation needed
✅ **Auto-scaling**: Handles traffic automatically
✅ **Built-in Auth**: (Future upgrade option)
✅ **Real-time**: Can add real-time features easily
✅ **Automatic backups**: Database is automatically backed up
✅ **Dashboard**: Easy data viewing and editing via Supabase UI
✅ **API**: Auto-generated REST API (we're using custom Express API for now)

## Security Notes

🔒 **IMPORTANT**: 
- The **service_role** key in your `.env` file has full database access
- Never commit it to version control
- Never expose it in frontend code
- Only use it in backend code

The current setup uses:
- Backend API with Express (keeps your service_role key secure)
- JWT authentication (your existing auth system)
- RLS policies (additional database-level security)

## Next Steps

Once everything is working, you can:
1. Add more employees via the Admin dashboard
2. Test employee login and features
3. Deploy to production (see deployment guide in README.md)
4. Optional: Migrate to Supabase Auth in the future for even simpler auth management

## Support

If you encounter any issues:
1. Check the browser console for frontend errors
2. Check the backend terminal for server errors
3. Check Supabase Dashboard → Logs for database errors
4. Verify all tables exist in Table Editor
5. Verify RLS policies exist in Authentication → Policies
