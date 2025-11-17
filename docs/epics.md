# Life.D - Epic & Story Breakdown

**Author:** Falk
**Date:** 2025-11-15
**Version:** 1.0 (Initial - will be updated by UX and Architecture workflows)

**Source PRD:** `docs/PRD.md`

---

## Document Status

**Living Document:** This epic breakdown will evolve as you progress through BMad Method:
- ✅ **Step 1 Complete:** Initial epic and story decomposition
- ⏳ **Step 2 Pending:** UX Design will add interaction details
- ⏳ **Step 3 Pending:** Architecture will add technical decisions
- ⏳ **Step 4:** Implementation pulls complete context from PRD + Epics + UX + Architecture

---

## Functional Requirements Inventory (from PRD)

**Quick Capture (FR1-FR8):**
- FR1: Desktop global hotkey capture
- FR2: Mobile widget capture
- FR3: <500ms save with offline support
- FR4: View all captures chronologically
- FR5: Search captures by text
- FR6: Auto-categorize (task/note/journal)
- FR7: Manual conversion to tasks/journal
- FR8: Tag captures with context

**Task & Event Management (FR9-FR17):**
- FR9: Create tasks (title, due date, priority, tags)
- FR10: Recurring tasks (daily/weekly/monthly/custom)
- FR11: Mark tasks complete
- FR12: Auto-hide completed tasks
- FR13: Import calendar events (read-only)
- FR14: Unified timeline (tasks + events)
- FR15: Task dependencies
- FR16: Snooze with smart reschedule
- FR17: Archive tasks for review

**Smart Reminders & Notifications (FR18-FR25):**
- FR18: Escalating notifications (gentle → persistent)
- FR19: Location-aware reminders
- FR20: Context-aware reminders (work hours)
- FR21: Configure escalation per task
- FR22: Persistent notification for urgent
- FR23: Daily digest notification
- FR24: Weekly planning notification
- FR25: Smart snooze (not infinite)

**Ambient Dashboard (FR26-FR33):**
- FR26: "Now" view (immediate attention)
- FR27: "Today" view (full day timeline)
- FR28: "This Week" view (7-day obligations)
- FR29: Visual distinction (overdue vs upcoming)
- FR30: Color-coded context tags
- FR31: Time until next event/deadline
- FR32: Quick complete from dashboard
- FR33: Real-time dashboard updates

**Life-Systems Journaling (FR34-FR45):**
- FR34: Daily prompt at configured time
- FR35-FR38: Rate Relationships/Work/Energy/Mood (1-10 + notes)
- FR39: Freeform self-awareness reflection
- FR40: Gentle journal completion reminders
- FR41: View journal history (calendar format)
- FR42: Weekly review with trend lines
- FR43: Highlight significant rating changes
- FR44: Add context notes in review
- FR45: End-to-end encryption for journals

**Data Management & Sync (FR46-FR53):**
- FR46: Local-first storage
- FR47: Cross-device sync when online
- FR48-FR49: Export/import all data
- FR50: Auto-resolve sync conflicts
- FR51: Sync status indicator
- FR52: Manual sync trigger
- FR53: Auto-backup to cloud (opt-in)

**Account & Settings (FR54-FR61):**
- FR54: Email authentication
- FR55: Configure notification preferences
- FR56: Configure journal timing/template
- FR57: Configure context tags/colors
- FR58: Set work hours
- FR59: Enable/disable location tracking
- FR60: Configure appearance (theme/font)
- FR61: Secure credential storage

**Weekly Review (FR62-FR67):**
- FR62: Generate review every Sunday
- FR63: Show completed vs incomplete tasks
- FR64: Journal trend analysis
- FR65: Reflection prompt ("what didn't get done?")
- FR66: Archive/reschedule during review
- FR67: Weekly review reminder notification

**Total:** 67 functional requirements covering complete MVP scope.

---

## Proposed Epic Structure

### Epic 1: Foundation & Core Infrastructure
**FR Coverage:** Infrastructure for FR46-FR61 (auth, sync, settings, local storage)

### Epic 2: Instant Capture System  
**FR Coverage:** FR1-FR8 (desktop hotkey, mobile widget, auto-categorize, search, tags)

### Epic 3: Proactive Task/Event Management
**FR Coverage:** FR9-FR17 (task CRUD, recurring, calendar import, dependencies, archiving), FR26-FR33 (Now/Today/Week views, real-time dashboard, quick actions)

### Epic 4: ADHD-Optimized Smart Reminders
**FR Coverage:** FR18-FR25 (escalating notifications, location-aware, context-aware, digest, persistent urgent, snooze, quiet hours)

### Epic 5: Life-Systems Journaling
**FR Coverage:** FR34-FR45 (daily prompt, 1-10 ratings, freeform reflection, trends, encryption, reminders), FR62-FR67 (weekly review, completion analysis, trend review, reflection, reschedule)

### Epic 6: Settings & Data Portability
**FR Coverage:** FR46-FR53 (data export, import, sync indicators, manual sync, cloud backup), FR54-FR61 (notification prefs, journal config, tags, work hours, location, appearance)

