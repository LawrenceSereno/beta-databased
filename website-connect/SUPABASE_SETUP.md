# Supabase Integration Setup Guide

This guide will help you set up Supabase for your BestBuddies Pet Grooming application.

## Prerequisites

1. A Supabase account (sign up at https://supabase.com)
2. Your Supabase project URL and anon key (already configured in `js/supabase-config.js`)

## Step 1: Create Database Tables

1. Go to your Supabase project dashboard
2. Navigate to **SQL Editor**
3. Open the file `supabase-schema.sql` from this project
4. Copy the entire SQL content
5. Paste it into the SQL Editor
6. Click **Run** to execute the SQL

This will create all necessary tables:
- `users` - User profiles
- `groomers` - Groomer information
- `packages` - Service packages
- `bookings` - Booking records
- `staff_absences` - Staff absence records
- `booking_history` - Booking history log
- `calendar_blackouts` - Calendar blackout dates
- `customer_profiles` - Customer profile data

## Step 2: Enable Email Authentication

1. In Supabase dashboard, go to **Authentication** > **Providers**
2. Enable **Email** provider
3. Configure email settings (optional, for production)

## Step 3: Set Up Google OAuth (Optional)

1. In Supabase dashboard, go to **Authentication** > **Providers**
2. Enable **Google** provider
3. Add your Google OAuth credentials:
   - Client ID
   - Client Secret
4. Add redirect URL: `https://uizkbnggqfwvmzttwbjx.supabase.co/auth/v1/callback`

## Step 4: Initialize Default Data

After creating the tables, you'll need to populate initial data:

### Packages
Run this SQL in the SQL Editor:

```sql
INSERT INTO public.packages (id, name, type, duration, includes, tiers) VALUES
('full-basic', '✂️ Full Package · Basic', 'any', 75, 
 '["Bath & Dry", "Brush / De-Shedding", "Hair Cut (Basic)", "Nail Trim", "Ear Clean", "Foot Pad Clean", "Cologne"]'::jsonb,
 '[{"label": "5kg & below", "price": 530}, {"label": "5.1 – 8kg", "price": 630}, {"label": "8.1 – 15kg", "price": 750}, {"label": "15.1 – 30kg", "price": 800}, {"label": "30kg & above", "price": 920}]'::jsonb),
('full-styled', '✂️ Full Package · Trimming & Styling', 'any', 90,
 '["Bath & Dry", "Brush / De-Shedding", "Hair Cut (Styled)", "Nail Trim", "Ear Clean", "Foot Pad Clean", "Cologne"]'::jsonb,
 '[{"label": "5kg & below", "price": 630}, {"label": "5.1 – 8kg", "price": 730}, {"label": "8.1 – 15kg", "price": 880}, {"label": "15.1 – 30kg", "price": 930}, {"label": "30kg & above", "price": 1050}]'::jsonb),
('bubble-bath', '🧴 Shampoo Bath ''n Bubble', 'any', 60,
 '["Bath & Dry", "Brush / De-Shedding", "Hygiene Trim", "Nail Trim", "Ear Clean", "Foot Pad Clean", "Cologne"]'::jsonb,
 '[{"label": "5kg & below", "price": 350}, {"label": "5.1 – 8kg", "price": 450}, {"label": "8.1 – 15kg", "price": 550}, {"label": "15.1 – 30kg", "price": 600}, {"label": "30kg & above", "price": 700}]'::jsonb),
('single-service', '🚿 Single Service · Mix & Match', 'any', 45,
 '["Choose from Nail Trim, Ear Clean, or Hygiene Focus", "Add to any package as needed"]'::jsonb,
 '[{"label": "Nail Trim 5kg & below", "price": 50}, {"label": "Nail Trim 30kg & above", "price": 80}, {"label": "Ear Clean 5kg & below", "price": 70}, {"label": "Ear Clean 30kg & above", "price": 90}]'::jsonb),
('addon-toothbrush', '🛁 Add-on · Toothbrush', 'addon', 5,
 '["Individual toothbrush to bring home"]'::jsonb,
 '[{"label": "Per item", "price": 25}]'::jsonb),
('addon-dematting', '🛁 Add-on · De-matting', 'addon', 25,
 '["Targeted de-matting service"]'::jsonb,
 '[{"label": "Light tangles", "price": 80}, {"label": "Heavy tangles", "price": 250}]'::jsonb);
```

### Groomers
```sql
INSERT INTO public.groomers (id, name, specialty, max_daily_bookings) VALUES
('groomer-sam', 'Sam', 'Small breed specialist', 3),
('groomer-jom', 'Jom', 'Double-coat care', 3),
('groomer-botchoy', 'Botchoy', 'Creative trims & styling', 3),
('groomer-jinold', 'Jinold', 'Senior pet handler', 3),
('groomer-ejay', 'Ejay', 'Cat whisperer', 3);
```

## Step 5: Create Admin User

1. Go to **Authentication** > **Users** in Supabase dashboard
2. Click **Add user** > **Create new user**
3. Enter admin email and password
4. After creating, note the user ID
5. Run this SQL (replace `USER_ID_HERE` with the actual user ID):

```sql
INSERT INTO public.users (id, name, email, role, warning_count, is_banned)
VALUES ('USER_ID_HERE', 'Admin User', 'admin@gmail.com', 'admin', 0, false);
```

## Step 6: Test the Integration

1. Open your application in a browser
2. Try signing up a new user
3. Check Supabase dashboard to verify:
   - User appears in **Authentication** > **Users**
   - User profile appears in `users` table
4. Try creating a booking
5. Verify booking appears in `bookings` table

## Data Migration (Optional)

If you have existing data in localStorage, you can migrate it:

1. Open browser console (F12)
2. Run the migration script (to be created)
3. Or manually export localStorage data and import to Supabase

## Troubleshooting

### "Supabase client not initialized"
- Make sure Supabase script is loaded before other scripts
- Check browser console for errors
- Verify Supabase URL and key in `js/supabase-config.js`

### "Row Level Security policy violation"
- Check that RLS policies are correctly set up
- Verify user is authenticated
- Check user role matches policy requirements

### "Table does not exist"
- Run the SQL schema again
- Check table names match exactly (case-sensitive)

## Security Notes

1. **Never commit** your Supabase service role key to version control
2. The anon key is safe to use in client-side code (it's protected by RLS)
3. Row Level Security (RLS) is enabled on all tables
4. Users can only access their own data unless they're admins

## Next Steps

- Set up email templates for authentication
- Configure storage buckets for images (before/after photos)
- Set up database backups
- Monitor usage in Supabase dashboard

## Support

For issues:
1. Check Supabase dashboard logs
2. Check browser console for errors
3. Verify all SQL was executed successfully
4. Check RLS policies match your use case

