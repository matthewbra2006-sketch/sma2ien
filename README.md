# سمائيين (Sma2ien) - Youth Meeting Card System

A gamified attendance and encouragement system for a university youth meeting. Each young person has a "card" level that grows as they stay committed, inspired by loyalty cards.

**Live site:** https://sma2ien.web.app

## What it does

- **Card levels:** Master, Gold, Platinum, and VIP. Levels are earned automatically from attendance at meetings, mass, confession, eftekad (visits), and Bible study. The ladder of requirements is configurable from the admin panel.
- **Live public-style board:** a clean, searchable list of everyone with their current card, plus stats (how many are on each level).
- **Thursday attendance and outings:** the admin records attendance and trip participation.
- **Per-person private notes:** phone, birthday, and event history, visible only to the signed-in admin.
- **Backup and restore:** export everything to JSON and restore from it.

## Tech stack

- Plain HTML, CSS, and vanilla JavaScript in a single page (no frameworks, no build step)
- Firebase Hosting
- Firebase Authentication (one admin account, email and password)
- Cloud Firestore (realtime sync)
- Google Fonts (Cairo)

## Setup

1. Create a Firebase project and enable **Authentication** (Email/Password) and **Cloud Firestore**.
2. In Authentication, create one user with the email in `ADMIN_EMAIL` near the top of the script in `index.html` (or change the constant to your own email), with a strong password.
3. Copy your own Firebase web config into the `FIREBASE_CONFIG` constant in `index.html`. (The config is not a secret; it only identifies the project. Access is controlled by Authentication and the Firestore rules below.)
4. In the Firebase console, go to **Firestore Database → Rules**, paste the contents of `firestore.rules`, and publish.
5. Deploy with `firebase deploy` (the Firebase CLI) or host the files anywhere as a static site.

## Privacy note

The first version of this site let anyone with the link read the full list of names and card levels without signing in. The `firestore.rules` file in this repo closes that: every read and write now requires the admin to be signed in. After publishing these rules, the list only loads after logging in, which is the intended behavior. People's names should not be public.

## Passwords

There are no passwords in the code. The admin password lives only in Firebase Authentication. If it is forgotten, reset it from the Firebase console (Authentication → Users).
