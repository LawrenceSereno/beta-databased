# Supabase Schema Fix - Duplicate Policy Names

## 🔴 Problem

The error occurred because **PostgreSQL requires policy names to be unique across the entire database**, not just per table.

### Duplicate Policy Names Found:

1. **"Users can view their own profile"**
   - Used for `users` table (line 155)
   - Used for `customer_profiles` table (line 315) ❌ DUPLICATE

2. **"Users can update their own profile"**
   - Used for `users` table (line 159)
   - Used for `customer_profiles` table (line 319 - INSERT) ❌ DUPLICATE
   - Used for `customer_profiles` table (line 323 - UPDATE) ❌ DUPLICATE

3. **"Admins can view all profiles"**
   - Used for `users` table (line 163)
   - Used for `customer_profiles` table (line 327) ❌ DUPLICATE

---

## ✅ Solution Applied

All policy names have been made unique by adding table-specific prefixes:

### Before (BROKEN):
```sql
CREATE POLICY "Users can view their own profile" ON public.users ...
CREATE POLICY "Users can view their own profile" ON public.customer_profiles ... ❌
```

### After (FIXED):
```sql
CREATE POLICY "Users: Users can view their own profile" ON public.users ...
CREATE POLICY "Customer profiles: Users can view their own profile" ON public.customer_profiles ... ✅
```

---

## 📋 All Policy Names Updated

### Users Table:
- ✅ `"Users: Users can view their own profile"`
- ✅ `"Users: Users can update their own profile"`
- ✅ `"Users: Admins can view all users"`
- ✅ `"Users: Admins can update all users"`

### Groomers Table:
- ✅ `"Groomers: Anyone can view groomers"`
- ✅ `"Groomers: Admins can manage groomers"`

### Packages Table:
- ✅ `"Packages: Anyone can view packages"`
- ✅ `"Packages: Admins can manage packages"`

### Bookings Table:
- ✅ `"Bookings: Users can view their own bookings"`
- ✅ `"Bookings: Users can create their own bookings"`
- ✅ `"Bookings: Users can update their own bookings"`
- ✅ `"Bookings: Admins and groomers can view all bookings"`
- ✅ `"Bookings: Admins and groomers can update all bookings"`

### Staff Absences Table:
- ✅ `"Staff absences: Groomers can view their own absences"`
- ✅ `"Staff absences: Groomers can create their own absences"`
- ✅ `"Staff absences: Admins can view all absences"`
- ✅ `"Staff absences: Admins can manage all absences"`

### Booking History Table:
- ✅ `"Booking history: Users can view history of their bookings"`
- ✅ `"Booking history: Admins and groomers can view all history"`
- ✅ `"Booking history: System can insert booking history"`

### Calendar Blackouts Table:
- ✅ `"Calendar blackouts: Anyone can view calendar blackouts"`
- ✅ `"Calendar blackouts: Admins can manage calendar blackouts"`

### Customer Profiles Table:
- ✅ `"Customer profiles: Users can view their own profile"`
- ✅ `"Customer profiles: Users can insert their own profile"`
- ✅ `"Customer profiles: Users can update their own profile"`
- ✅ `"Customer profiles: Admins can view all profiles"`

---

## 🔧 How to Fix Existing Database

If you've already run part of the schema and have duplicate policies:

### Option 1: Drop Existing Policies First

Run this SQL to drop all existing policies, then run the full schema:

```sql
-- Drop all existing policies
DO $$ 
DECLARE
    r RECORD;
BEGIN
    FOR r IN (SELECT schemaname, tablename, policyname 
              FROM pg_policies 
              WHERE schemaname = 'public') 
    LOOP
        EXECUTE format('DROP POLICY IF EXISTS %I ON %I.%I', 
                       r.policyname, r.schemaname, r.tablename);
    END LOOP;
END $$;
```

Then run the updated `supabase-schema.sql` file.

### Option 2: Use CREATE OR REPLACE (Not Available)

**Note**: PostgreSQL doesn't support `CREATE OR REPLACE` for policies. You must `DROP POLICY` first, then `CREATE POLICY`.

### Option 3: Drop Specific Duplicates

If you know which policies are duplicates, drop them individually:

```sql
DROP POLICY IF EXISTS "Users can view their own profile" ON public.customer_profiles;
DROP POLICY IF EXISTS "Users can update their own profile" ON public.customer_profiles;
DROP POLICY IF EXISTS "Admins can view all profiles" ON public.customer_profiles;
```

Then run the updated schema file.

---

## ✅ Next Steps

1. **Drop existing duplicate policies** (use Option 1 or 3 above)
2. **Run the updated `supabase-schema.sql`** file
3. **Verify policies** by checking Supabase dashboard → Authentication → Policies

---

## 🎯 Why This Happened

PostgreSQL policy names are stored in a global namespace, not per-table. Even though policies are scoped to specific tables, their **names** must be unique across the entire database.

This is similar to how function names must be unique - you can't have two functions with the same name, even if they're in different schemas (unless you use overloading with different parameters).

---

## ✅ Status

**All policy names are now unique!** The schema should run without errors. 🎉

