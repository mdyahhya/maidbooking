Maidly-Online Maid Booking — PWA + Supabase : Live on maidly.netlify.app
A production-style maid booking platform with customer and maid roles, real-time booking lifecycle, and installable PWA experience for Android and Windows, built with vanilla HTML/CSS/JS and Supabase for authentication and data.

Features
Role-based auth for Customers and Maids with session restoration and guarded actions per role.

Profiles: customers edit name/phone; maids edit address, experience, daily/monthly rates, bio, and photo (base64) with validation and error handling.

Booking lifecycle: customers create/cancel; maids accept/reject/complete with status chips and timestamped updates ordered by recency.

Search & browse: homepage search bar and dynamic maids grid to discover providers by name, location, or experience.

Robust UX: global loading overlay, toast notifications, history-aware SPA navigation, online/offline detection, and defensive error handlers.

PWA install: service worker, deferred install prompt, custom banner, and standalone detection for Android/Windows.

Architecture
Frontend: Single-page app (index.html) with pages for Home, Auth, Customer Dashboard, Maid Dashboard, and a modal for maid details; navigation uses history state and a custom back stack.

Backend: Supabase tables customers, maids, bookings with CRUD via select/insert/update/delete and eq filters per user id and role.

State: localStorage stores current user and type; verifyUserSession refreshes from backend; navigationHistory controls SPA back/forward behavior.

Reliability: centralized notification, loader, and error utilities; phone/email validations; graceful offline/online transitions and retries.

PWA: service-worker.js registration, beforeinstallprompt handling, install UI with “Install/Maybe later,” and appinstalled handling.

Core flows
Customer: Register/Login → Profile → Browse Maids → Create bookings → Manage/cancel pending bookings, view status updates.

Maid: Register/Login → Profile (photo/rates/bio) → Receive booking requests → Accept/Reject → Mark Confirmed → Complete.

Data model (expected)
customers: id, name, email, phone, created_at, updated_at.

maids: id, name, email, phone, address, experience, dailyrate, monthlyrate, bio, photo, created_at, updated_at.

bookings: id, customer_id, customer_name, maid_id, maid_name, status (pending|confirmed|completed|rejected), service_date, created_at, updated_at .

Getting started
Prerequisites

Supabase project (URL and anon key).

Tables as above; add basic RLS later for production (customers can read/write own profile and bookings, maids their own profile and incoming bookings).

Setup

Clone the repo and open index.html.

Replace SUPABASE_URL and SUPABASE_ANON_KEY in the Supabase client initialization block in the HTML script.

Ensure service-worker.js exists at the project root (add a basic cache-first handler if needed).

Serve over HTTP(S), not file://, so the service worker can register (e.g., http-server or VS Code Live Server).

Run locally

npm i -g http-server.

http-server -p 5173.

Open http://localhost:5173 and test register/login, profiles, and bookings.

Deploy

Host as a static site (GitHub Pages, Netlify, Vercel); ensure HTTPS so PWA install works in production.

Roadmap
Supabase Storage for images instead of base64 in table.

RLS policies for least-privilege access and production hardening.

Filters and pagination for large maid directories.

Notifications (email/WhatsApp) on booking status changes.

Tech
HTML, CSS, JavaScript (vanilla) + Supabase JS client + Service Worker/PWA APIs.

Author
Yahya Mundewadi — Developer and maintainer of One Day Maid.

License
Add LICENSE if open-sourcing; otherwise mark “All rights reserved”
