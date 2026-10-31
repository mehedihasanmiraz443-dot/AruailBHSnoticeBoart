ARUAIL BHS Smart Notice Board — Free deployment edition
========================================================

This package contains the website frontend plus a Supabase-backed admin flow.
It is NOT live yet: you must create the free Supabase project and publish the files.
No real admin username/password has been created by this package, and no default password is provided.

FILES
-----
index.html, style.css, script.js, config.js
assets/aruail-bhs-school-logo.jpg
supabase-setup.sql

FREE HOSTING PATH (no paid plan required for the initial setup)
---------------------------------------------------------------
A. Set up Supabase (database, login and PDF storage)
1. Create a project at https://supabase.com/ and choose the Free plan.
2. Open Project Settings / API (or Connect) and copy the Project URL and anon/public key.
3. Edit config.js and replace YOUR_SUPABASE_PROJECT_URL and YOUR_SUPABASE_ANON_PUBLIC_KEY.
   These are public client values. NEVER put a service_role/secret key in config.js or GitHub.
4. In Supabase SQL Editor, run all of supabase-setup.sql.
5. Go to Authentication > Users and create your admin user with an email you control and a strong unique password.
6. Copy that user's UUID, then run this in SQL Editor (replace both values):
   INSERT INTO public.school_admins (user_id)
   VALUES ('PASTE-USER-UUID-HERE');
   -- alternatively use: select id from auth.users where email='your-email@example.com'
   -- in the INSERT...SELECT query shown at the bottom of supabase-setup.sql.
7. In Authentication settings, disable public sign-ups if you do not need registration.
8. Open the website, ডেস্কটপে উপরের বাম দিকের স্কুলের লোগোতে ডাবল-ক্লিক করুন; মোবাইলে একই লোগোতে দ্রুত ডাবল-ট্যাপ করুন। তারপর অ্যাডমিন ইমেইল/পাসওয়ার্ড দিয়ে লগইন করুন।
   Password changes are available inside the admin panel.

B. Publish free with GitHub Pages
1. Create/sign in to https://github.com/ and create a repository, e.g. aruail-bhs-notice-board.
2. Upload the CONTENTS of this folder (index.html, style.css, script.js, config.js, supabase-setup.sql and assets folder).
3. In repository Settings > Pages, choose Deploy from a branch, select main and /(root), then Save.
4. Wait for the published URL shown by GitHub Pages. Test the site from a phone/mobile network.
5. Do not upload any Supabase service_role key, passwords, private student data, or secret tokens.

ADMIN SECURITY
--------------
- There is no visible admin/settings button. Admin login opens by double-clicking (desktop) or quickly double-tapping (mobile) the top-left school logo. This is obscurity only; Supabase Auth and RLS are the actual security boundary.
- Supabase Auth handles password authentication; database Row Level Security (RLS) protects writes.
- Only user IDs explicitly listed in public.school_admins can create/update/delete notices or upload/delete PDFs.
- Public visitors can read published notices and PDFs.
- The anon/public key is designed to be visible in browser code; RLS is essential.
- Never share your admin password with me or put it in the source code.
- This setup does not include MFA, audit dashboard, scheduled backups, or a custom domain. Check the current Supabase Free plan quotas and backup/export options.
- Admin account recovery depends on your Supabase Auth settings/email configuration.
- PDF links are public; upload only notices intended for public access.

BEFORE ANNOUNCING THE SITE
--------------------------
- Replace sample/demo notices with approved school notices. This site does not publish fake sample notices once Supabase is configured; an empty database shows an empty notice state.
- Verify school name, address, contact information and external official link.
- Test admin login, adding a notice, viewing it in a private/incognito window, deleting a test notice, and password change.
- Verify the live GitHub Pages URL and HTTPS.
- The site is a static frontend with Supabase as the backend. “Free” depends on current provider quotas and policies; custom domain purchase is optional, not included.


ত্রুটি নির্ণয়
-------------
অ্যাডমিনে নোটিশ লোড না হলে এখন প্রকৃত Supabase error message দেখাবে। সেটির লেখা কপি করে সহায়তায় পাঠান; Secret key বা database password পাঠাবেন না। প্রকাশিত নোটিশ পেজ খোলা থাকলে প্রতি ৩০ সেকেন্ডে ডেটা রিফ্রেশ হবে।
