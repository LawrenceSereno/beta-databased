# 🧪 Test Signup & Login - Quick Guide

## ✅ Step 1: Set Firebase Security Rules

1. Go to: https://console.firebase.google.com/project/testing-6398b/database/testing-6398b-default-rtdb/rules
2. Replace the rules with:

```json
{
  "rules": {
    "users": {
      "$uid": {
        ".read": "$uid === auth.uid || (auth != null && root.child('users').child(auth.uid).child('role').val() === 'admin')",
        ".write": "$uid === auth.uid || (auth != null && root.child('users').child(auth.uid).child('role').val() === 'admin')"
      },
      ".read": "auth != null",
      ".write": "auth != null"
    },
    "packages": {
      ".read": true,
      ".write": false
    },
    "groomers": {
      ".read": true,
      ".write": false
    }
  }
}
```

3. Click **Publish**

---

## ✅ Step 2: Enable Email/Password Authentication

1. Go to: https://console.firebase.google.com/project/testing-6398b/authentication/providers
2. Click **Email/Password**
3. **Enable** it
4. Click **Save**

---

## ✅ Step 3: Start Local Server

**Option A: Using Python**
```bash
# Python 3
python -m http.server 8000

# Python 2
python -m SimpleHTTPServer 8000
```

**Option B: Using Node.js**
```bash
npx http-server -p 8000
```

**Option C: Using VS Code**
- Install "Live Server" extension
- Right-click `signup.html` → "Open with Live Server"

Then open: **http://localhost:8000/signup.html**

---

## ✅ Step 4: Test Signup

1. Open `signup.html` in browser (via local server)
2. Fill the form:
   - **Name:** Test User
   - **Email:** test@example.com
   - **Password:** test123456
3. Click **Sign Up**

### Expected Result:
- ✅ No errors in browser console (F12)
- ✅ Redirected to `customer-dashboard.html`
- ✅ User appears in Firebase Console → Authentication → Users
- ✅ User profile appears in Firebase Console → Realtime Database → users → {userId}

### Check Firebase Console:
1. **Authentication → Users**
   - Should see: `test@example.com`
   - UID: something like `abc123...`

2. **Realtime Database → Data → users**
   - Click on the user's UID
   - Should see:
     ```json
     {
       "id": "abc123...",
       "name": "Test User",
       "email": "test@example.com",
       "role": "customer",
       "warnings": 0,
       "isBanned": false,
       "createdAt": 1234567890
     }
     ```

---

## ✅ Step 5: Test Login

1. **Logout** (if logged in) or open `login.html` in a new incognito window
2. Enter:
   - **Email:** test@example.com
   - **Password:** test123456
3. Click **Login**

### Expected Result:
- ✅ No errors in browser console
- ✅ Redirected to `customer-dashboard.html`
- ✅ User data loads correctly

### Check Browser Console (F12):
```javascript
// Should show user data
const user = await getCurrentUser();
console.log('Current user:', user);
```

---

## 🐛 Troubleshooting

### Error: "Permission denied"
- **Fix:** Make sure security rules are updated (Step 1)
- Check that rules allow `users/$uid` write when `$uid === auth.uid`

### Error: "Email already in use"
- User already exists
- Try different email or login instead

### Error: "Firebase not initialized"
- Check browser console
- Make sure `js/firebase-config.js` loads before other scripts
- Verify scripts load in this order:
  1. `firebase-config.js`
  2. `firebase-db.js`
  3. `main.js`
  4. `auth.js`

### User created but not in database
- Check browser console for errors
- Verify security rules allow write
- Check network tab for failed requests

### Can't login after signup
- Check if user exists in Firebase Authentication
- Check if user profile exists in Realtime Database
- Try logging out and logging in again

---

## 📊 Success Checklist

- [ ] Firebase Authentication enabled
- [ ] Security rules updated
- [ ] Can sign up new user
- [ ] User appears in Firebase Authentication
- [ ] User profile appears in Realtime Database
- [ ] Can login with created account
- [ ] User data loads after login
- [ ] No console errors

---

## 🎯 Next Steps

Once signup/login works:
1. Test with multiple users
2. Test logout
3. Test login persistence (close browser, reopen, login)
4. Then move to booking functionality

---

## 🔍 Debug Commands

Open browser console (F12) and run:

```javascript
// Check Firebase
console.log('Auth:', window.firebaseAuth);
console.log('Database:', window.firebaseDatabase);

// Check current user
const user = await getCurrentUser();
console.log('User:', user);

// Check Firebase Auth user
console.log('Auth user:', window.firebaseAuth?.currentUser);

// Check localStorage
console.log('localStorage user:', localStorage.getItem('currentUser'));
```

---

**Ready to test!** 🚀

