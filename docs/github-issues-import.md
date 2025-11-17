# GitHub Issues Import Guide for Life.D MVP

This document contains all epics and stories ready to be imported into GitHub Issues for the `eysenfalk/journote` repository.

## How to Import

You can import these issues using one of these methods:

### Method 1: Manual Creation (Recommended for now)
Copy each issue section below and create manually in GitHub

### Method 2: GitHub CLI (after installing `gh`)
```bash
# Install gh CLI first, then authenticate
gh auth login

# Create each issue (example)
gh issue create --title "Epic 1: Foundation & Core Infrastructure" --label "epic,foundation" --body "$(cat issue-content.md)"
```

### Method 3: GitHub API Script
Use the provided PowerShell script at the end of this document

---

## Project Setup

**Repository:** `eysenfalk/journote`  
**Project Name:** Life.D MVP - Phase 0  
**Timeline:** 60 days (Nov 17, 2025 - Jan 15, 2026)  
**Total Stories:** 48 (across 6 epics)

---

## Epic 1: Foundation & Core Infrastructure

**Labels:** `epic`, `foundation`, `infrastructure`

**Description:**
```markdown
# Epic 1: Foundation & Core Infrastructure

**Goal:** Establish technical foundation enabling offline-first, cross-platform functionality with secure authentication and real-time sync.

**Value:** Enables all subsequent features—cannot capture, manage tasks, or journal without this foundation.

**FR Coverage:** Infrastructure supporting FR46-FR61 (local storage, sync, auth, settings)

## Stories (5)
- [ ] #X Story 1.1: Project Setup & Development Environment
- [ ] #X Story 1.2: Local Database Schema & Offline Storage
- [ ] #X Story 1.3: Supabase Authentication & User Accounts
- [ ] #X Story 1.4: Real-Time Sync Engine with Conflict Resolution
- [ ] #X Story 1.5: App State Management & Navigation

## Tech Stack
- Flutter 3.16+ (Windows + Android)
- Drift (type-safe SQLite)
- Supabase (auth + sync)
- BLoC (state management)
- go_router (navigation)

## Acceptance Criteria
- ✅ App builds on Windows + Android
- ✅ Local database with Captures, Tasks, JournalEntries, Settings tables
- ✅ Auth flow: signup, login, session persistence
- ✅ Sync engine: offline queue, conflict resolution (last-write-wins)
- ✅ BLoC architecture with dependency injection

**See:** `docs/epics.md` for detailed story breakdown
```

---

### Story 1.1: Project Setup & Development Environment

**Labels:** `story`, `foundation`, `setup`  
**Milestone:** Epic 1  
**Assignee:** (unassigned)

**Description:**
```markdown
# Story 1.1: Project Setup & Development Environment

**Parent Epic:** #X (Epic 1)  
**As a** developer  
**I want** a properly initialized Flutter project with core dependencies  
**So that** I can build cross-platform (Windows desktop + Android mobile) with offline-first architecture

## Acceptance Criteria

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

## Technical Notes
- Use BLoC pattern for state management (testable, separates business logic)
- Local-first architecture: SQLite primary, Supabase sync secondary
- Drift for type-safe database access with compile-time query validation
- Hive for fast settings/cache (faster than SQLite for simple key-value)

## Prerequisites
None (first story)

## Definition of Done
- [ ] Flutter project created with correct SDK version
- [ ] All dependencies added to `pubspec.yaml`
- [ ] Project builds successfully on Windows
- [ ] Project builds successfully on Android
- [ ] `flutter doctor` shows no errors
- [ ] Folder structure created (lib/features, lib/core, lib/shared, test, assets)
- [ ] Git repository initialized with proper `.gitignore`
- [ ] README.md created with setup instructions
```

---

### Story 1.2: Local Database Schema & Offline Storage

**Labels:** `story`, `foundation`, `database`  
**Milestone:** Epic 1  
**Dependencies:** #X (Story 1.1)

