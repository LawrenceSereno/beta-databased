# Next Steps After Schema Setup ✅

## 🎉 Schema Successfully Created!

Your database tables, policies, and triggers are now set up. Here's what to do next:

---

## Step 1: Initialize Default Data

You need to populate your database with initial data. Run these SQL queries in your Supabase SQL Editor:

### 1.1 Insert Service Packages

```sql
INSERT INTO public.packages (id, name, type, duration, includes, tiers) VALUES
('full-basic', '✂️ Full Package · Basic', 'any', 75, 
 '["Bath & Dry", "Brush / De-Shedding", "Hair Cut (Basic)", "Nail Trim", "Ear Clean", "Foot Pad Clean", "Cologne"]'::jsonb,
 '[{"label": "5kg & below", "price": 530}, {"label": "5.1 – 8kg", "price": 630}, {"label": "8.1 – 15kg", "price": 750}, {"label": "15.1 – 30kg", "price": 800}, {"label": "30kg & above", "price": 920}]'::jsonb)
ON CONFLICT (id) DO NOTHING;

INSERT INTO public.packages (id, name, type, duration, includes, tiers) VALUES
('full-styled', '✂️ Full Package · Trimming & Styling', 'any', 90,
 '["Bath & Dry", "Brush / De-Shedding", "Hair Cut (Styled)", "Nail Trim", "Ear Clean", "Foot Pad Clean", "Cologne"]'::jsonb,
 '[{"label": "5kg & below", "price": 630}, {"label": "5.1 – 8kg", "price": 730}, {"label": "8.1 – 15kg", "price": 880}, {"label": "15.1 – 30kg", "price": 930}, {"label": "30kg & above", "price": 1050}]'::jsonb)
ON CONFLICT (id) DO NOTHING;

INSERT INTO public.packages (id, name, type, duration, includes, tiers) VALUES
('bubble-bath', '🧴 Shampoo Bath ''n Bubble', 'any', 60,
 '["Bath & Dry", "Brush / De-Shedding", "Hygiene Trim", "Nail Trim", "Ear Clean", "Foot Pad Clean", "Cologne"]'::jsonb,
 '[{"label": "5kg & below", "price": 350}, {"label": "5.1 – 8kg", "price": 450}, {"label": "8.1 – 15kg", "price": 550}, {"label": "15.1 – 30kg", "price": 600}, {"label": "30kg & above", "price": 700}]'::jsonb)
ON CONFLICT (id) DO NOTHING;

INSERT INTO public.packages (id, name, type, duration, includes, tiers) VALUES
('single-service', '🚿 Single Service · Mix & Match', 'any', 45,
 '["Choose from Nail Trim, Ear Clean, or Hygiene Focus", "Add to any package as needed"]'::jsonb,
 '[{"label": "Nail Trim 5kg & below", "price": 50}, {"label": "Nail Trim 30kg & above", "price": 80}, {"label": "Ear Clean 5kg & below", "price": 70}, {"label": "Ear Clean 30kg & above", "price": 90}]'::jsonb)
ON CONFLICT (id) DO NOTHING;

INSERT INTO public.packages (id, name, type, duration, includes, tiers) VALUES
('addon-toothbrush', '🛁 Add-on · Toothbrush', 'addon', 5,
 '["Individual toothbrush to bring home"]'::jsonb,
 '[{"label": "Per item", "price": 25}]'::jsonb)
ON CONFLICT (id) DO NOTHING;

INSERT INTO public.packages (id, name, type, duration, includes, tiers) VALUES
('addon-dematting', '🛁 Add-on · De-matting', 'addon', 25,
 '["Targeted de-matting service"]'::jsonb,
 '[{"label": "Light tangles", "price": 80}, {"label": "Heavy tangles", "price": 250}]'::jsonb)
ON CONFLICT (id) DO NOTHING;
```

### 1.2 Insert Groomers

```sql
INSERT INTO public.groomers (id, name, specialty, max_daily_bookings) VALUES
('groomer-sam', 'Sam', 'Small breed specialist', 3),
('groomer-jom', 'Jom', 'Double-coat care', 3),
('groomer-botchoy', 'Botchoy', 'Creative trims & styling', 3),
('groomer-jinold', 'Jinold', 'Senior pet handler', 3),
('groomer-ejay', 'Ejay', 'Cat whisperer', 3)
ON CONFLICT (id) DO NOTHING;
```

---

## Step 2: Create Admin User

