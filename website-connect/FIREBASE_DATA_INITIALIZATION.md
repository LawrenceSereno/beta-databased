# Firebase Realtime Database - Data Initialization Guide

## Overview

Firebase Realtime Database uses **JSON**, not SQL. I've created files to help you initialize your database with default data.

## Files Created

1. **`firebase-initial-data.json`** - JSON file with all initial data (can be imported manually)
2. **`js/firebase-init-data.js`** - JavaScript script to initialize data programmatically

## Method 1: Import JSON File (Easiest)

### Step 1: Prepare the JSON file
The file `firebase-initial-data.json` contains all your initial data in the correct format.

### Step 2: Import to Firebase
1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Select your project: **testing-6398b**
3. Go to **Realtime Database** → **Data**
4. Click the **⋮** (three dots) menu → **Import JSON**
5. Select `firebase-initial-data.json`
6. Click **Import**

**⚠️ Warning:** This will **overwrite** all existing data! Make sure you want to do this.

## Method 2: Use JavaScript Script (Recommended)

### Step 1: Add script to your HTML
Add this to any HTML page (or create a separate admin page):

```html
<script type="module" src="js/firebase-config.js"></script>
<script type="module" src="js/firebase-init-data.js"></script>
```

### Step 2: Run the initialization
Open browser console (F12) and run:

```javascript
await initializeFirebaseData();
```

Or create a button in your HTML:

```html
<button onclick="initializeFirebaseData()">Initialize Firebase Data</button>
```

### Step 3: Verify
Check Firebase Console → Realtime Database → Data
- You should see `packages` with 6 packages
- You should see `groomers` with 5 groomers
- Other collections should be empty objects `{}`

## Method 3: Manual Entry (For Testing)

1. Go to Firebase Console → Realtime Database → Data
2. Click **+** to add nodes
3. Manually add data following the structure in `firebase-initial-data.json`

## Data Structure

Your Firebase database will have this structure:

```
testing-6398b-default-rtdb/
├── packages/
│   ├── full-basic/
│   ├── full-styled/
│   ├── bubble-bath/
│   ├── single-service/
│   ├── addon-toothbrush/
│   └── addon-dematting/
├── groomers/
│   ├── groomer-sam/
│   ├── groomer-jom/
│   ├── groomer-botchoy/
│   ├── groomer-jinold/
│   └── groomer-ejay/
├── bookings/          (empty initially)
├── users/             (empty initially - will be created when users sign up)
├── customerProfiles/  (empty initially)
├── staffAbsences/     (empty initially)
├── bookingHistory/    (empty initially)
└── calendarBlackouts/ (empty initially)
```

## Creating Admin User

After initializing data, you need to create an admin user:

### Option 1: Through Firebase Console
1. Go to **Authentication** → **Users**
2. Click **Add user** → **Create new user**
3. Enter:
   - Email: `admin@gmail.com`
   - Password: `admin12345`
   - Auto Confirm: ✅
4. Copy the **User ID** (UID)
5. Go to **Realtime Database** → **Data** → **users**
6. Add new node with the UID as key:
   ```json
   {
     "id": "YOUR_USER_ID_HERE",
     "name": "Admin User",
     "email": "admin@gmail.com",
     "role": "admin",
     "warnings": 0,
     "isBanned": false,
     "createdAt": 1234567890
   }
   ```

### Option 2: Through Your App
1. Sign up normally through your app
2. Go to Firebase Console → Realtime Database → users
3. Find your user and change `role` from `"customer"` to `"admin"`

## Verifying Data

After initialization, verify:

1. **Packages:**
   - Go to Firebase Console → Realtime Database → packages
   - Should see 6 packages

2. **Groomers:**
   - Go to Firebase Console → Realtime Database → groomers
   - Should see 5 groomers

3. **Test in App:**
   - Go to `booking.html`
   - Packages should load
   - Groomers should be available

## Troubleshooting

### "Firebase Database not initialized"
- Make sure `js/firebase-config.js` loads first
- Check browser console for errors
- Verify Firebase config is correct

### "Permission denied"
- Update Security Rules (see FIREBASE_SETUP_INSTRUCTIONS.md)
- Make sure you're authenticated (for write operations)

### "Data not showing in app"
- Check browser console for errors
- Verify data exists in Firebase Console
- Make sure Security Rules allow read access

## Next Steps

1. ✅ Initialize default data (packages, groomers)
2. ✅ Create admin user
3. ✅ Test signup/login
4. ✅ Test booking creation
5. ✅ Verify data appears in Firebase Console

## Notes

- **Packages and groomers** are initialized once
- **Users, bookings, etc.** are created dynamically as users interact with the app
- **Data syncs** between Firebase and localStorage as backup
- **Security Rules** control who can read/write data

Your Firebase database is now ready! 🎉