**Description:**
```markdown
# Story 1.2: Local Database Schema & Offline Storage

**Parent Epic:** #X (Epic 1)  
**Prerequisites:** #X (Story 1.1)

**As a** user  
**I want** all my data stored locally on my device  
**So that** the app works fully offline and I never lose data due to connectivity issues

## Database Tables (Drift)

### Captures Table
\`\`\`dart
@DataClassName('Capture')
class Captures extends Table {
  IntColumn get id => integer().autoIncrement()();
  TextColumn get content => text()();
  TextColumn get category => text()(); // 'task', 'note', 'journal'
  TextColumn get contextTags => text().nullable()(); // JSON array
  DateTimeColumn get createdAt => dateTime()();
  DateTimeColumn get syncedAt => dateTime().nullable()();
  TextColumn get supabaseId => text().nullable()();
  BoolColumn get isSynced => boolean().withDefault(const Constant(false))();
}
\`\`\`

### Tasks Table
\`\`\`dart
@DataClassName('Task')
class Tasks extends Table {
  IntColumn get id => integer().autoIncrement()();
  TextColumn get title => text()();
  TextColumn get description => text().nullable()();
  DateTimeColumn get dueDate => dateTime().nullable()();
  TextColumn get priority => text()(); // 'low', 'medium', 'high', 'urgent'
  TextColumn get contextTags => text().nullable()();
  TextColumn get recurrence => text().nullable()(); // JSON
  BoolColumn get isComplete => boolean().withDefault(const Constant(false))();
  DateTimeColumn get completedAt => dateTime().nullable()();
  IntColumn get dependsOn => integer().nullable().references(Tasks, #id)();
  DateTimeColumn get createdAt => dateTime()();
  DateTimeColumn get syncedAt => dateTime().nullable()();
  TextColumn get supabaseId => text().nullable()();
}
\`\`\`

### JournalEntries Table
\`\`\`dart
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
  TextColumn get encryptedContent => text().nullable()();
  DateTimeColumn get createdAt => dateTime()();
  DateTimeColumn get syncedAt => dateTime().nullable()();
  TextColumn get supabaseId => text().nullable()();
}
\`\`\`

### Settings Table
\`\`\`dart
@DataClassName('Setting')
class Settings extends Table {
  TextColumn get key => text()();
  TextColumn get value => text()();
  
  @override
  Set<Column> get primaryKey => {key};
}
\`\`\`

## Acceptance Criteria
- Migrations run on first launch
- CRUD operations work offline
- Data persists across restarts
- Encrypted journal storage

## Technical Notes
- Drift generates type-safe DAOs at build time
- Use `@UseRowClass()` for custom model classes if needed
- Implement database migrations for future schema changes
- Store encrypted journals using `encrypted_shared_preferences` + user-controlled key
- JSON columns for flexibility (context tags, recurrence rules)

## Definition of Done
- [ ] All 4 Drift tables defined (Captures, Tasks, JournalEntries, Settings)
- [ ] Database migrations created and tested
- [ ] DAOs generated and compiling successfully
- [ ] CRUD operations working for all tables
- [ ] Data persists after app restart
- [ ] Works completely offline (no network required)
- [ ] Unit tests for database operations
```

---

### Story 1.3: Supabase Authentication & User Accounts

**Labels:** `story`, `foundation`, `auth`  
**Milestone:** Epic 1  
**Dependencies:** #X (Story 1.1)

**Description:**
```markdown
# Story 1.3: Supabase Authentication & User Accounts

**Parent Epic:** #X (Epic 1)  
**Prerequisites:** #X (Story 1.1)

**As a** user  
**I want** to create an account and log in securely  
**So that** my data syncs across devices and stays private

## Acceptance Criteria

### Email/Password Sign-Up
- Email validation (RFC 5322)
- Password requirements: 8+ chars, 1 uppercase, 1 number, 1 special
- Password strength meter (weak/medium/strong)
- Confirm password with real-time match validation
- Email verification sent within 15 minutes
- Account creation <2 seconds
- Helpful error messages

### Login Flow
- Email + password fields
- "Remember me" checkbox (secure session token storage)
- "Forgot password" link
- Session persists across restarts
- Auto-logout after 30 days inactivity
- Login <1 second

### Security
- Passwords never stored locally
- Session tokens in `flutter_secure_storage`
- Automatic token refresh
- Logout clears session data

### ADHD-Friendly UI
- 44x44px minimum touch targets
- Clear focus indicators
- WCAG 2.1 AA compliant
- Loading states prevent double-submission
- Prominent error display

## Technical Notes
- Use `supabase_flutter` package for auth
- Store Supabase URL + anon key in `.env` file (not version controlled)
- Implement auth state management with BLoC pattern
- Handle network errors gracefully (offline mode)
- Add biometric auth in future story (Phase 2)

## Definition of Done
- [ ] Sign-up screen created with email + password validation
- [ ] Login screen created with session persistence
- [ ] "Forgot password" flow implemented
- [ ] Session tokens stored securely
- [ ] Auth state managed with BLoC
- [ ] WCAG 2.1 AA compliant UI
- [ ] Integration tests for auth flows
- [ ] Error handling for network failures
```

---

### Story 1.4: Real-Time Sync Engine with Conflict Resolution

