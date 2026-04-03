# Gym Momentum

A workout tracking app that helps you monitor exercise progress, detect stagnation, and stay on top of your training routine — built with React, TypeScript, and Lovable Cloud.

## Key Features

### 🏋️ Exercise Tracking
- Track sets (reps × weight) per exercise, organized by workout groups (Push, Pull, Legs)
- Automatic score calculation (`reps × weight` summed across sets)
- Change log records every update with previous/new scores and diff

### 🚦 Stagnation Detection
- Traffic-light system (green / orange / red) flags exercises that haven't been updated in a while to encourage challenging self with increased weight
- Configurable thresholds: "Change Soon" and "Change ASAP" day counts
- **Upcoming tab** shows a badge `[X | Y]` with color-coded ASAP (red) and Soon (orange) counts to alert user to approaching stagnation alert triggers

### 📈 History & Charts
- Per-exercise line charts showing score progression over time
- Charts ordered by most recently updated first
### 🔐 Authentication & Security
- Email/password sign-up and sign-in with email verification
- Full password reset flow: "Forgot Password" → email link → `/reset-password` page
- Inline error messaging with contextual reset link on invalid credentials
- Row-Level Security (RLS) on all tables — users can only access their own data

### ☁️ Cloud Persistence
- All data stored in Lovable Cloud (powered by Supabase)
- Data persists across deploys and code changes
- Automatic seeding of default exercises for new users

### 🎨 Design
- Clean light theme with Space Grotesk + JetBrains Mono typography
- Teal primary accent (`hsl(174, 72%, 38%)`) with semantic color tokens
- Custom status colors: green for fresh, orange for stale, red for urgent
- Fully responsive layout

## Tech Stack

- **Frontend:** React 18, TypeScript, Vite, Tailwind CSS, shadcn/ui
- **Backend:** Lovable Cloud (Supabase) — auth, database, RLS policies
- **Charts:** Recharts
- **Routing:** React Router v6

## Project Structure

```
src/
├── components/
│   ├── ExerciseCard.tsx    # Individual exercise with editable sets
│   ├── ForecastTab.tsx     # Upcoming changes (stagnation alerts)
│   ├── HistoryTab.tsx      # Change log with line charts
│   ├── SettingsPanel.tsx   # Stagnation config + reset data
│   └── NavLink.tsx         # Tab navigation link
├── hooks/
│   ├── useAuth.ts          # Auth state management
│   └── useWorkoutData.ts   # CRUD operations + Supabase sync
├── lib/
│   ├── types.ts            # Interfaces, score calc, stagnation logic
│   ├── initialData.ts      # Default seed exercises
│   └── utils.ts            # Tailwind merge utility
├── pages/
│   ├── Index.tsx           # Main app shell with tab navigation
│   ├── Auth.tsx            # Login / signup form
│   ├── ForgotPassword.tsx  # Password reset request
│   └── ResetPassword.tsx   # Set new password
└── integrations/
    └── supabase/           # Auto-generated client + types
```

## Database Schema

| Table | Purpose |
|-------|---------|
| `exercises` | Exercise definitions with sets data (JSON), grouped by workout |
| `change_log` | Timestamped score changes per exercise |
| `stagnation_config` | Per-user thresholds for change alerts |

All tables enforce RLS — users can only read, write, and delete their own rows.
