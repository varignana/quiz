# AWS AI Practitioner Quiz

A self-contained study tool for the **AWS Certified AI Practitioner** exam, hosted on GitHub Pages. No build step, no dependencies to install — everything lives in a single HTML file.

---

## Live App

👉 **[https://varignana.github.io/quiz/](https://varignana.github.io/quiz/)**

---

## Features

- **Study mode** — Browse all questions with category and label filters, or jump to a random unanswered one
- **Exam mode** — Official AWS-style mock exam (65 questions, 90 min) or a custom proportional-timing mode
- **Focus tab** — Drill only the questions you got wrong, with bulk labelling
- **Multiple tries** — Start a fresh attempt with `+Try` while keeping full history of past tries
- **Progress sync** — All answers, labels, and stats are saved to the cloud (Supabase) and sync across devices
- **Guest mode** — Try the app without an account; no progress saved
- **Admin mode** — Add, edit, and organise questions and categories from within the app
- **Dark mode** — Automatic, follows your system preference

---

## How to Use

### Creating an account

1. Open the app and click **"No account yet? Create one"**
2. Choose a **username** (letters, numbers, `_`, `-`) and a password of at least 6 characters
3. No real email needed to sign up

> Your username becomes your identity. There is no email confirmation step.

### Changing your password

Go to the **Account** tab → **Change Password** → enter your new password twice → click **Update Password**. Works while you are logged in, no email required.

### Linking a recovery email *(recommended)*

Go to **Account** tab → **Recovery Email** → enter a real email address → click **Link Email**.

This saves your email to your profile. If you are ever locked out, contact the admin and share your username + this email to verify your identity.

### Forgot your password?

On the login screen click **"Forgot password?"** and enter your recovery email (if you linked one). A reset link will be sent to that address.

If you never linked a recovery email, contact the admin — they can reset your account from the Supabase dashboard.

### Switching between tries

Use the **Try selector** in the top bar to switch between past attempts. Click **+Try** to start a clean slate while keeping all previous history.

---

## Tech Stack

| Layer | What |
|---|---|
| Frontend | Vanilla HTML + CSS + JavaScript (single file) |
| Auth & Database | [Supabase](https://supabase.com) |
| Hosting | GitHub Pages |
| No build step | ✅ — edit the file, commit, done |

All question content, categories, explanations, and corrections are stored in a Supabase `quiz_content` table and loaded at runtime.

---

## Project Structure

```
/
└── index.html      ← The entire app (HTML + CSS + JS)
└── README.md       ← This file
```

That is the whole repo. There are no frameworks, bundlers, or `node_modules`.

---

## Contributing / Adding Questions

Questions can be added directly inside the app if you have **admin access**:

1. Log in and go to the **Study** tab
2. Enable admin mode from the **Account** tab → **Admin** → **Enable admin mode**
3. Use the **Add Question** button that appears at the top of the study view

Questions are immediately saved to the shared Supabase database and visible to all users.

To add questions in bulk, use the **Export** feature in the Account tab to get the current question list and format, then re-import via the admin panel.

---

## Supabase Setup *(for self-hosting)*

If you want to run your own copy:

1. Create a free project at [supabase.com](https://supabase.com)
2. In `index.html`, update these two constants near the top of the `<script>` block:
   ```js
   const SB_URL = 'https://your-project.supabase.co';
   const SB_KEY = 'your-anon-public-key';
   ```
3. Create a `quiz_content` table with a single `jsonb` column called `data` and a `text` column called `key`
4. In **Authentication → Providers → Email**, turn **Secure email change** OFF
5. In **Authentication → URL Configuration**, add your GitHub Pages URL to the Redirect URLs list
6. Set row-level security (RLS) policies as needed

---

## Exam Blueprint

The mock exam follows the official AWS AI Practitioner weighting:

| Domain | Weight |
|---|---|
| Fundamentals of AI and ML | 20% |
| Fundamentals of Generative AI | 24% |
| Applications of Foundation Models | 28% |
| Guidelines for Responsible AI | 14% |
| Security, Compliance, and Governance | 14% |

Pass score: **700 / 1000** (~67% correct)

---

## License

Personal study tool — feel free to fork and adapt for your own exam prep.