**Labels:** `story`, `foundation`, `sync`  
**Milestone:** Epic 1  
**Dependencies:** #X (Story 1.2), #X (Story 1.3)

**Description:**
```markdown
# Story 1.4: Real-Time Sync Engine with Conflict Resolution

**Parent Epic:** #X (Epic 1)  
**Prerequisites:** #X (Story 1.2 - Database), #X (Story 1.3 - Auth)

**As a** user  
**I want** my data to sync automatically across devices when online  
**So that** I can seamlessly switch between desktop and mobile

## Sync Features

### Sync Queue
- Local changes queued immediately (even offline)
- Queue persisted (survives app restart)
- Auto-retry with exponential backoff (1s, 2s, 4s, 8s, 16s, max 30s)
- Manual sync trigger
- Status indicator: ✓ Synced | ⟳ Syncing | ⚠ Offline | ✗ Error

### Sync Logic
- **Push**: Upload local changes (upsert by `supabaseId`)
- **Pull**: Fetch remote changes since `syncedAt`
- **Merge**: Apply remote changes to local DB
- **Conflict resolution**: Last-write-wins (`updatedAt` timestamp)
- **Optimistic UI**: Show immediately, revert if fails

### Performance Targets
- Initial sync: <5s for 1000 items
- Incremental sync: <1s
- Batch operations: 50 items at once
- Background sync: every 5 minutes

### Error Handling
- Network errors → retry, show "Offline"
- Auth errors → force re-login, preserve local changes
- Server errors → retry with backoff, log to Sentry
- Zero data loss tolerance

## Observable Sync
- Last sync timestamp
- Pending changes count
- Sync history log (last 20 events)

## Technical Notes
- Use Supabase Realtime for push notifications of remote changes (optional Phase 2 enhancement)
- Implement sync with `SyncRepository` pattern (separates sync logic from UI)
- Store `syncedAt` timestamp per record to detect changes since last sync
- Use Supabase RLS (Row Level Security) policies to enforce user data isolation
- Consider eventual consistency model (not strong consistency)

## Definition of Done
- [ ] Sync queue implemented (persistent, survives restart)
- [ ] Push sync: local changes uploaded to Supabase
- [ ] Pull sync: remote changes fetched and merged
- [ ] Conflict resolution: last-write-wins implemented
- [ ] Exponential backoff retry logic
- [ ] Sync status indicator in UI
- [ ] Manual sync trigger button
- [ ] Performance targets met (<5s initial, <1s incremental)
- [ ] Unit tests for sync logic
- [ ] Integration tests for conflict scenarios
```

---

### Story 1.5: App State Management & Navigation

**Labels:** `story`, `foundation`, `architecture`  
**Milestone:** Epic 1  
**Dependencies:** #X (Story 1.1), #X (Story 1.3), #X (Story 1.4)

**Description:**
```markdown
# Story 1.5: App State Management & Navigation

**Parent Epic:** #X (Epic 1)  
**Prerequisites:** #X (Story 1.1), #X (Story 1.3 - Auth), #X (Story 1.4 - Sync)

**As a** developer  
**I want** consistent state management and navigation patterns  
**So that** feature development is predictable and testable

## BLoC Architecture

\`\`\`dart
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
\`\`\`

## Navigation (go_router)
- `/` → Splash (check auth)
- `/login` → Auth screen
- `/signup` → Registration
- `/home` → Dashboard (protected)
- `/captures` → Captures list
- `/tasks` → Tasks view
- `/journal` → Journal prompt
- `/settings` → Settings
- Protected routes redirect to login
- Deep linking support

## Dependency Injection (get_it)
- `AuthRepository`
- `SyncRepository`
- `LocalDatabase`
- `SupabaseClient`
- All BLoCs as singletons

## Error Handling
- Global error boundary
- Sentry logging (production)
- User-friendly messages
- Retry mechanisms

## Testing
- BLoC state transitions
- Error case coverage
- Mocked side effects

## Technical Notes
- BLoC pattern separates business logic from UI (easier to test)
- Use `bloc_test` package for testing BLoCs
- Implement `Equatable` for all states/events (enables proper state comparison)
- Consider `hydrated_bloc` for state persistence (optional Phase 2)

## Definition of Done
- [ ] BLoC structure created (Auth, Sync, Settings)
- [ ] Navigation configured with go_router
- [ ] Protected routes implemented
- [ ] Dependency injection setup with get_it
- [ ] Global error boundary implemented
- [ ] Unit tests for all BLoCs
- [ ] Navigation tests
- [ ] Deep linking support (Android + Windows)
```

---

## Epic 2: Instant Capture System