**Sequencing Rationale:**
1 → 2 → 3 → 4 → 5 → 6 enables incremental delivery:
- After Epic 1: Infrastructure works
- After Epic 2: Can capture thoughts
- After Epic 3: Can manage tasks (basic functionality)
- After Epic 4: ADHD-friendly reminders (full core value)
- After Epic 5: Self-awareness tracking (complete MVP)
- After Epic 6: Customizable experience (polished product)

---

## Epic 1: Foundation & Core Infrastructure

**Goal:** Establish technical foundation enabling offline-first, cross-platform functionality with secure authentication and real-time sync.

**Value:** Enables all subsequent features—cannot capture, manage tasks, or journal without this foundation.

**FR Coverage:** Infrastructure supporting FR46-FR61 (local storage, sync, auth, settings)

### Story 1.1: Project Setup & Development Environment

**As a** developer  
**I want** a properly initialized Flutter project with core dependencies  
**So that** I can build cross-platform (Windows desktop + Android mobile) with offline-first architecture

**Acceptance Criteria:**

**Given** a new project initialization  
**When** setting up the Flutter project structure  
**Then** the following must be configured:
- Flutter SDK 3.16+ with stable channel
- Project supports Windows desktop + Android 12+ targets
- Folder structure: `lib/` (features, core, shared), `test/`, `assets/`
- Core dependencies in `pubspec.yaml`:
  - `supabase_flutter: ^2.0.0` (backend + auth + realtime)
  - `sqflite: ^2.3.0` (local SQLite database)
  - `hive_flutter: ^1.1.0` (fast local key-value storage)
  - `drift: ^2.14.0` (type-safe SQL queries)
  - `get_it: ^7.6.0` (dependency injection)
  - `bloc: ^8.1.0` + `flutter_bloc: ^8.1.0` (state management)
  - `equatable: ^2.0.5` (value equality)
  - `dartz: ^0.10.1` (functional programming)
- Dev dependencies: `flutter_test`, `build_runner`, `drift_dev`
- Git initialized with `.gitignore` for Flutter/Dart
- Build variants configured: debug, profile, release
- Platform-specific setup:
  - Windows: `windows/runner/` configured for global hotkeys
  - Android: `android/app/` configured for widgets + background services

**And** development environment is validated  
**Then** `flutter doctor` shows no errors, app builds successfully on both platforms

**Prerequisites:** None (first story)

**Technical Notes:**
- Use BLoC pattern for state management (testable, separates business logic)
- Local-first architecture: SQLite primary, Supabase sync secondary
- Drift for type-safe database access with compile-time query validation
- Hive for fast settings/cache (faster than SQLite for simple key-value)

---

### Story 1.2: Local Database Schema & Offline Storage

**As a** user  
**I want** all my data stored locally on my device  
**So that** the app works fully offline and I never lose data due to connectivity issues

**Acceptance Criteria:**

**Given** the Flutter project with Drift installed  
**When** defining the local database schema  
**Then** create the following Drift tables with migrations:

**Captures Table:**
```dart
@DataClassName('Capture')
class Captures extends Table {
  IntColumn get id => integer().autoIncrement()();
  TextColumn get content => text()();
  TextColumn get category => text()(); // 'task', 'note', 'journal'
  TextColumn get contextTags => text().nullable()(); // JSON array
  DateTimeColumn get createdAt => dateTime()();
  DateTimeColumn get syncedAt => dateTime().nullable()();
  TextColumn get supabaseId => text().nullable()(); // for sync
  BoolColumn get isSynced => boolean().withDefault(const Constant(false))();
}
```

**Tasks Table:**
```dart
@DataClassName('Task')
class Tasks extends Table {
  IntColumn get id => integer().autoIncrement()();
  TextColumn get title => text()();
  TextColumn get description => text().nullable()();
  DateTimeColumn get dueDate => dateTime().nullable()();
  TextColumn get priority => text()(); // 'low', 'medium', 'high', 'urgent'
  TextColumn get contextTags => text().nullable()(); // JSON array
  TextColumn get recurrence => text().nullable()(); // JSON: {type, interval}
  BoolColumn get isComplete => boolean().withDefault(const Constant(false))();
  DateTimeColumn get completedAt => dateTime().nullable()();
  IntColumn get dependsOn => integer().nullable().references(Tasks, #id)();
  DateTimeColumn get createdAt => dateTime()();
  DateTimeColumn get syncedAt => dateTime().nullable()();
  TextColumn get supabaseId => text().nullable()();
}
```

**JournalEntries Table:**
```dart
@DataClassName('JournalEntry')
class JournalEntries extends Table {
  IntColumn get id => integer().autoIncrement()();
  DateTimeColumn get entryDate => dateTime()();
  IntColumn get relationshipRating => integer().nullable()();
  TextColumn get relationshipNotes => text().nullable()();
  IntColumn get workRating => integer().nullable()();
  TextColumn get workNotes => text().nullable()();
  IntColumn get energyRating => integer().nullable()();
  TextColumn get energyNotes => text().nullable()();
  IntColumn get moodRating => integer().nullable()();
  TextColumn get moodNotes => text().nullable()();
  TextColumn get reflection => text().nullable()();
  TextColumn get encryptedContent => text().nullable()(); // encrypted JSON
  DateTimeColumn get createdAt => dateTime()();
  DateTimeColumn get syncedAt => dateTime().nullable()();
  TextColumn get supabaseId => text().nullable()();
}
```

