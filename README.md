# n8n-customeroutreach

## Database Setup

This project requires two tables in Supabase: `companies` and `contacts`. Navigate to the SQL Editor in your Supabase dashboard and run the following script to create the schema.

```sql
-- Create companies table
CREATE TABLE companies (
    id text PRIMARY KEY,
    name text,
    website text,
    branche text,
    pain_point text,
    booking_mode text,
    opening_hours_analysis text,
    created_at timestamptz DEFAULT now(),
    general_email text,
    status text,
    email_draft text,
    lifecycle_stage text,
    is_paying_customer boolean,
    product_tier text,
    account_manager text
);

-- Create contacts table
CREATE TABLE contacts (
    id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id text REFERENCES companies(id),
    full_name text,
    role text,
    email text,
    created_at timestamptz DEFAULT now(),
    status text,
    email_draft text,
    "Company_name" text
);
```
### Row Level Security (RLS) Policies

To secure the database, enable RLS on both tables and apply the following baseline policies. These policies restrict all operations (Select, Insert, Update, Delete) to authenticated users. Execute this script in the Supabase SQL Editor:

```sql
-- Enable RLS on both tables
ALTER TABLE companies ENABLE ROW LEVEL SECURITY;
ALTER TABLE contacts ENABLE ROW LEVEL SECURITY;

-- Policies for companies table
CREATE POLICY "Allow authenticated SELECT on companies" 
    ON companies FOR SELECT TO authenticated USING (true);

CREATE POLICY "Allow authenticated INSERT on companies" 
    ON companies FOR INSERT TO authenticated WITH CHECK (true);

CREATE POLICY "Allow authenticated UPDATE on companies" 
    ON companies FOR UPDATE TO authenticated USING (true) WITH CHECK (true);

CREATE POLICY "Allow authenticated DELETE on companies" 
    ON companies FOR DELETE TO authenticated USING (true);

-- Policies for contacts table
CREATE POLICY "Allow authenticated SELECT on contacts" 
    ON contacts FOR SELECT TO authenticated USING (true);

CREATE POLICY "Allow authenticated INSERT on contacts"
    ON contacts FOR INSERT TO authenticated WITH CHECK (true);

CREATE POLICY "Allow authenticated UPDATE on contacts" 
    ON contacts FOR UPDATE TO authenticated USING (true) WITH CHECK (true);

CREATE POLICY "Allow authenticated DELETE on contacts" 
    ON contacts FOR DELETE TO authenticated USING (true);

```
## Loom Video
https://www.loom.com/share/368517bfc9fa48d487987bf5a99e57bc