### Option A: Create via Supabase Dashboard (Recommended)

1. Go to **Authentication** > **Users** in Supabase dashboard
2. Click **Add user** > **Create new user**
3. Enter:
   - Email: `admin@gmail.com`
   - Password: `admin12345`
   - Auto Confirm User: ✅ (checked)
4. After creating, note the **User ID** (UUID)
5. Run this SQL (replace `USER_ID_HERE` with the actual UUID):

```sql
INSERT INTO public.users (id, name, email, role, warning_count, is_banned)
VALUES ('USER_ID_HERE', 'Admin User', 'admin@gmail.com', 'admin', 0, false)
ON CONFLICT (id) DO UPDATE SET role = 'admin';
```

### Option B: Create via SQL (If you have service role key)

```sql
-- This requires service role key - use Option A if you don't have it
-- The user must be created in auth.users first via Supabase Auth
```

---

## Step 3: Test the Integration

### 3.1 Test User Signup

1. Open your application in browser
2. Go to `signup.html`
3. Create a test account:
   - Name: Test User
   - Email: test@example.com
   - Password: test123456
4. Check Supabase dashboard:
   - **Authentication** > **Users** - Should see new user
   - **Table Editor** > **users** - Should see user profile

### 3.2 Test Booking Creation

1. Log in with your test account
2. Go to `booking.html`
3. Complete a booking:
   - Select pet type
   - Select package
   - Select date and time
   - Fill in details
   - Submit booking
4. Check Supabase dashboard:
   - **Table Editor** > **bookings** - Should see new booking

### 3.3 Test Data Retrieval

1. Go to customer dashboard
2. Verify your booking appears
3. Check browser console (F12) for any errors

---

## Step 4: Verify Database

Check these in Supabase dashboard:

### Tables Created ✅
- [ ] `users` - Has your test user
- [ ] `groomers` - Has 5 groomers
- [ ] `packages` - Has 6 packages
- [ ] `bookings` - Has your test booking (if created)
- [ ] `customer_profiles` - Has profile (if saved)
- [ ] `staff_absences` - Empty (normal)
- [ ] `booking_history` - Has history entries (if booking created)
- [ ] `calendar_blackouts` - Empty (normal)

### Policies Active ✅
- [ ] Go to **Authentication** > **Policies**
- [ ] Verify policies are created for each table
- [ ] Check that RLS is enabled

### Triggers Active ✅
- [ ] Go to **Database** > **Functions**
- [ ] Verify `update_updated_at_column()` function exists
- [ ] Triggers should be automatically created

---

## Step 5: Optional - Migrate Existing Data

If you have existing data in localStorage that you want to migrate:

1. Open your application
2. Log in with an account that has bookings
3. Open browser console (F12)
4. Run:
   ```javascript
   await migrateLocalStorageToSupabase();
   ```
5. Check the console for migration results
6. Verify data in Supabase dashboard

---

## Step 6: Set Up Google OAuth (Optional)

If you want Google Sign-In:

1. Go to Supabase dashboard > **Authentication** > **Providers**
2. Enable **Google** provider
3. Add your Google OAuth credentials:
   - Client ID
   - Client Secret
4. Add redirect URL: `https://uizkbnggqfwvmzttwbjx.supabase.co/auth/v1/callback`

---

## 🎯 Quick Checklist

- [ ] ✅ Schema created (DONE!)
- [ ] ⬜ Packages inserted
- [ ] ⬜ Groomers inserted
- [ ] ⬜ Admin user created
- [ ] ⬜ Test user signup
- [ ] ⬜ Test booking creation
- [ ] ⬜ Verify data in Supabase
- [ ] ⬜ Test dashboard loading
- [ ] ⬜ Migrate existing data (optional)

---

## 🐛 Troubleshooting

### "No packages showing"
- Run the package INSERT statements
- Check `packages` table in Supabase

### "Can't sign up"
- Check Supabase dashboard > Authentication > Settings
- Verify email provider is enabled
- Check browser console for errors

### "Bookings not saving"
- Check browser console for errors
- Verify RLS policies allow INSERT
- Check user is authenticated

### "Dashboard shows empty"
- Check browser console for errors
- Verify data exists in Supabase
- Check network tab for API calls

---

## 🎉 You're Almost Done!

Once you complete steps 1-3, your application will be fully connected to Supabase!

**Next**: Run the package and groomer INSERT statements, then create your admin user.

