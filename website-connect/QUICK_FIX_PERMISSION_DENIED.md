# Quick Fix: "Permission Denied" Error

## 🔴 Problem
You're getting "Permission denied" when trying to initialize Firebase data.

## ✅ Solution (2 Minutes)

### Step 1: Open Firebase Console
1. Go to: https://console.firebase.google.com/
2. Select project: **testing-6398b**
3. Click **Realtime Database** (left sidebar)
4. Click **Rules** tab (at the top)

### Step 2: Set Temporary Test Rules
Copy and paste this into the Rules editor:

```json
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
```

### Step 3: Publish
1. Click **Publish** button
2. Wait 5 seconds

### Step 4: Initialize Data
1. Go back to your initialization page
2. Click **"Initialize Firebase Data"** button
3. Should work now! ✅

### Step 5: Set Secure Rules (After Initialization)
After data is initialized, come back and replace with secure rules (see FIREBASE_SECURITY_RULES_FOR_INIT.md)

---

## Why This Works

The test rules allow anyone to read/write temporarily. This lets the initialization script create the data. After that, you should switch to secure rules.

---

## Visual Guide

```
Firebase Console
  └─ Realtime Database
      └─ Rules tab
          └─ Paste test rules
              └─ Publish
                  └─ Initialize data ✅
```

That's it! 🎉

