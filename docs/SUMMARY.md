# Life.D MVP - Project Summary

**Project Name:** Life.D (formerly Journote)  
**Repository:** `eysenfalk/journote` (GitHub)  
**Mission:** ADHD-optimized life management where success = "never search for or miss tasks and events ever again"  
**Timeline:** 60 days (Nov 17, 2025 → Jan 15, 2026)  
**Status:** ✅ Planning Complete → Ready for Implementation

---

## 📋 What We Just Created

### Documents Generated
1. **`docs/PRD.md`** - Product Requirements Document
   - 67 functional requirements
   - Non-functional requirements (performance, security, accessibility)
   - Platform-specific requirements (Windows desktop, Android mobile)
   - Success criteria: Zero missed tasks/events for 30 days

2. **`docs/epics.md`** - Epic & Story Breakdown
   - 6 epics with detailed descriptions
   - 48 user stories in BDD format (Given/When/Then)
   - Full FR coverage matrix (all 67 FRs mapped to stories)
   - Technical implementation notes per story

3. **`docs/github-issues-import.md`** - GitHub Import Guide
   - Ready-to-copy issue templates
   - PowerShell script for bulk import
   - Instructions for manual creation

4. **`.bmad/bmm/config.yaml`** - Project Configuration
   - Project name updated to "Life.D"
   - User: Falk
   - Output folder: `docs/`

---

## 🎯 Project Scope (67 FRs → 6 Epics → 48 Stories)

### Epic 1: Foundation & Core Infrastructure (5 stories)
**Goal:** Offline-first Flutter app with Supabase sync  
**Tech:** Drift (SQLite), BLoC, go_router, Supabase auth  
**Stories:**
- 1.1: Project Setup & Dev Environment
- 1.2: Local Database Schema (Captures, Tasks, JournalEntries, Settings)
- 1.3: Supabase Authentication
- 1.4: Real-Time Sync Engine (conflict resolution, offline queue)
- 1.5: App State Management & Navigation

### Epic 2: Instant Capture System (5 stories)
**Goal:** <3 second thought capture from anywhere  
**Tech:** Windows hotkey (`Ctrl+Shift+L`), Android widget, SQLite FTS5  
**Stories:**
- 2.1: Desktop Global Hotkey Capture
- 2.2: Mobile Widget Capture (3x1, 4x1)
- 2.3: Auto-Categorization Engine (task/note/journal detection)
- 2.4: Captures List View & Search (<100ms, 1000 items)
- 2.5: Context Tags & Manual Reclassification

### Epic 3: Proactive Task/Event Management (10 stories)
**Goal:** Never miss tasks/events (core mission)  
**Tech:** Google Calendar OAuth, SQL UNION timeline, real-time countdown  
**Stories:**
- 3.1: Create & Edit Tasks
- 3.2: Recurring Tasks Logic (daily/weekly/monthly)
- 3.3: Google Calendar Import (read-only)
- 3.4: Unified Timeline (tasks + events)
- 3.5: Ambient Dashboard (Now/Today/Week tabs)
- 3.6: Task Dependencies & Blocking
- 3.7: Snooze & Reschedule
- 3.8: Archive Completed Tasks
- 3.9: Quick Actions (swipe gestures)
- 3.10: Task Completion Stats (for weekly review)

### Epic 4: ADHD-Optimized Smart Reminders (8 stories)
**Goal:** Notifications that respect ADHD attention patterns  
**Tech:** Escalating reminders, geofencing, context-aware timing  
**Stories:**
- 4.1: Basic Notification Infrastructure
- 4.2: Escalating Task Reminders (4 levels)
- 4.3: Location-Aware Reminders (geofences)
- 4.4: Context-Aware Timing (no reminders during meetings)
- 4.5: Daily Digest (8am default)
- 4.6: Weekly Digest (Sunday 7pm)
- 4.7: Persistent Urgent Notification
- 4.8: Quiet Hours & Snooze Settings

### Epic 5: Life-Systems Journaling (12 stories)
**Goal:** Detect invisible self-changes via trend analysis  
**Tech:** AES-256 encryption, trend graphs, correlation detection  
**Stories:**
- 5.1: Daily Journal Prompt Screen
- 5.2: Life-Systems Rating Inputs (1-10 scale: Relationship, Work, Energy, Mood)
- 5.3: Freeform Reflection Field
- 5.4: Journal Entry Encryption (optional)
- 5.5: Journal Calendar Heatmap
- 5.6: 7-Day Trend Graph
- 5.7: 30-Day Trend Analysis (with decline alerts)
- 5.8: Cross-System Correlation Detection
- 5.9: Journal Streak Tracking
- 5.10: Journal Reminder Notification (8pm default)
- 5.11: Journal History & Search
- 5.12: Weekly Review Workflow (task stats + trends + reschedule)

