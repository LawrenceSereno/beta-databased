# Quick Fix Checklist for Auth & Booking Issues

## ✅ What I Just Fixed

1. **Better Error Handling in Auth Functions**
   - Added checks for Supabase client availability
   - Added error messages for missing functions
   - Improved error logging

2. **Fixed Async/Await Issues**
   - Made `submitBooking` properly async
   - Added safety checks before calling async functions

3. **Improved Function Availability Checks**
   - Added checks for `getCurrentUser`, `setCurrentUser`, `redirect` before use
   - Added fallback redirects if functions aren't available

4. **Better Error Messages**
   - More descriptive error messages
   - Console logging for debugging

---

## 🔍 How to Debug

### Step 1: Open Browser Console (F12)

Look for these errors:
- ❌ "Supabase library not loaded"
- ❌ "getCurrentUser is not a function"
- ❌ "Supabase client not available"
- ❌ Network errors (CORS, 401, 403, etc.)

### Step 2: Test Supabase Connection

In browser console, run:
```javascript
console.log('Supabase client:', getSupabaseClient());
```

**Expected:** Should return an object, not `null`

### Step 3: Test Authentication

In browser console, run:
```javascript
const supabase = getSupabaseClient();
const { data, error } = await supabase.auth.getSession();
console.log('Session:', data);
console.log('Error:', error);
```

**Expected:** Should show session data or null (if not logged in)

### Step 4: Check Script Loading Order

Open Network tab (F12) and verify scripts load in this order:
1. ✅ `@supabase/supabase-js@2` (CDN)
2. ✅ `js/supabase-config.js`
3. ✅ `js/supabase-db.js`
4. ✅ `js/main.js`
5. ✅ `js/auth.js` (for login/signup pages)
6. ✅ `js/booking.js` (for booking page)

---

## 🐛 Common Issues & Solutions

### Issue: "Supabase client not available"
**Solution:**
1. Check if Supabase CDN is accessible
2. Check browser console for network errors
3. Verify Supabase URL and key in `js/supabase-config.js`

### Issue: "getCurrentUser is not a function"
**Solution:**
1. Check if `js/supabase-db.js` is loading
2. Check script order in HTML
3. Hard refresh: Ctrl+Shift+R

### Issue: Signup/Login form does nothing
**Solution:**
1. Check browser console for errors
2. Verify form IDs: `loginForm`, `signupForm`
3. Check if event listeners are attached (should see in console on page load)

### Issue: Can't create booking
**Solution:**
1. Check if user is logged in: `await getCurrentUser()`
2. Check browser console for errors
3. Verify RLS policies allow INSERT into bookings table
4. Check if packages and groomers are loaded

---

## 🧪 Test Signup Manually

In browser console:
```javascript
const supabase = getSupabaseClient();
const { data, error } = await supabase.auth.signUp({
  email: 'test@example.com',
  password: 'test123456'
});
console.log('Signup result:', data);
console.log('Signup error:', error);
```

**Expected:** Should create user in `auth.users` table

---

## 🧪 Test Login Manually

In browser console:
```javascript
const supabase = getSupabaseClient();
const { data, error } = await supabase.auth.signInWithPassword({
  email: 'test@example.com',
  password: 'test123456'
});
console.log('Login result:', data);
console.log('Login error:', error);
```

**Expected:** Should return session with user data

---

## 🧪 Test Booking Creation

In browser console (after logging in):
```javascript
const user = await getCurrentUser();
console.log('Current user:', user);

const supabase = getSupabaseClient();
const { data, error } = await supabase
  .from('bookings')
  .insert([{
    user_id: user.id,
    pet_name: 'Test Pet',
    pet_type: 'dog',
    date: '2024-12-25',
    time: '10:00',
    phone: '1234567890',
    customer_name: user.name,
    package_name: 'Test Package',
    status: 'pending'
  }]);
console.log('Booking result:', data);
console.log('Booking error:', error);
```

**Expected:** Should create booking in `bookings` table

---

## 📋 Next Steps

1. **Open browser console** and check for errors
2. **Try signup** and watch console for errors
3. **Try login** and watch console for errors
4. **Try booking** and watch console for errors
5. **Share any error messages** you see in console

---

## 🔗 Files Modified

- ✅ `js/supabase-config.js` - Better error handling
- ✅ `js/auth.js` - Improved signup/login error handling
- ✅ `js/booking.js` - Fixed async issues, better error handling

---

## 💡 Still Having Issues?

1. **Clear browser cache** (Ctrl+Shift+Delete)
2. **Hard refresh** (Ctrl+Shift+R)
3. **Check Supabase dashboard** - verify tables and policies exist
4. **Check network tab** - look for failed requests
5. **Share console errors** - copy/paste any red error messages