**Settings Table:**
```dart
@DataClassName('Setting')
class Settings extends Table {
  TextColumn get key => text()();
  TextColumn get value => text()();
  
  @override
  Set<Column> get primaryKey => {key};
}
```

**And** database initialization completes  
**Then** migrations run successfully on first app launch, all tables created

**And** offline functionality verified  
**Then** CRUD operations work without internet connection, data persists across app restarts

**Prerequisites:** Story 1.1 (project setup with Drift)

**Technical Notes:**
- Drift generates type-safe DAOs at build time
- Use `@UseRowClass()` for custom model classes if needed
- Implement database migrations for future schema changes
- Store encrypted journals using `encrypted_shared_preferences` + user-controlled key
- JSON columns for flexibility (context tags, recurrence rules)

---

### Story 1.3: Supabase Authentication & User Accounts

**As a** user  
**I want** to create an account and log in securely  
**So that** my data syncs across devices and stays private

**Acceptance Criteria:**

**Given** Supabase project configured with Auth enabled  
**When** implementing authentication flow  
**Then** the following capabilities exist:

**Email/Password Sign-Up:**
- Email field with RFC 5322 validation
- Password requirements enforced:
  - Minimum 8 characters
  - At least 1 uppercase letter
  - At least 1 number
  - At least 1 special character (!@#$%^&*)
- Password strength meter with visual feedback (weak/medium/strong)
- Confirm password field with real-time match validation
- Email verification sent within 15 minutes of sign-up
- Account creation completes in <2 seconds
- Error messages specific and helpful ("Email already exists" not "Error 400")

**Login Flow:**
- Email + password fields
- "Remember me" checkbox (stores session token securely)
- "Forgot password" link triggers email reset
- Session persists across app restarts
- Auto-logout after 30 days of inactivity
- Login completes in <1 second

**Security:**
- Passwords never stored locally (only session tokens)
- Session tokens stored in secure storage (`flutter_secure_storage`)
- Automatic token refresh before expiration
- Logout clears all local session data

**And** authentication UI is ADHD-friendly  
**Then**:
- Mobile responsive with 44x44px minimum touch targets
- Clear visual focus indicators for keyboard navigation
- WCAG 2.1 AA compliant (color contrast, text sizing)
- Loading states prevent double-submission
- Errors display prominently without disappearing automatically

**Prerequisites:** Story 1.1 (project setup with Supabase)

**Technical Notes:**
- Use `supabase_flutter` package for auth
- Store Supabase URL + anon key in `.env` file (not version controlled)
- Implement auth state management with BLoC pattern
- Handle network errors gracefully (offline mode)
- Add biometric auth in future story (Phase 2)

---

### Story 1.4: Real-Time Sync Engine with Conflict Resolution

**As a** user  
**I want** my data to sync automatically across devices when online  
**So that** I can seamlessly switch between desktop and mobile without manual export/import

**Acceptance Criteria:**

**Given** user is authenticated and online  
**When** local data changes (create/update/delete capture, task, or journal)  
**Then** sync engine handles the following:

**Sync Queue:**
- Local changes queued immediately (even if offline)
- Queue persisted to local storage (survives app restart)
- Automatic retry with exponential backoff (1s, 2s, 4s, 8s, 16s, max 30s)
- Manual sync trigger available in UI
- Sync status indicator shows: ✓ Synced | ⟳ Syncing | ⚠ Offline | ✗ Error

**Sync Logic:**
- Push: Upload local changes to Supabase (upsert by `supabaseId`)
- Pull: Fetch remote changes since last sync (`syncedAt` timestamp)
- Merge: Apply remote changes to local database
- Conflict resolution: **Last-write-wins** (most recent `updatedAt` timestamp)
- Optimistic UI: Show changes immediately, revert if sync fails

**Sync Performance:**
- Initial sync (full data download) completes in <5 seconds for 1000 items
- Incremental sync (changes only) completes in <1 second
- Batch operations (sync 50 items at once, not one-by-one)
- Background sync every 5 minutes when app is open

**Error Handling:**
- Network errors: Retry automatically, show "Offline" indicator
- Auth errors: Force re-login, preserve local changes
- Server errors (5xx): Retry with backoff, log to Sentry
- Data loss: Zero tolerance—local changes never deleted without successful upload

**And** sync is observable  
**Then** user can view:
- Last successful sync timestamp
- Pending changes count ("3 items waiting to sync")
- Sync history log (last 20 sync events with success/failure)

**Prerequisites:** Story 1.2 (local database), Story 1.3 (authentication)

**Technical Notes:**
- Use Supabase Realtime for push notifications of remote changes (optional Phase 2 enhancement)
- Implement sync with `SyncRepository` pattern (separates sync logic from UI)
- Store `syncedAt` timestamp per record to detect changes since last sync
- Use Supabase RLS (Row Level Security) policies to enforce user data isolation
- Consider eventual consistency model (not strong consistency)

---

### Story 1.5: App State Management & Navigation

**As a** developer  
**I want** consistent state management and navigation patterns  
**So that** feature development is predictable and testable

**Acceptance Criteria:**

**Given** BLoC pattern established in Story 1.1  
**When** implementing app-wide state and navigation  
**Then** the following architecture exists:

**BLoC Structure:**
```dart
// Authentication BLoC
class AuthBloc extends Bloc<AuthEvent, AuthState> {
  // Events: LoginRequested, LogoutRequested, TokenRefreshed
  // States: Authenticated, Unauthenticated, AuthLoading, AuthError
}

// Sync BLoC
class SyncBloc extends Bloc<SyncEvent, SyncState> {
  // Events: SyncRequested, SyncCompleted, SyncFailed
  // States: Synced, Syncing, SyncError, Offline
}

// App Settings BLoC
class SettingsBloc extends Bloc<SettingsEvent, SettingsState> {
  // Events: ThemeChanged, NotificationPrefsChanged
  // States: SettingsLoaded, SettingsLoading
}
```

**Navigation:**
- Use `go_router` package for declarative routing
- Routes defined:
  - `/` → Splash screen (check auth status)
  - `/login` → Authentication screen
  - `/signup` → Registration screen
  - `/home` → Main dashboard (protected route)
  - `/captures` → Captures list
  - `/tasks` → Tasks view
  - `/journal` → Journal prompt
  - `/settings` → Settings screen
- Protected routes redirect to `/login` if unauthenticated
- Deep linking support (Android intents, Windows protocol)

**Dependency Injection:**
- Use `get_it` for service locator pattern
- Register services at app startup:
  - `AuthRepository`
  - `SyncRepository`
  - `LocalDatabase`
  - `SupabaseClient`
  - All BLoCs registered as singletons

**Error Handling:**
- Global error boundary catches unhandled exceptions
- Errors logged to Sentry (production only)
- User-friendly error messages (never show stack traces)
- Retry mechanisms for transient failures

**And** state is testable  
**Then** BLoC tests cover:
- State transitions for all events
- Error cases handled gracefully
- Side effects (API calls) mocked properly

**Prerequisites:** Story 1.1 (project setup), Story 1.3 (auth), Story 1.4 (sync)

**Technical Notes:**
- BLoC pattern separates business logic from UI (easier to test)
- Use `bloc_test` package for testing BLoCs
- Implement `Equatable` for all states/events (enables proper state comparison)
- Consider `hydrated_bloc` for state persistence (optional Phase 2)

---

## Epic 2: Instant Capture System

**Goal:** Enable frictionless thought capture in <3 seconds from desktop (global hotkey) or mobile (widget), with auto-categorization and offline support.

**Value:** ADHD tax prevention—never lose an idea because of tool friction.

**FR Coverage:** FR1-FR8 (capture, search, auto-categorize, tagging)

### Story 2.1: Desktop Global Hotkey Capture (Windows)

**As a** desktop user  
**I want** to press a keyboard shortcut from anywhere and instantly type my thought  
**So that** I never lose ideas while working (switching apps kills ADHD focus)

**Acceptance Criteria:**

**Given** Life.D is running on Windows (minimized or background)  
**When** user presses global hotkey `Ctrl+Shift+L` (configurable in settings)  
**Then** capture window behavior:

**Window Appearance:**
- Small overlay window appears at cursor position (300x150px minimum)
- Always-on-top (sits above all other windows)
- Frameless design with rounded corners (8px border-radius)
- Semi-transparent background (80% opacity) until focused
- Appears in <100ms (feels instant)

**Input Field:**
- Auto-focused text field (cursor ready, no click needed)
- Multi-line input (3-5 lines visible, expands to 10 lines)
- Placeholder text: "Quick capture... (Esc to cancel, Enter to save)"
- Character counter shows remaining (no hard limit, but warn at 500 chars)
- Syntax highlighting for task markers: `@work`, `#urgent`, `due:tomorrow`

**Save Behavior:**
- **Enter key**: Save and close window (single-line capture)
- **Ctrl+Enter**: Save and close window (multi-line capture)
- **Esc key**: Cancel and close window (no save)
- Save completes in <500ms
- Success feedback: Brief green flash + sound (optional, configurable)
- Capture stored locally immediately (offline-first)
- Sync to Supabase in background (non-blocking)

**Error Handling:**
- If save fails: Show error banner, keep window open, retry button
- Lost focus: Window stays open (doesn't auto-close)
- Multiple hotkey presses: Focus existing window (don't open duplicates)

**And** hotkey is customizable  
**Then** user can change in Settings → Capture → Global Hotkey

**Prerequisites:** Story 1.1 (project setup), Story 1.2 (local database)

**Technical Notes:**
- Use `hotkey_manager` package for Windows global hotkey registration
- Capture window is a separate Flutter window (not main app window)
- Register hotkey on app startup, unregister on exit
- Handle hotkey conflicts gracefully (show error if hotkey already used)
- Store captures in `Captures` table with `category: 'uncategorized'` initially

---

### Story 2.2: Mobile Widget Capture (Android)

**As a** mobile user  
**I want** a home screen widget that opens instant capture  
**So that** I can save thoughts in <3 seconds without hunting for the app icon

**Acceptance Criteria:**

**Given** Life.D installed on Android 12+  
**When** user adds home screen widget  
**Then** widget options:

**Widget Sizes:**
- **3x1 widget**: Single button "Quick Capture +"
- **4x1 widget**: Text input field + save button
- Both sizes launch capture screen on tap

**Widget Appearance:**
- Dark/light theme follows system settings
- App icon + "Life.D" branding visible
- Minimal design (no clutter)
- Updates when app theme changes

**Capture Screen (launched from widget):**
- Full-screen overlay (not separate activity—feels faster)
- Large text input field (auto-focused, keyboard auto-opens)
- Top bar: "Quick Capture" title + Close button (X)
- Bottom bar: Save button (primary color, prominent)
- Swipe down to dismiss (gestures feel natural on mobile)

**Save Behavior:**
- Tap Save button: Store locally, show success toast, close screen
- Save completes in <500ms
- Success feedback: Haptic vibration + "Saved ✓" toast
- Offline support: Works without internet
- Background sync: Queued for sync when online

**And** widget is configurable  
**Then** long-press widget → Widget Settings:
- Choose widget size (3x1 or 4x1)
- Toggle auto-categorization (on by default)
- Toggle haptic feedback (on by default)

**Prerequisites:** Story 1.2 (local database), Story 2.1 (capture logic)

**Technical Notes:**
- Use `home_widget` package for Android widget support
- Widget communicates with app via `MethodChannel` (platform-specific code)
- Capture screen is Flutter activity (not native Android)
- Store captures same as desktop (unified data model)
- Test on multiple Android versions (12, 13, 14)

---

### Story 2.3: Auto-Categorization Engine

**As a** user  
**I want** my captures automatically categorized as task, note, or journal entry  
**So that** I don't have to manually organize everything (reduces friction)

**Acceptance Criteria:**

**Given** a new capture is saved  
**When** auto-categorization engine analyzes content  
**Then** classification rules:

**Task Indicators (→ category: 'task'):**
- Starts with action verbs: "Call", "Email", "Buy", "Fix", "Schedule", "Remember to", "Don't forget"
- Contains deadline keywords: "tomorrow", "next week", "by Friday", "due", "deadline"
- Contains task markers: `@work`, `@personal`, `#urgent`, `#important`
- Contains time indicators: "9am", "3pm", "in 2 hours"
- Question format: "Did I...?", "Should I...?"

**Journal Indicators (→ category: 'journal'):**
- Emotional language: "felt", "feeling", "emotions", "thoughts", "realized"
- Self-reflection: "I noticed", "I think", "I wonder", "Today was"
- Ratings mentioned: "8/10", "feeling 7", "energy level 6"
- Contains journal categories: "relationship", "work", "energy", "mood"

**Note Indicators (→ category: 'note'):**
- Informational: "Note:", "Remember:", "Idea:", "Thought:"
- URLs present (links to save for later)
- Code snippets (backticks or programming keywords)
- Lists (bullet points, numbered items)
- Longer than 100 characters without task/journal indicators

**Default (when uncertain):**
- If no clear indicators: category = 'note'
- User can manually reclassify later

**And** auto-categorization is fast  
**Then** classification completes in <100ms (doesn't block save)

**And** categorization is visible  
**Then** capture shows badge: 📝 Note | ✓ Task | 📔 Journal

**And** user can override  
**Then** tap category badge → dropdown → manually select different category

**Prerequisites:** Story 2.1 (desktop capture), Story 2.2 (mobile capture)

**Technical Notes:**
- Implement as rule-based classifier (not ML—too heavyweight for MVP)
- Use regex patterns for keyword matching
- Run classification in background isolate (doesn't block UI thread)
- Store classification confidence score (for future ML enhancements)
- Log misclassifications for future training data

---

### Story 2.4: Captures List View & Search

**As a** user  
**I want** to view all my captures in one place and search by keyword  
**So that** I can find that idea I captured last week (ADHD memory is unreliable)

**Acceptance Criteria:**

**Given** user navigates to Captures screen  
**When** viewing captures list  
**Then** display shows:

**List Layout:**
- Reverse chronological order (newest first)
- Each item shows:
  - Content (first 100 characters, "..." if truncated)
  - Category badge (📝 Note | ✓ Task | 📔 Journal)
  - Context tags (if any): `@work` `#urgent`
  - Timestamp: "2 mins ago", "1 hour ago", "Yesterday", "Nov 14"
  - Sync status: ✓ Synced | ⟳ Syncing | ⚠ Pending
- Tap item → expand to full content
- Swipe actions:
  - Swipe right: Convert to Task
  - Swipe left: Delete (with undo option)
- Pull to refresh: Trigger manual sync

**Search Functionality:**
- Search bar at top (auto-focuses on scroll up)
- Real-time filtering as user types
- Searches: content, tags, category
- Highlights matching keywords in results
- Search completes in <100ms (even with 1000 captures)

**Filtering:**
- Filter by category: All | Tasks | Notes | Journals
- Filter by tags: Show tag cloud, tap to filter
- Filter by date range: Today | This Week | This Month | All Time
- Multiple filters combine (AND logic)

**Empty States:**
- No captures: "No captures yet. Press Ctrl+Shift+L to start!"
- No search results: "No matches for 'keyword'. Try different terms."

**And** list is performant  
**Then** lazy loading loads 20 items at a time, smooth 60fps scrolling

**Prerequisites:** Story 2.1-2.3 (capture system)

**Technical Notes:**
- Use `ListView.builder` for efficient rendering
- Implement full-text search with SQLite FTS5 (fast)
- Cache search results (invalidate on new captures)
- Use `Dismissible` widget for swipe actions
- Show "deleted" state for 3 seconds with undo button

---

### Story 2.5: Context Tags & Manual Reclassification

**As a** user  
**I want** to tag captures with context (@work, @personal) and manually change categories  
**So that** I can organize thoughts my way (not just auto-categorization)

**Acceptance Criteria:**

**Given** user is viewing a capture  
**When** adding context tags  
**Then** tag UI allows:

**Tag Input:**
- Tap "+ Add tag" button → tag input field appears
- Type `@work`, `@personal`, `@relationship`, `@health`, `#urgent`, `#important`
- Autocomplete suggests existing tags as user types
- Tags saved immediately (no explicit "Save" button)
- Multiple tags allowed per capture
- Tags shown as colored chips (customizable colors in settings)

**Tag Management:**
- Tap tag chip → remove tag (with confirmation)
- Long-press tag → rename tag globally (affects all captures with that tag)
- Settings → Manage Tags: View all tags, set colors, merge duplicates

**Manual Reclassification:**
- Tap category badge (📝 Note | ✓ Task | 📔 Journal)
- Dropdown menu: Note | Task | Journal
- Select new category → saves immediately
- If reclassified to Task: Prompt to add due date (optional)
- If reclassified to Journal: Prompt to add ratings (optional)

**Bulk Actions:**
- Select multiple captures (checkbox mode)
- Bulk add tags to selected items
- Bulk reclassify selected items
- Bulk delete with confirmation

**And** tags are searchable  
**Then** search `@work` shows all work-tagged captures, `#urgent` shows urgent items

**Prerequisites:** Story 2.4 (captures list view)

**Technical Notes:**
- Store tags as JSON array in `contextTags` column
- Index `contextTags` for fast searching (use SQLite JSON functions)
- Tag colors stored in Settings table
- Implement tag autocomplete with Trie data structure (fast prefix matching)

---

## Epic 3: Proactive Task/Event Management

**Goal:** Make it impossible to miss tasks/events by surfacing them at the right time without requiring search.

**Value:** Core product mission—never miss anything again.

**FR Coverage:** FR9-FR17 (task management), FR26-FR33 (ambient dashboard)

### Story 3.1: Create & Edit Tasks

**As a** user  
**I want** to create tasks with title, due date, priority, and context tags  
**So that** I can capture what needs doing with enough detail to act on it later

**Acceptance Criteria:**

**Given** user taps "New Task" button or converts a capture to task  
**When** task creation screen opens  
**Then** form fields:

**Required Fields:**
- **Title**: Text input (max 200 chars), auto-focused
- Placeholder: "What needs to be done?"

**Optional Fields:**
- **Description**: Multi-line text (max 1000 chars)
- Placeholder: "Add details..."
- **Due Date**: Date picker (tomorrow by default)
- Quick options: Today | Tomorrow | This Week | Next Week | Custom
- **Due Time**: Time picker (optional, defaults to 9am if not set)
- **Priority**: Radio buttons (Low | Medium | High | Urgent)
- Visual indicators: Low=gray, Medium=blue, High=orange, Urgent=red
- **Context Tags**: Tag input (same as Story 2.5)
- **Recurring**: Toggle switch + recurrence picker
- Options: Daily | Weekly | Monthly | Custom interval

**Save Behavior:**
- Tap "Save" button: Validate (title required), save to local DB, close screen
- Save completes in <300ms
- Success feedback: "Task created ✓" toast
- Auto-sync to Supabase in background

**Edit Task:**
- Tap any task → opens edit screen (same form, pre-populated)
- Changes save immediately on field blur (no explicit "Save" button)
- "Delete Task" button at bottom (with confirmation)

**And** task creation is fast  
**Then** default task (just title + due date) creates in <1 second end-to-end

**Prerequisites:** Story 1.2 (local database), Story 2.5 (tags)

**Technical Notes:**
- Use `Form` widget with `TextFormField` for validation
- Store tasks in `Tasks` table (see Story 1.2 schema)
- Implement `TaskRepository` for CRUD operations
- Use `DatePicker` and `TimePicker` widgets (Material Design)
- Recurrence stored as JSON: `{"type": "weekly", "interval": 1, "daysOfWeek": [1,3,5]}`

---

### Story 3.2: Recurring Tasks Logic

**As a** user  
**I want** tasks to automatically recreate on schedule (daily, weekly, monthly)  
**So that** I don't forget routine commitments (relationship check-ins, health routines)

**Acceptance Criteria:**

**Given** user creates task with recurrence enabled  
**When** task is marked complete  
**Then** recurrence engine:

**Recurrence Types:**
- **Daily**: Repeats every N days
- **Weekly**: Repeats every N weeks on specific days (Mon, Wed, Fri)
- **Monthly**: Repeats every N months on specific day (1st, 15th, last day)
- **Custom**: Cron-style expression (advanced users)

**Recreation Logic:**
- When task marked complete → check recurrence rule
- If recurring: Create new task with same title, description, tags, priority
- New due date calculated based on recurrence rule:
  - Daily: `originalDueDate + N days`
  - Weekly: Next occurrence of selected weekday
  - Monthly: Same day next month (or last day if month shorter)
- Original task archived (not deleted) for weekly review

**Edge Cases:**
- Complete task early: Next occurrence calculated from completion date (not original due date)
- Skip instance: Allow user to "Skip this occurrence" (doesn't recreate)
- End recurrence: Allow user to set end date or occurrence count

**And** recurrence is visible  
**Then** recurring tasks show icon 🔁 and next occurrence date

**And** recurring tasks respect time blindness  
**Then** reminders start earlier for recurring tasks (remind 1 day before, not just 1 hour)

**Prerequisites:** Story 3.1 (create tasks)

**Technical Notes:**
- Implement `RecurrenceEngine` service (background job)
- Run recurrence check on task completion + daily at midnight
- Use `cron` package for cron-style expressions (advanced feature)
- Store recurrence rule as JSON in `Tasks.recurrence` column
- Archived tasks kept in database (with `isArchived` flag) for history

---

### Story 3.3: Import Calendar Events (Google Calendar Read-Only)

**As a** user  
**I want** to import my Google Calendar events  
**So that** I see all my obligations (tasks + events) in one unified timeline

**Acceptance Criteria:**

**Given** user navigates to Settings → Calendar Integration  
**When** user taps "Connect Google Calendar"  
**Then** OAuth flow:

**Authorization:**
- Opens Google OAuth consent screen (in-app browser)
- Requests permissions: Read-only access to Google Calendar (`https://www.googleapis.com/auth/calendar.readonly`)
- User approves → app receives OAuth token
- Token stored securely (`flutter_secure_storage`)
- Token auto-refreshes before expiration

**Calendar Selection:**
- After auth: Show list of user's calendars (with checkboxes)
- User selects which calendars to import (default: primary calendar only)
- Save selections to Settings

**Event Import:**
- Fetch events from selected calendars (next 30 days)
- Store in local `CalendarEvents` table (new table, similar to Tasks):
  ```dart
  class CalendarEvents extends Table {
    IntColumn get id => integer().autoIncrement()();
    TextColumn get title => text()();
    DateTimeColumn get startTime => dateTime()();
    DateTimeColumn get endTime => dateTime()();
    TextColumn get location => text().nullable()();
    TextColumn get description => text().nullable()();
    TextColumn get googleEventId => text().unique()();
    TextColumn get calendarId => text()();
    DateTimeColumn get lastSyncedAt => dateTime()();
  }
  ```
- Import completes in <5 seconds for 100 events
- Refresh events automatically every 1 hour when app is open

**Display:**
- Calendar events appear in unified timeline alongside tasks
- Distinguished visually: Calendar icon 📅 vs Task icon ✓
- Tapping event shows details (read-only, can't edit external events)

**And** calendar sync is observable  
**Then** Settings shows:
- Connected calendars list
- Last sync timestamp
- Manual "Sync Now" button

**And** errors are handled  
**Then** if OAuth revoked: Show "Reconnect Google Calendar" prompt

**Prerequisites:** Story 1.3 (auth), Story 3.1 (tasks)

**Technical Notes:**
- Use `google_sign_in` + `googleapis` packages for Google Calendar API
- Implement incremental sync (fetch only events changed since last sync)
- Handle rate limits (Google Calendar API: 1M requests/day)
- Store minimal event data (not full event object—reduces storage)
- **Optional for MVP:** Support Outlook Calendar in Phase 2 (same pattern)

---

### Story 3.4: Unified Timeline View (Tasks + Calendar Events)

**As a** user  
**I want** to see tasks and calendar events together in one timeline  
**So that** I know what's coming without switching between apps

**Acceptance Criteria:**

**Given** user has tasks and calendar events  
**When** viewing unified timeline  
**Then** display modes:

**"Today" View:**
- Current time indicator (red line)
- Events/tasks sorted chronologically
- Time-blocked layout:
  - 9:00 AM - Meeting with team 📅
  - 10:30 AM - Call Sarah ✓ (task)
  - 12:00 PM - Lunch 📅
  - 2:00 PM - Finish report ✓ (task, due today)
- Tasks without specific time appear at bottom ("Also today:")
- Overdue tasks highlighted in red at top
- Completed tasks grayed out (with strikethrough)

**"This Week" View:**
- Grouped by day (Today, Tomorrow, Wed, Thu, Fri, Weekend)
- Collapsed by default (tap to expand day)
- Shows count per day: "Tomorrow (3 items)"
- Same time-blocked layout within each day

**"Now" View (special):**
- Shows ONLY items needing immediate attention:
  - Overdue tasks (due < now)
  - Events happening now (startTime < now < endTime)
  - Tasks due within 1 hour
  - Urgent priority tasks (regardless of due date)
- Empty state: "Nothing urgent right now. You're on track! ✓"

**Interaction:**
- Tap task → opens task edit screen
- Tap calendar event → shows event details (read-only)
- Swipe task right → mark complete
- Swipe task left → snooze (reschedule to later today or tomorrow)
- Pull to refresh → re-fetch calendar events + re-render timeline

**And** timeline is performant  
**Then** renders 50 items in <200ms, smooth 60fps scrolling

**Prerequisites:** Story 3.1 (tasks), Story 3.3 (calendar import)

**Technical Notes:**
- Combine `Tasks` and `CalendarEvents` queries with SQL `UNION`
- Sort by `dueDate`/`startTime` ASC, then by `priority` DESC
- Use `SliverList` for efficient scrolling (lazy loading)
- Cache timeline data (invalidate on task/event changes)
- Implement "jump to now" FAB (floating action button)

---

### Story 3.5: Ambient Dashboard ("Now", "Today", "This Week" Tabs)

**As a** user  
**I want** the app to always show me what matters RIGHT NOW without searching  
**So that** I never miss deadlines or forget what needs attention (ADHD working memory)

**Acceptance Criteria:**

**Given** user opens Life.D app  
**When** landing on Home screen  
**Then** dashboard layout:

**Tab Navigation (bottom tabs):**
- **Now** tab: Urgent items only (see Story 3.4 "Now" view)
- **Today** tab: Full day timeline (see Story 3.4 "Today" view)
- **This Week** tab: Week overview (see Story 3.4 "This Week" view)
- **Journal** tab: Quick access to journal prompt
- **More** tab: Settings, captures, weekly review

**"Now" Tab (default view on app open):**
- Hero section at top: Time until next deadline
  - "Meeting in 23 minutes" (countdown timer, updates every second)
  - Large, impossible-to-miss text (32px font)
  - Red if <15 mins, orange if <1 hour, blue otherwise
- List of urgent items below (see Story 3.4)
- FAB (floating action button): "+ Quick Capture"

**Real-Time Updates:**
- Dashboard refreshes automatically every 1 minute
- Countdown timers update every second
- New tasks appear immediately (no manual refresh)
- Completed tasks removed with animation

**Visual Priority:**
- Overdue tasks: Red background, ⚠️ icon
- Due soon (<1 hour): Orange background, ⏰ icon
- Urgent priority: Red badge
- High priority: Orange badge
- Medium priority: Blue badge
- Low priority: Gray badge (subtle)

**Empty States:**
- Now tab empty: "Nothing urgent. You're on track! ✓" + motivational message
- Today tab empty: "No tasks today. Enjoy the free time! 🎉"
- Week tab empty: "Clear week ahead. Time to plan!" 

**And** dashboard is ADHD-friendly  
**Then**:
- High contrast colors (passes WCAG AA)
- Large touch targets (44x44px minimum)
- Clear visual hierarchy (most important = largest, boldest)
- No cluttered information (show only essential data)
- Smooth animations (reduce cognitive load)

**Prerequisites:** Story 3.4 (unified timeline)

**Technical Notes:**
- Use `TabBarView` for tab navigation (Material Design)
- Implement `StreamBuilder` for real-time countdown updates
- Use `AnimatedList` for smooth item additions/removals
- Cache dashboard data (refresh on pull-down or every 1 min)
- Show skeleton loaders while data loading (avoid blank screens)

---

_Epic 3 continues with Stories 3.6-3.10 covering task dependencies, snooze, archiving, quick actions, and weekly task review._
_Epics 4-6 will follow the same detailed BDD format covering Smart Reminders, Journaling, and Settings/Data Portability._

**Total Story Count (estimated):**
- Epic 1: 5 stories
- Epic 2: 5 stories  
- Epic 3: 10 stories (5 shown above + 5 more)
- Epic 4: 8 stories (smart reminders)
- Epic 5: 12 stories (journaling + weekly review)
- Epic 6: 8 stories (settings + data portability)

**TOTAL: ~48 user stories** to implement full MVP (67 functional requirements).

---

## Next Steps

This document will be updated by subsequent workflows:
1. **UX Design workflow** → Adds wireframes/mockups to each story
2. **Architecture workflow** → Adds technical architecture diagrams + API specs
3. **Implementation** → Marks stories complete, adds retrospective learnings

[c] Continue with remaining stories for Epics 3-6 | [stop] This detail is sufficient