### Epic 6: Settings & Data Portability (8 stories)
**Goal:** User control and data ownership  
**Tech:** Export CSV/JSON/Markdown, flexible import mapping  
**Stories:**
- 6.1: Notification Preferences
- 6.2: Journal Configuration (customize systems, reminder time)
- 6.3: Context Tags Management (edit, merge, delete)
- 6.4: Work Hours & Quiet Hours
- 6.5: Location Tracking Toggle
- 6.6: Appearance Settings (theme, font, color)
- 6.7: Data Export (CSV/JSON/Markdown)
- 6.8: Data Import & Restore

---

## 🚀 Next Steps (Priority Order)

### Immediate (Today)
1. **Import to GitHub Issues**
   - Use `docs/github-issues-import.md` as guide
   - Option A: Manual creation (15-20 min)
   - Option B: Install GitHub CLI + run PowerShell script (2 min)
   - Creates 54 issues (6 epics + 48 stories)

2. **Create GitHub Project Board**
   - Project name: "Life.D MVP - Phase 0"
   - Columns: Backlog → Ready → In Progress → Review → Done
   - Link all issues to project
   - Set milestone dates

### Short-Term (This Week)
3. **Run UX Design Workflow** (optional but recommended)
   - Load UX Designer agent: `.bmad/bmm/agents/ux.md`
   - Command: `*wireframes` or `*design-system`
   - Adds wireframes/mockups to each story
   - Output: `docs/ux-design.md`

4. **Run Architecture Workflow** (optional but recommended)
   - Load Solutions Architect agent: `.bmad/bmm/agents/sa.md`
   - Command: `*architecture`
   - Adds:
     - System architecture diagrams
     - Database ER diagrams
     - API specifications
     - Component interaction flows
   - Output: `docs/architecture.md`

5. **Setup Development Environment**
   - Start Story 1.1: Project Setup
   - Initialize Flutter project (Windows + Android)
   - Install dependencies (Drift, Supabase, BLoC)
   - Validate with `flutter doctor`

### Medium-Term (Week 2-3)
6. **Implement Epic 1 (Foundation)**
   - Stories 1.1 → 1.5 sequentially
   - Each story = 1 dev agent session
   - Test after each story completion
   - Mark done in GitHub project

7. **Implement Epic 2 (Capture)**
   - Stories 2.1 → 2.5 sequentially
   - Desktop hotkey first (faster to validate)
   - Then Android widget
   - Test capture → save → search flow

### Long-Term (Week 4-8)
8. **Implement Epics 3-6**
   - Epic 3: Task/Event Management (core value)
   - Epic 4: Smart Reminders (ADHD optimization)
   - Epic 5: Journaling (self-awareness)
   - Epic 6: Settings (polish)

9. **Personal Dogfooding**
   - Use app for 30 days
   - Track: missed tasks/events count
   - Success = zero misses for 30 days
   - Iterate based on real usage

10. **Phase 1 Planning**
    - Based on Phase 0 learnings
    - Add: Biometric auth, Outlook calendar, ML categorization
    - Consider: iOS version, web dashboard

---

## 📊 Success Metrics

### Primary KPI
**Zero missed tasks/events for 30 consecutive days**
- Measured: Manual tracking during dogfooding
- Target: 100% recall (no false negatives)

### Secondary KPIs
- **Capture Speed:** <3 seconds from trigger to saved
  - Desktop: <100ms window open, <500ms save
  - Mobile: <500ms widget → saved
- **App Launch:** <2 seconds cold start
- **Search:** <100ms for 1000 captures
- **Sync:** <1s incremental, <5s initial (1000 items)
- **Notification Reliability:** 99.9% delivery rate

### Qualitative KPIs
- **ADHD Tax Reduction:** Subjective feeling of "never losing thoughts"
- **Self-Awareness:** Can answer "How have I been lately?" with data, not memory
- **Task Visibility:** Never searching for "what do I need to do today?"

---

## 🛠️ Tech Stack Summary

### Frontend
- **Flutter 3.16+** (Dart)
- **Targets:** Windows desktop (primary), Android 12+ (secondary)
- **State Management:** BLoC pattern
- **Navigation:** go_router
- **UI:** Material Design 3 (ADHD-optimized: high contrast, large touch targets)

### Local Storage
- **Drift 2.14+** (type-safe SQLite)
- **Hive** (fast key-value for settings)
- **Tables:** Captures, Tasks, JournalEntries, CalendarEvents, Settings
- **Full-text Search:** SQLite FTS5

### Backend & Sync
- **Supabase** (Postgres + Auth + Realtime)
- **Sync Strategy:** Local-first, eventual consistency, last-write-wins
- **Auth:** Email/password (biometric Phase 2)

### Notifications
- **Windows:** Toast notifications
- **Android:** Notification channels + WorkManager (background)