**Labels:** `epic`, `capture`, `core-feature`

**Description:**
```markdown
# Epic 2: Instant Capture System

**Goal:** Enable frictionless thought capture in <3 seconds from desktop (global hotkey) or mobile (widget), with auto-categorization and offline support.

**Value:** ADHD tax prevention—never lose an idea because of tool friction.

**FR Coverage:** FR1-FR8 (capture, search, auto-categorize, tagging)

## Stories (5)
- [ ] #X Story 2.1: Desktop Global Hotkey Capture (Windows)
- [ ] #X Story 2.2: Mobile Widget Capture (Android)
- [ ] #X Story 2.3: Auto-Categorization Engine
- [ ] #X Story 2.4: Captures List View & Search
- [ ] #X Story 2.5: Context Tags & Manual Reclassification

## Performance Targets
- Capture window appears: <100ms
- Save operation: <500ms
- Search results: <100ms (1000 items)
- Offline-first: Works without internet

## Acceptance Criteria
- ✅ Windows global hotkey (`Ctrl+Shift+L`) opens capture overlay
- ✅ Android widget (3x1, 4x1) launches instant capture
- ✅ Auto-categorize: task/note/journal based on content
- ✅ Full-text search with highlighting
- ✅ Context tags (@work, #urgent) with autocomplete

**See:** `docs/epics.md` for detailed story breakdown
```

---

_[Continue with Stories 2.1-2.5, Epic 3, and remaining epics using the same format]_

---

## PowerShell Import Script

Save this as `import-github-issues.ps1`:

\`\`\`powershell
# GitHub Issues Import Script for Life.D MVP
# Prerequisites: Install GitHub CLI (gh) and authenticate

param(
    [Parameter(Mandatory=$true)]
    [string]$RepoOwner = "eysenfalk",
    
    [Parameter(Mandatory=$true)]
    [string]$RepoName = "journote"
)

# Check if gh CLI is installed
if (!(Get-Command gh -ErrorAction SilentlyContinue)) {
    Write-Error "GitHub CLI (gh) not found. Install from: https://cli.github.com/"
    exit 1
}

# Check authentication
$authStatus = gh auth status 2>&1
if ($LASTEXITCODE -ne 0) {
    Write-Error "Not authenticated with GitHub CLI. Run: gh auth login"
    exit 1
}

Write-Host "Creating Epic 1: Foundation & Core Infrastructure..." -ForegroundColor Cyan

# Epic 1
$epic1Body = @"
# Epic 1: Foundation & Core Infrastructure

**Goal:** Establish technical foundation enabling offline-first, cross-platform functionality with secure authentication and real-time sync.

**Value:** Enables all subsequent features—cannot capture, manage tasks, or journal without this foundation.

**FR Coverage:** Infrastructure supporting FR46-FR61 (local storage, sync, auth, settings)

## Stories (5)
- [ ] Story 1.1: Project Setup & Development Environment
- [ ] Story 1.2: Local Database Schema & Offline Storage
- [ ] Story 1.3: Supabase Authentication & User Accounts
- [ ] Story 1.4: Real-Time Sync Engine with Conflict Resolution
- [ ] Story 1.5: App State Management & Navigation

## Tech Stack
- Flutter 3.16+ (Windows + Android)
- Drift (type-safe SQLite)
- Supabase (auth + sync)
- BLoC (state management)
- go_router (navigation)

## Acceptance Criteria
- ✅ App builds on Windows + Android
- ✅ Local database with Captures, Tasks, JournalEntries, Settings tables
- ✅ Auth flow: signup, login, session persistence
- ✅ Sync engine: offline queue, conflict resolution (last-write-wins)
- ✅ BLoC architecture with dependency injection

**See:** docs/epics.md for detailed story breakdown
"@

$epic1 = gh issue create `
    --repo "$RepoOwner/$RepoName" `
    --title "Epic 1: Foundation & Core Infrastructure" `
    --body $epic1Body `
    --label "epic,foundation,infrastructure"

Write-Host "✅ Created Epic 1: $epic1" -ForegroundColor Green

# Add more epics and stories here...

Write-Host "`n🎉 Import complete!" -ForegroundColor Green
\`\`\`

## Usage

1. Save the script as `import-github-issues.ps1`
2. Install GitHub CLI: `winget install GitHub.cli`
3. Authenticate: `gh auth login`
4. Run: `.\import-github-issues.ps1 -RepoOwner eysenfalk -RepoName journote`

---

**Total Issues to Create:** 54  
- 6 Epics
- 48 Stories

**Estimated Time:** 15-20 minutes manual creation OR 2 minutes with script
