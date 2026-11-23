# JisrPay — Next.js + Supabase

## 1. Supabase
1. Create a project at supabase.com. Run `supabase/schema.sql` in the SQL Editor.
2. Authentication > Providers: Email is on (use the 6-digit code template: put `{{ .Token }}` in the Magic Link/OTP email template).
   For phone login, enable Phone and connect an SMS provider (e.g. Twilio).
3. Settings > API: copy the Project URL, anon key, and service_role key.

## 2. Local
    cp .env.example .env.local   # fill the values
    npm install && npm run dev

## 3. Vercel
Import the repo, add every variable from `.env.example` in Project Settings > Environment Variables, deploy.
`vercel.json` runs `/api/cron/update` daily (05:00 UTC). Vercel sends `Authorization: Bearer $CRON_SECRET` automatically.
Run it once by hand to fill the first rates: `curl -H "Authorization: Bearer YOUR_SECRET" https://YOUR-SITE/api/cron/update`

## 4. First admin
Open /account, log in with your email, then run the commented `update ... role = 'admin'` line at the end of schema.sql.

## Providers
- Rates: open.er-api.com (no key). Gold: GOLD_API_KEY (goldapi.io or any provider; edit parsing in route.js). News: NEWS_API_KEY (GNews). Check each provider's terms and free-tier limits.
- Never put SUPABASE_SERVICE_ROLE_KEY in client code.
