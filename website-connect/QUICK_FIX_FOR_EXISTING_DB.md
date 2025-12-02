# Quick Fix for Existing Database

## 🔴 Problem

You're getting errors because you've already run part of the schema:
- **Policies already exist** (duplicate policy names)
- **Triggers already exist** (duplicate trigger names)

## ✅ Solution

I've updated `supabase-schema.sql` to include `DROP IF EXISTS` statements before creating policies and triggers. This makes the schema **idempotent** (safe to run multiple times).

### What Changed

1. **Added DROP statements for all policies** - Removes old policies before creating new ones
2. **Added DROP statements for all triggers** - Removes old triggers before creating new ones
3. **Includes both old and new policy names** - Handles migration from old names to new names

## 🚀 How to Use

### Option 1: Run the Updated Schema (Recommended)

Just run the updated `supabase-schema.sql` file. It will:
1. Drop existing policies/triggers
2. Create new ones with unique names
3. Work even if you've run it before

### Option 2: Manual Cleanup First

If you prefer to clean up first, run this SQL:

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

-- Drop all existing triggers
DROP TRIGGER IF EXISTS update_users_updated_at ON public.users;
DROP TRIGGER IF EXISTS update_groomers_updated_at ON public.groomers;
DROP TRIGGER IF EXISTS update_packages_updated_at ON public.packages;
DROP TRIGGER IF EXISTS update_bookings_updated_at ON public.bookings;
DROP TRIGGER IF EXISTS update_staff_absences_updated_at ON public.staff_absences;
DROP TRIGGER IF EXISTS update_customer_profiles_updated_at ON public.customer_profiles;
```

Then run the updated `supabase-schema.sql`.

## ✅ Status

**The schema file is now idempotent!** You can run it multiple times without errors. 🎉

