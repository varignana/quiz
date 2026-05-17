# ExamForge

A self-contained, multi-exam study tool hosted on GitHub Pages. No build step, no framework, no install — everything lives in a single HTML file. Create any number of exams, add questions, track progress, and take timed mock tests — all saved to the cloud under one account.

---

## Live App

👉 **[https://varignana.github.io/quiz/](https://varignana.github.io/quiz/)**

---

## What It Does

ExamForge lets you build and study for any exam or topic. Out of the box it comes loaded with the **AWS Certified AI Practitioner** exam. You can add more exams (Life in the UK, Azure AZ-900, a custom topic — anything) without touching the code.

Each exam has its own:
- Question pool
- Study progress and answer history
- Multiple study tries (attempts)
- Mock exam attempts and scores
- Custom question sets

---

## Features

### Study tab
- Browse all questions for the active exam with category and label filters
- Jump to a random unanswered question
- Submit answers and get instant feedback with per-option explanations
- Label questions (mark wrong ones for the Focus tab)
- **Multiple tries** — start a fresh attempt with `+Try` while keeping full history

### Stats tab
- Visual breakdown of correct / wrong / unanswered across all questions
- Per-category accuracy grid
- Progress tracked across tries

### Focus tab
- Drill only the questions you got wrong or flagged
- Bulk-label questions for efficient review

### Exam tab
- **Random mock exam** — draws questions from the full pool using the exam's configured settings (question count, time limit, pass score)
- **Custom Sets** — admin-created named collections of hand-picked questions; all users can start them
- Timed countdown, flag questions, review before submit
- Auto-submits when time runs out
- Full answer review after submission with correct/wrong colouring per question and per option
- **Past attempts** — stored with score, date, set name (or "Random"), and a 📖 Review button to revisit any attempt's full answer detail at any time

### Account tab
- Change password (no email required, works from active session)
- Link a recovery email for self-service password reset if locked out
- Admin tools (gated by a separate admin PIN)
- Study tips

---

## Exam Management (Admin)

### Creating an exam

Account tab → Admin → **🎓 Manage Exams** → Create New Exam

| Field | Description |
|---|---|
| Provider | Short label shown bold in the header, e.g. `AWS`, `GOV.UK` |
| Exam name | Shown next to the provider, e.g. `AI PRACTITIONER`, `LIFE IN THE UK` |
| Total questions | How many questions to draw for a mock exam |
| Time (minutes) | Countdown timer for the mock exam |
| Score system | AWS Scale (100–1000), Percentage (0–100%), or Custom max |
| Pass threshold | Score needed to pass, in the chosen score units |
| Draw mode | Random (pick N at random) or Proportional by question type |
| Allowed question types | Which types can be added and drawn for this exam |

### Editing exam settings

Every exam in the Manage Exams modal has an **✎ Edit** button. All settings can be changed after creation. Questions and user progress are stored separately by exam ID and are **never affected** by editing the settings.

### Switching exams

When more than one exam exists, a **▾ Switch** button appears next to the header logo for all users. The dropdown lists all exams and highlights the active one.

### Adding questions

Study tab → **Add Question** (visible in admin mode). Five question types are supported:

| Type | Description |
|---|---|
| **Single choice** | One correct answer from 2–10 options |
| **Multi-select** | Two or more correct answers; all must be selected to score |
| **True / False** | A factual statement evaluated as True or False |
| **Ordering** | Drag items into the correct sequence |
| **Matching** | Match left-column descriptions to right-column answers |

The allowed types for each exam are configured when creating or editing the exam. Only those types appear in the Add Question form.

### Editing questions

Every question card has an **✎ Edit** button in admin mode. The edit modal lets you change everything — including the question type — with a dynamic form that rebuilds for each type. Options can be added or deleted individually. Supported across all five types.

### Custom exam sets

Exam tab → **✚ New Custom Set** (admin mode only, visible to all users once created)

1. Give the set a name
2. Use the filter bar or **From # / To #** range selector to find questions quickly
3. Use **All visible** to select/deselect everything currently filtered
4. Click question squares (grid view) or rows (list view) to toggle — scroll position never resets
5. Optionally untick **Shuffle question order** to serve questions in the exact order selected
6. Save — the set appears as a **Start →** card in the Exam tab for all users

---

## AI-Assisted Question Creation

The Account tab has a **Show AI prompt & format guide** button that generates a complete, copy-paste-ready prompt tailored to the active exam. It includes:

- Exam metadata (name, question count, time, pass score)
- Full JSON format examples for every **allowed question type** of that exam only
- A separate "Fill Explanations" section for adding per-option explanations to existing questions
- Common mistake warnings to reduce bad JSON output

The same prompt is embedded inside the downloaded JSON file (`_readme` array), so you always have instructions alongside your data.

### JSON format

Download: Account tab → Export Questions & Explanations

```json
{
  "_readme": ["...full AI prompt lines..."],
  "questions": [
    {
      "id": 1,
      "type": "single",
      "stem": "Which service is used for real-time inference?",
      "options": { "A": "S3", "B": "SageMaker", "C": "Glue", "D": "Athena" },
      "correct": ["B"],
      "category": "ML Services",
      "explanation": {
        "concept": "SageMaker provides managed endpoints for real-time inference.",
        "A": { "ok": false, "why": "S3 is object storage." },
        "B": { "ok": true,  "why": "SageMaker Endpoints serve real-time predictions." },
        "C": { "ok": false, "why": "Glue is an ETL service." },
        "D": { "ok": false, "why": "Athena is a SQL query service." }
      }
    },
    {
      "id": 2,
      "type": "truefalse",
      "stem": "The Battle of Hastings took place in 1066.",
      "correct": ["True"],
      "category": "History",
      "explanation": {
        "concept": "The Norman Conquest began with this battle.",
        "why": "TRUE — The Battle of Hastings was fought on 14 October 1066."
      }
    },
    {
      "id": 3,
      "type": "multi",
      "stem": "Which TWO of the following are AWS AI services?",
      "options": { "A": "Rekognition", "B": "Glue", "C": "Comprehend", "D": "CloudTrail" },
      "correct": ["A", "C"],
      "category": "AI Services",
      "explanation": {
        "concept": "AWS offers several purpose-built AI services.",
        "A": { "ok": true,  "why": "Rekognition does image and video analysis." },
        "B": { "ok": false, "why": "Glue is an ETL service, not an AI service." },
        "C": { "ok": true,  "why": "Comprehend does NLP on text." },
        "D": { "ok": false, "why": "CloudTrail is an audit logging service." }
      }
    }
  ]
}
```

Upload the completed file via **Import JSON** in the Account tab. The app automatically normalises options from AI tools — both array `[{key, text}]` and object `{A: text}` formats are accepted on import.

---

## Accounts & Access

### Creating an account
Click **No account yet? Create one** on the login screen. Choose a username and a password of at least 6 characters. No real email address is required.

### Changing your password
Account tab → **🔒 Change Password** → enter a new password twice → Update Password. Works from any active session with no email needed.

### Linking a recovery email
Account tab → **📌 Recovery Email** → enter a real email → Link Email. If you get locked out later, contact the admin and quote your username plus this email to verify your identity.

### Forgot your password
Login screen → **Forgot password?** → enter your recovery email. A reset link is sent if a match is found. Without a recovery email, an admin can reset your account from the Supabase dashboard.

### Guest mode
Click **Continue as guest** to browse questions without signing in. Progress is not saved.

---

## Tech Stack

| Layer | What |
|---|---|
| Frontend | Vanilla HTML + CSS + JavaScript — single file, no build step |
| Backend / Auth | [Supabase](https://supabase.com) (Postgres + GoTrue Auth) |
| Hosting | GitHub Pages |

### Supabase tables

| Table | Columns | Purpose |
|---|---|---|
| `quiz_progress` | `user_id`, `data` (jsonb), `updated_at` | Per-user study progress, tries, exam attempt history |
| `quiz_content` | `key` (text PK), `data` (jsonb), `updated_at` | Shared content: questions, explanations, exam definitions, custom sets |

Content keys follow the pattern `exam_<id>_questions`, `exam_<id>_categories`, etc. The default AWS exam uses legacy unnamespaced keys (`questions`, `categories`) for backward compatibility.

---

## Self-Hosting

1. Fork the repo and enable GitHub Pages (Settings → Pages → Deploy from `main`, root `/`)
2. Create a free project at [supabase.com](https://supabase.com)
3. In `index.html`, update the two constants near the top of the `<script>` block:
   ```js
   var SB_URL = 'https://your-project.supabase.co';
   var SB_KEY = 'your-anon-public-key';
   ```
4. Create the two tables above in Supabase (Table Editor or SQL editor)
5. In **Authentication → Providers → Email**, turn **Secure email change** OFF — required because user accounts use synthetic internal emails
6. In **Authentication → URL Configuration**, add your GitHub Pages URL to the **Redirect URLs** list — required for password reset emails to work
7. Configure Row Level Security (RLS) so each user can only read and write their own `quiz_progress` row

---

## Project Structure

```
/
├── index.html   ← The entire app (~183 KB, single file)
└── README.md    ← This file
```

---

## AWS AI Practitioner Exam Reference

The default exam uses proportional draw mode to match the official AWS weighting:

| Domain | Weight | Questions (of 65) |
|---|---|---|
| Fundamentals of AI and ML | 20% | ~13 |
| Fundamentals of Generative AI | 24% | ~16 |
| Applications of Foundation Models | 28% | ~18 |
| Guidelines for Responsible AI | 14% | ~9 |
| Security, Compliance, and Governance | 14% | ~9 |

Pass score: **700 / 1000** (≈ 67% correct) · Time: **90 minutes**

---

## License

Personal study tool — free to fork and adapt for your own exam preparation.
