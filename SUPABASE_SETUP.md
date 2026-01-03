# Supabase Setup Guide

## 1. Create Supabase Project

1. Go to [supabase.com](https://supabase.com) and create an account
2. Create a new project
3. Wait for the database to be set up (this takes a few minutes)

## 2. Get Your Project Credentials

Once your project is ready:

1. Go to **Settings** → **API**
2. Copy the following values:
   - **Project URL**: `https://[YOUR-PROJECT-REF].supabase.co`
   - **anon/public key**: Your anon key
   - **service_role key**: Your service role key (keep this secret!)

3. Go to **Settings** → **Database**
4. Copy the **Connection string** (it should look like: `postgresql://postgres:[PASSWORD]@db.[PROJECT-REF].supabase.co:5432/postgres`)

## 3. Configure Environment Variables

### Backend (.env)
```env
DATABASE_URL=postgresql://postgres:[YOUR-PASSWORD]@db.[YOUR-PROJECT-REF].supabase.co:5432/postgres
SUPABASE_URL=https://[YOUR-PROJECT-REF].supabase.co
SUPABASE_ANON_KEY=[YOUR-ANON-KEY]
SUPABASE_SERVICE_ROLE_KEY=[YOUR-SERVICE-ROLE-KEY]
```

### Frontend (.env.local)
```env
NEXT_PUBLIC_API_URL=http://localhost:8001
NEXT_PUBLIC_SUPABASE_URL=https://[YOUR-PROJECT-REF].supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=[YOUR-ANON-KEY]
```

## 4. Database Setup

The app will automatically create tables when you run the initial data script. But if you want to set up manually:

1. Go to **SQL Editor** in your Supabase dashboard
2. The tables will be created automatically when you run:
   ```bash
   cd backend && python initial_data.py
   ```

## 5. Authentication Setup

Supabase Auth is already configured in the code. Users can:
- Register with email/password
- Login with email/password
- Automatic session management
- Password reset (if you enable it in Supabase dashboard)

## 6. Enable Email Confirmation (Optional)

In your Supabase dashboard:
1. Go to **Authentication** → **Settings**
2. Enable **Enable email confirmations**
3. Configure SMTP settings if you want custom emails

## 7. Run the Application

```bash
# Backend
cd backend
pip install -r requirements.txt
python initial_data.py
python run.py

# Frontend (new terminal)
npm install
npm run dev
```

## 8. Test Authentication

1. Go to `http://localhost:3000`
2. Try registering a new account
3. Check your email for verification (if enabled)
4. Login and access the dashboard

## Troubleshooting

### Database Connection Issues
- Make sure your DATABASE_URL is correct
- Check if your IP is allowed in Supabase (Settings → Database → Allow all IPs for development)

### Authentication Issues
- Verify your SUPABASE_URL and keys are correct
- Check Supabase dashboard for any auth errors

### CORS Issues
- Supabase handles CORS automatically for the database
- For the API, make sure your NEXT_PUBLIC_API_URL is correct

## Security Notes

- Never commit your `.env` files to version control
- Keep your `SUPABASE_SERVICE_ROLE_KEY` secret (only used server-side)
- The `SUPABASE_ANON_KEY` is safe to use in frontend code