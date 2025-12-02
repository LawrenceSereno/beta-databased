# Troubleshooting Auth & Booking Issues

## Common Issues and Fixes

### Issue 1: Supabase Client Not Initializing
**Symptoms:** Can't sign up, sign in, or book

**Check:**
1. Open browser console (F12)
2. Look for error: "Supabase library not loaded"
3. Check if Supabase CDN is accessible

**Fix:** Make sure Supabase script loads before other scripts:
```html
<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
<script src="js/supabase-config.js"></script>
<script src="js/supabase-db.js"></script>
```

### Issue 2: CORS Errors
**Symptoms:** Network errors in console, requests blocked

**Fix:** Check Supabase dashboard:
1. Go to Settings > API
2. Verify CORS settings allow your domain
3. Add your domain to allowed origins

### Issue 3: RLS Policies Blocking Operations
**Symptoms:** Signup works but can't insert into users table

**Check:**
1. Verify RLS policies are created
2. Check if user has permission to INSERT into users table
3. Verify policies allow INSERT for new users

**Fix:** The signup should create user in auth.users first, then insert into public.users. If this fails, check:
- User ID matches between auth.users and public.users
- RLS policy allows INSERT for authenticated users

### Issue 4: Form Event Listeners Not Attaching
**Symptoms:** Form submission does nothing

**Check:**
1. Open console and check for errors
2. Verify form IDs match: `loginForm`, `signupForm`
3. Check if scripts load in correct order

### Issue 5: getCurrentUser Not Available
**Symptoms:** "getCurrentUser is not a function" error

**Fix:** Make sure `supabase-db.js` loads before `auth.js`

---

## Debugging Steps

1. **Open Browser Console (F12)**
   - Check for JavaScript errors
   - Look for Supabase-related errors
   - Check network tab for failed requests

2. **Test Supabase Connection**
   ```javascript
   // In browser console:
   console.log(getSupabaseClient());
   // Should return Supabase client object, not null
   ```

3. **Test Authentication**
   ```javascript
   // In browser console:
   const supabase = getSupabaseClient();
   const { data, error } = await supabase.auth.getSession();
   console.log('Session:', data, 'Error:', error);
   ```

4. **Check Database Tables**
   - Go to Supabase dashboard
   - Check if tables exist
   - Verify data can be inserted manually

5. **Check RLS Policies**
   - Go to Authentication > Policies
   - Verify policies exist for all tables
   - Check if policies allow necessary operations

---

## Quick Fixes to Try

1. **Clear Browser Cache**
   - Hard refresh: Ctrl+Shift+R (Windows) or Cmd+Shift+R (Mac)

2. **Check Script Loading Order**
   - Supabase library must load first
   - Then supabase-config.js
   - Then supabase-db.js
   - Then main.js
   - Finally auth.js

3. **Verify Supabase Credentials**
   - Check SUPABASE_URL in supabase-config.js
   - Check SUPABASE_ANON_KEY
   - Verify these match your Supabase project

4. **Test with Console Commands**
   ```javascript
   // Test signup manually:
   const supabase = getSupabaseClient();
   const { data, error } = await supabase.auth.signUp({
     email: 'test@example.com',
     password: 'test123456'
   });
   console.log(data, error);
   ```

