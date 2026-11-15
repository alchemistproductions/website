# ALCHEMIST PRODUCTIONS website
Next.js 14 + Tailwind + Supabase (auth, Postgres RLS). No secret/service keys are used anywhere.

## Setup
1. **Supabase**: create a project → SQL Editor → paste & run `supabase/schema.sql`.
2. Supabase → Project Settings → API: copy *Project URL* and *anon public key*.
3. Supabase → Authentication → Providers → Email: keep **Confirm email** ON (set a custom SMTP for real traffic).
4. **GitHub**: create a repo, push this folder.
5. **Vercel**: Add New Project → import the repo → Environment Variables: `NEXT_PUBLIC_SUPABASE_URL`, `NEXT_PUBLIC_SUPABASE_ANON_KEY` → Deploy.
6. Supabase → Authentication → URL Configuration: Site URL = your Vercel URL; Redirect URLs = `https://YOUR-DOMAIN/auth/callback` (+ `http://localhost:3000/auth/callback`).
7. On the site go to `/login` → Create account with **kkanjarkar@gmail.com** → verify the email. Then run in SQL Editor:
   `insert into admins(user_id,role) select id,'super_admin' from auth.users where email='kkanjarkar@gmail.com' and email_confirmed_at is not null;`
   Now `/admin` works for that account only. Other staff: they sign up and verify first, then you add them at `/admin/team` (Super Admin only) with role Admin, Recruitment Manager or Content Manager.
8. Replace the images in `public/v/` with the original high-res posters (same file names: `011.jpg` … `001.jpg`).

Local: `npm i`, copy `.env.example` to `.env.local`, `npm run dev`.
Edit the application dropdown in `lib/data.ts` (`JOIN_ROLES`).
Department members: add rows to the `members` table (`role_slug` e.g. `video-editor`, `name`).
