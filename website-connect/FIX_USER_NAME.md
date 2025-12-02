# Fix User Name Display Issue

## Problem
User name "james" is showing as "Customer" on the dashboard.

## Quick Fix - Check Firebase Console

1. **Go to Firebase Console:**
   - https://console.firebase.google.com/project/testing-6398b/database/testing-6398b-default-rtdb/data

2. **Navigate to:** `users` → Find your user's UID

3. **Check the user profile:**
   ```json
   {
     "id": "YOUR_UID",
     "name": "james",  // ← Make sure this exists and has the correct value
     "email": "your-email@example.com",
     "role": "customer",
     "warnings": 0,
     "isBanned": false,
     "createdAt": 1234567890
   }
   ```

4. **If `name` is missing or wrong:**
   - Click on the user node
   - Add/edit the `name` field
   - Set value to: `"james"`
   - Click outside to save

5. **Clear browser cache:**
   - Open browser console (F12)
   - Run: `localStorage.clear()`
   - Refresh the page
   - Log in again

## Debug Steps

1. **Open browser console (F12)**
2. **Go to customer dashboard**
3. **Check console logs:**
   - Look for: "Current user data:"
   - Look for: "User name:"
   - Look for: "User profile from Firebase:"

4. **If name is missing in Firebase:**
   - The console will show: `"User name: undefined"` or `"User name: null"`
   - Fix it in Firebase Console (see above)

5. **If name exists in Firebase but not showing:**
   - Check console for errors
   - Try clearing localStorage: `localStorage.clear()`
   - Refresh and log in again

## Verify Fix

After updating Firebase:
1. Clear localStorage: `localStorage.clear()` in console
2. Refresh page
3. Log in again
4. Dashboard should show: "Welcome back, **james**!"

## If Still Not Working

Check the console logs and share:
- What does "Current user data:" show?
- What does "User name:" show?
- What does "User profile from Firebase:" show?

This will help identify the exact issue.