### Integrations
- **Google Calendar API** (OAuth 2.0, read-only)
- **Outlook Calendar** (Phase 2)

### Security
- **Encryption:** AES-256 for journal entries (user-controlled key)
- **Secure Storage:** flutter_secure_storage (session tokens, encryption keys)
- **RLS:** Supabase Row Level Security (user data isolation)

---

## 📁 Repository Structure

```
eysenfalk/journote/
├── .bmad/                      # BMad Method configuration
│   └── bmm/
│       ├── agents/             # PM, UX, SA, Dev, QA agents
│       ├── config.yaml         # Project: Life.D, User: Falk
│       └── workflows/          # PRD, Epic, UX, Architecture, Implementation
├── docs/                       # Living documents
│   ├── PRD.md                  # ✅ Complete (67 FRs)
│   ├── epics.md                # ✅ Complete (6 epics, 48 stories)
│   ├── github-issues-import.md # ✅ Complete (import guide)
│   ├── SUMMARY.md              # ✅ This file
│   ├── ux-design.md            # ⏳ Pending (UX workflow)
│   └── architecture.md         # ⏳ Pending (Architecture workflow)
├── lib/                        # ⏳ Flutter source (after Story 1.1)
│   ├── features/               # Feature modules (capture, tasks, journal)
│   ├── core/                   # Shared infrastructure (sync, auth, db)
│   └── shared/                 # Widgets, utils, constants
├── test/                       # Unit + integration tests
├── android/                    # Android-specific code
├── windows/                    # Windows-specific code
├── pubspec.yaml                # Dependencies
└── README.md                   # Setup instructions
```

---

## 💡 Key Design Decisions

### 1. **Local-First Architecture**
**Why:** ADHD brains can't tolerate "waiting for sync" friction. Offline must be first-class.

### 2. **BLoC State Management**
**Why:** Testable, separates business logic from UI, scales well for 48 stories.

### 3. **Flutter (not React Native or native)**
**Why:** Single codebase for Windows + Android, excellent desktop support, Dart type safety.

### 4. **Supabase (not Firebase or custom backend)**
**Why:** Postgres (real database), instant APIs, built-in auth, self-hostable (future).

### 5. **Rule-Based Categorization (not ML)**
**Why:** MVP speed. Regex patterns are fast, deterministic, and good enough. ML in Phase 2 if needed.

### 6. **Last-Write-Wins Conflict Resolution**
**Why:** Simple, predictable. ADHD users unlikely to edit same task simultaneously on multiple devices.

### 7. **Global Hotkey (not menu bar app)**
**Why:** <100ms feels instant. Menu bar requires mouse (breaks flow).

### 8. **Ambient Dashboard (not search-first)**
**Why:** ADHD working memory issue. Can't search if you forgot what to search for.

---

## 🎨 ADHD-Specific Design Principles

### Visual Hierarchy
- **Most important = largest, boldest, brightest**
- Countdown timers: 32px font, red if <15 min
- Overdue tasks: Red background, ⚠️ icon
- Empty states: Motivational, not guilt-inducing

### Friction Reduction
- **<3 seconds capture** (faster than opening Notes app)
- **No "Are you sure?" dialogs** (undo instead)
- **Auto-save everywhere** (no explicit Save buttons)
- **Swipe gestures** (faster than menus)

### Forgiveness
- **Undo for 3 seconds** after delete
- **Archive, don't delete** (can restore)
- **Snooze, don't dismiss** notifications
- **Reschedule in weekly review** (not guilt about overdue)

### Working Memory Support
- **Now view = only urgent** (no cognitive load deciding what's urgent)
- **Countdown timers** ("Meeting in 23 minutes" vs "Meeting at 3pm")
- **Context tags** (@work, @home) not folder hierarchies
- **Heatmap calendar** (visual memory cue)

### Motivation
- **Streak tracking** (gamification without guilt)
- **Completion rates** (celebrate what *did* get done)
- **Trend detection** ("You've been improving!" vs raw numbers)
- **Empty state encouragement** ("You're on track! ✓")

---

## 📞 Contact & Support

**Developer:** Falk (GitHub: @eysenfalk)  
**Repository:** https://github.com/eysenfalk/journote  
**Documentation:** `docs/` folder  
**BMad Method Version:** 6.0.0-alpha.9

**Next Agent to Load:**
- For GitHub import: Manual process (see `docs/github-issues-import.md`)
- For UX design: Load `.bmad/bmm/agents/ux.md`, run `*wireframes`
- For architecture: Load `.bmad/bmm/agents/sa.md`, run `*architecture`
- For implementation: Load `.bmad/bmm/agents/dev.md`, start Story 1.1

---

**Status:** ✅ Ready for Implementation  
**Last Updated:** November 17, 2025, 7:15 AM UTC  
**Epic Breakdown Complete:** 6 epics, 48 stories, 67 FRs covered
