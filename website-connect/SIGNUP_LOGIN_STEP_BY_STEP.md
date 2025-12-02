# Signup & Login - Step by Step Guide

## 🎯 Goal
Make signup and login work with Firebase, and see users appear in Firebase Database.

---

## Step 1: Set Up Firebase Security Rules (For Signup/Login)

### Go to Firebase Console:
1. Open: https://console.firebase.google.com/
2. Select project: **testing-6398b**
3. Go to **Realtime Database** → **Rules**

### Set These Rules (Allow users to create their own profile):

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

**Click Publish**

---

## Step 2: Enable Firebase Authentication

1. In Firebase Console, go to **Authentication**
2. Click **Get Started** (if not already enabled)
3. Go to **Sign-in method** tab
4. Click on **Email/Password**
5. **Enable** it
6. Click **Save**

---

## Step 3: Test Signup

1. **Open your app** (using a web server - see HOW_TO_RUN_LOCAL_SERVER.md)
2. Go to `signup.html`
3. Fill in the form:
   - Name: Test User
   - Email: test@example.com
   - Password: test123456
4. Click **Sign Up**

### What Should Happen:
- ✅ User created in Firebase Authentication
- ✅ User profile created in Firebase Realtime Database → `users/{userId}`
- ✅ Redirected to customer dashboard

### Verify in Firebase Console:
1. Go to **Authentication** → **Users**
   - Should see: `test@example.com`
2. Go to **Realtime Database** → **Data** → **users**
   - Should see a node with the user's UID
   - Click on it to see: `name`, `email`, `role: "customer"`, etc.

---

## Step 4: Test Login

1. **Logout** (if logged in)
2. Go to `login.html`
3. Enter:
   - Email: test@example.com
   - Password: test123456
4. Click **Login**

### What Should Happen:
- ✅ Successfully logs in
- ✅ User data loaded from Firebase
- ✅ Redirected to customer dashboard

### Verify:
- Check browser console (F12) - should see user data
- Check Firebase Console → Authentication → Users (user should be active)

---

## Step 5: Check Data in Firebase

### In Firebase Console:

1. **Authentication** → **Users**
   - Lists all registered users
   - Shows email, creation date, last sign-in

2. **Realtime Database** → **Data** → **users**
   - Shows user profiles
   - Structure:
     ```
     users/
       {userId}/
         id: "abc123..."
         name: "Test User"
         email: "test@example.com"
         role: "customer"
         warnings: 0
         isBanned: false
         createdAt: 1234567890
     ```

---

## 🔧 Troubleshooting

### "Permission denied" on signup
- **Fix:** Update security rules (Step 1)
- Make sure rules allow users to write to `users/$uid` where `$uid === auth.uid`

### "Email already in use"
- User already exists
- Try a different email or login instead

### "Firebase not initialized"
- Check browser console for errors
- Make sure `js/firebase-config.js` loads before other scripts
- Verify Firebase config is correct

### User created but not in database
- Check browser console for errors
- Verify security rules allow write
- Check if there's a network error

### Can't login after signup
- Check if user exists in Firebase Authentication
- Check if user profile exists in Realtime Database
- Check browser console for errors

---

## ✅ Success Checklist

After completing all steps, you should have:

- [ ] Firebase Authentication enabled
- [ ] Security rules updated
- [ ] Can sign up new users
- [ ] Users appear in Firebase Authentication
- [ ] User profiles appear in Realtime Database
- [ ] Can login with created account
- [ ] User data loads correctly after login

---

## 📝 Next Steps (After Signup/Login Works)

1. Test creating multiple users
2. Test login with different accounts
3. Verify data persists (close browser, reopen, login again)
4. Then move on to booking functionality

---

## 🐛 Debug Commands

Open browser console (F12) and run:

```javascript
// Check if Firebase is loaded
console.log('Firebase Auth:', window.firebaseAuth);
console.log('Firebase Database:', window.firebaseDatabase);

// Check current user
const user = await getCurrentUser();
console.log('Current user:', user);

// Check Firebase Auth user
const auth = window.firebaseAuth;
console.log('Auth user:', auth?.currentUser);
```

---

Let's fix the code first, then test step by step! 🚀


