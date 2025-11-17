# Life.D - Product Requirements Document

**Author:** Falk
**Date:** 2025-11-15
**Version:** 1.0

---

## Executive Summary

Life.D is a personal ADHD life management tool built to solve one problem: **never miss or search for tasks/events again**.

**The Core Problem:**
ADHD working memory means tasks and events vanish. Current tools require YOU to remember to check them. Life.D inverts this: the app remembers FOR you and surfaces what matters WHEN it matters.

**What Makes This Special:**
Unlike Notion/Obsidian (you must search) or Apple Reminders (notification noise), Life.D combines:
1. **Zero-search task/event system** - Smart reminders + ambient dashboard = never miss anything
2. **Instant capture** - Thought → saved in <3 seconds, anywhere
3. **Life-systems journaling** - Detect invisible self-changes ("you've been cold lately") BEFORE external feedback

**Success Metric:**
Zero missed tasks/events for 30 days. That's it. Everything else (graphs, AI, sharing) is bonus.

**Personal Tool First:** Built for Falk's ADHD brain. Maybe shared later if it works.

---

## Project Classification

**Type:** Mobile + Desktop App (Flutter)  
**Domain:** ADHD-specific productivity / Mental health support  
**Complexity:** Medium-High (ADHD-native UX + real-time sync + future AI)  
**Platform Priority:** Mobile-first (60% ADHD users), desktop for capture/power features

**ADHD as Core Domain:**
Every design decision is filtered through "Does this work for ADHD brains?" Not "ADHD-friendly" features added later—ADHD considerations ARE the architecture.

---

## Success Criteria

### Primary Success: Never Miss Tasks/Events

**30-Day Test (December 2025):**
- ✅ **Zero missed tasks** - Did everything that needed doing (or consciously chose not to)
- ✅ **Zero missed events** - Made every meeting, appointment, commitment
- ✅ **Zero searches** - Never had to hunt for "what was that thing I needed to do?"
- ✅ **App surfaced everything** - Right task/event appeared at right time

**If ALL true:** Success. Keep using.  
**If ANY false:** Failure. Fix or kill.

### Secondary Success: Catch Invisible Self-Changes

**30-Day Test:**
- ✅ Weekly review showed at least ONE pattern I missed consciously
- ✅ Caught mood/energy/behavior shift BEFORE external feedback
- ✅ Girlfriend notices I'm more aware/present

**This is bonus.** Primary success = never miss tasks/events.

### Kill Criteria

**Week 2:**
- Missed 3+ tasks/events → fundamental failure
- Opened app <5 days → not using it
- Still using Apple Notes/Reminders → didn't replace kludge

**Week 4:**
- <50% journal completion → not sticky
- Went back to old tools → failed to deliver value

---

## Product Scope

### MVP Phase 0 (December 2025 - 60 Days)

**Core Mission: Make it impossible to miss tasks/events**

#### Priority #1: Proactive Task/Event System

**Task Management:**
- Create tasks from captures or standalone
- Due dates, priorities, recurring schedules
- Calendar event integration (import, don't own the calendar)
- Context tags (work, personal, relationship, health)

**Smart Reminders (ADHD-Optimized):**
- Escalating notifications (gentle → persistent as deadline approaches)
- Location-aware (surface "grocery list" when near store)
- Context-aware (show work tasks during work hours, not 11pm)
- Snooze intelligence (not forever—resurfaces smartly)

**Ambient Dashboard:**
- "Now" view: What needs attention RIGHT NOW
- "Today" view: Full day overview, time-blocked
- "This Week" view: Upcoming obligations visible
- No searching needed—app shows you what matters

**Why First:** If this doesn't work, nothing else matters. Must nail the core problem.

#### Priority #2: Instant Capture

- Desktop global hotkey (Windows primary)
- Mobile widget (Android secondary)
- Text input (<3 seconds thought → saved)
- Auto-categorize to task vs note vs journal entry
- Offline-first, syncs when connected

**Why Second:** Can't manage what you don't capture. ADHD tax is real.

#### Priority #3: Life-Systems Journaling

**Evening Prompt (<2 minutes):**
- Relationships: 1-10 + optional note
- Work: 1-10 + optional note
- Energy: 1-10 + optional note
- Mood: 1-10 + optional note
- Quick reflection: Anything noticed about myself?

**Weekly Review (Sunday, 5 minutes):**
- Trend lines: This week vs last week
- Pattern highlights: "Relationship score dropped 8→6 over 3 days"
- Forces awareness: "What changed?"

**Why Third (but still MVP):** Detects invisible self-changes. Differentiator from commodity task apps.

### What's NOT in Phase 0

**Explicitly cut for speed:**
- ❌ Graph visualization (Phase 3)
- ❌ AI pattern detection (Phase 3)
- ❌ Habit tracking (recurring tasks handle this)
- ❌ Todoist/Google Calendar/Apple Health sync (OAuth hell)
- ❌ Voice notes (text covers 90%)
- ❌ Browser extension (desktop + mobile enough)
- ❌ Social/sharing features (personal tool first)
- ❌ Gamification/streaks (not needed for core value)

**Rule:** Only add features if 10+ users request AND it serves core mission (never miss tasks/events).

### Technical Foundation

**Stack:**
- Flutter (cross-platform: Windows desktop, Android mobile)
- Supabase (backend, auth, real-time sync, Postgres)
- Local-first architecture (works offline, syncs online)

**Performance Targets:**
- App launch: <2 seconds
- Capture-to-save: <500ms (ADHD friction threshold)
- Sync latency: <1 second
- Notification reliability: 99.9% (cannot miss reminders)

**Why These:** You know Flutter. Supabase handles complexity. Local-first = no lag = no friction.

---

## Functional Requirements

**Purpose:** Complete inventory of capabilities Life.D must have to solve "never miss tasks/events" + detect invisible self-changes.

**Organization:** Grouped by capability area (what users/system can DO), not by technology layer.

**Altitude:** States WHAT exists and WHO it serves, NOT HOW it's implemented or specific UI details.

### Quick Capture

**FR1:** Users can capture thoughts via desktop global hotkey shortcut  
**FR2:** Users can capture thoughts via mobile home screen widget  
**FR3:** System saves captures in <500ms with offline support  
**FR4:** Users can view all captures in chronological list  
**FR5:** Users can search captures by text content  
**FR6:** System auto-categorizes captures as task, note, or journal entry based on content  
**FR7:** Users can manually convert captures to tasks or journal entries  
**FR8:** Users can tag captures with context (work, personal, relationship, health)

### Task & Event Management

**FR9:** Users can create tasks with title, due date, priority, and context tags  
**FR10:** Users can create recurring tasks (daily, weekly, monthly, custom intervals)  
**FR11:** Users can mark tasks as complete  
**FR12:** System automatically hides completed tasks from active views  
**FR13:** Users can import calendar events from external calendars (read-only integration)  
**FR14:** Users can view tasks and calendar events together in unified timeline  
**FR15:** Users can set task dependencies (task B depends on task A completion)  
**FR16:** Users can snooze tasks with intelligent rescheduling suggestions  
**FR17:** Users can archive tasks without deleting (for weekly review)

### Smart Reminders & Notifications (ADHD-Optimized)

**FR18:** System sends escalating notifications as task deadlines approach (gentle → persistent)  
**FR19:** System sends location-aware reminders when user is near relevant location  
**FR20:** System sends context-aware reminders (work tasks during work hours, personal tasks during personal time)  
**FR21:** Users can configure notification escalation preferences per task  
**FR22:** System surfaces urgent tasks in persistent notification (always visible)  
**FR23:** System sends daily digest notification showing today's obligations  
**FR24:** System sends weekly planning notification (Sunday evening)  
**FR25:** Users can snooze notifications with smart reschedule options (not infinite)

### Ambient Dashboard (Zero-Search Interface)

**FR26:** Users can view "Now" dashboard showing tasks/events needing immediate attention  
**FR27:** Users can view "Today" dashboard showing full day timeline with time blocks  
**FR28:** Users can view "This Week" dashboard showing upcoming 7-day obligations  
**FR29:** System visually distinguishes overdue tasks from upcoming tasks  
**FR30:** System shows task context tags with color-coding for quick scanning  
**FR31:** System displays time until next event/deadline prominently  
**FR32:** Users can quickly mark tasks complete directly from dashboard views  
**FR33:** System updates dashboard in real-time as tasks complete or deadlines change

### Life-Systems Journaling

**FR34:** System prompts users for daily journal entry at configured time (default: evening)  
**FR35:** Users can rate Relationships on 1-10 scale with optional notes  
**FR36:** Users can rate Work productivity/engagement on 1-10 scale with optional notes  
**FR37:** Users can rate Energy level on 1-10 scale with optional notes  
**FR38:** Users can rate Mood on 1-10 scale with optional notes  
**FR39:** Users can add freeform self-awareness reflection notes  
**FR40:** System reminds users to complete journal if skipped (gentle, not guilt-inducing)  
**FR41:** Users can view journal entry history in calendar format  
**FR42:** System generates weekly review showing trend lines (this week vs last week)  
**FR43:** System highlights significant changes in ratings (e.g., "Relationship 8→6 over 3 days")  
**FR44:** Users can add context notes during weekly review ("what changed?")  
**FR45:** System stores journal entries with end-to-end encryption

### Data Management & Sync

**FR46:** System stores all data locally on device (offline-first)  
**FR47:** System syncs data across user's devices when online  
**FR48:** Users can export all data (tasks, captures, journal entries) in standard formats  
**FR49:** Users can import previously exported data  
**FR50:** System resolves sync conflicts automatically with last-write-wins  
**FR51:** System provides sync status indicator (synced, syncing, offline)  
**FR52:** Users can manually trigger sync  
**FR53:** System backs up data automatically to user's cloud storage (opt-in)

### Account & Settings

**FR54:** Users can create accounts with email authentication  
**FR55:** Users can configure notification preferences (frequency, escalation, quiet hours)  
**FR56:** Users can configure journal prompt timing and template  
**FR57:** Users can configure context tags and colors  
**FR58:** Users can set work hours for context-aware reminders  
**FR59:** Users can enable/disable location-aware reminders  
**FR60:** Users can configure app appearance (theme, font size)  
**FR61:** System securely stores authentication credentials

### Weekly Review

**FR62:** System generates weekly review every Sunday evening  
**FR63:** Weekly review shows tasks completed vs not completed  
**FR64:** Weekly review shows journal trend analysis  
**FR65:** Weekly review prompts reflection: "What didn't get done and why?"  
**FR66:** Users can archive or reschedule incomplete tasks during review  
**FR67:** System sends weekly review reminder notification

**Total FRs:** 67 capabilities covering capture, task/event management, smart reminders, ambient dashboard, journaling, data management, and weekly review.

**Completeness Check:**
✅ Every capability in MVP scope represented  
✅ Core mission (never miss tasks/events) thoroughly covered (FR9-FR33)  
✅ ADHD-specific features included (FR18-FR25 smart reminders, FR26-FR33 ambient dashboard)  
✅ Secondary mission (detect self-changes) covered (FR34-FR45 journaling)  
✅ Supporting infrastructure covered (FR1-FR8 capture, FR46-FR53 sync, FR54-FR61 settings)

---

## Non-Functional Requirements

### Performance

**NFR-P1:** App launches in <2 seconds on mid-range devices  
**NFR-P2:** Capture operations complete in <500ms (ADHD friction threshold)  
**NFR-P3:** Sync latency <1 second when online  
**NFR-P4:** Dashboard views render in <300ms  
**NFR-P5:** App maintains 60fps during normal use

**Rationale:** ADHD brains are friction-sensitive. Any lag = abandonment.

### Reliability

**NFR-R1:** Notification delivery: 99.9% reliability (critical for core mission)  
**NFR-R2:** Data sync: 99.5% success rate (conflicts auto-resolved)  
**NFR-R3:** Offline functionality: 100% of core features work without internet  
**NFR-R4:** Data loss: Zero tolerance (automatic local + cloud backups)

**Rationale:** Cannot miss reminders. That's the entire value proposition.

### Security & Privacy

**NFR-S1:** Journal entries encrypted at rest with user-controlled keys  
**NFR-S2:** Data transmission encrypted via TLS 1.3+  
**NFR-S3:** Authentication uses secure token-based sessions  
**NFR-S4:** No third-party analytics or tracking (privacy-first)  
**NFR-S5:** User can delete all data permanently (GDPR compliance)

**Rationale:** Journal contains intimate self-reflection. Privacy is non-negotiable.

### Accessibility

**NFR-A1:** Text scales to 200% without breaking layout (ADHD users often adjust)  
**NFR-A2:** Color contrast meets WCAG AA standards  
**NFR-A3:** All interactive elements have 44px minimum touch target (mobile)  
**NFR-A4:** Screen reader support for core workflows

**Rationale:** ADHD often co-occurs with other accessibility needs.

### Platform Support

**NFR-PL1:** Windows 10+ desktop support (primary development platform)  
**NFR-PL2:** Android 12+ mobile support (60% of ADHD users prefer Android)  
**NFR-PL3:** Responsive design adapts to phone, tablet, desktop screen sizes  
**NFR-PL4:** Widget support on Android home screen  
**NFR-PL5:** Global hotkey support on Windows desktop

**Rationale:** Falk uses Windows desktop + Android mobile. Others are Phase 2+.

---

## Mobile App Specific Requirements

### Android Platform Features

**Mobile-1:** Home screen widget for instant capture (3x1, 4x1 sizes)  
**Mobile-2:** Share intent integration (capture from any app via "Share")  
**Mobile-3:** Persistent notification for urgent tasks (dismissible but resurfaces)  
**Mobile-4:** Background location tracking for location-aware reminders (opt-in, battery-efficient)  
**Mobile-5:** Alarm-level notification for critical deadlines (bypasses Do Not Disturb)

**Mobile-6:** Quick actions from notification (complete task, snooze, open)  
**Mobile-7:** Offline mode indicator in status bar  
**Mobile-8:** Biometric unlock option (fingerprint, face)

### Windows Desktop Features

**Desktop-1:** Global hotkey capture (default: Ctrl+Shift+L, configurable)  
**Desktop-2:** System tray icon with quick actions menu  
**Desktop-3:** Toast notifications for reminders  
**Desktop-4:** Always-on-top mini-dashboard mode (optional, non-intrusive)  
**Desktop-5:** Taskbar badge showing count of urgent items

---

## Integration Requirements

### Calendar Integration (Read-Only)

**INT-1:** Import events from Google Calendar via OAuth (read-only)  
**INT-2:** Import events from Outlook Calendar via OAuth (read-only)  
**INT-3:** Display imported calendar events in unified timeline view  
**INT-4:** Refresh calendar events automatically (hourly when online)  
**INT-5:** Users can configure which calendars to import

**Rationale:** Don't own the calendar—integrate to show unified view of obligations. Avoid OAuth complexity for Phase 0 if possible (manual import/export alternative).

### Export Capabilities

**INT-6:** Export tasks to CSV format  
**INT-7:** Export journal entries to Markdown format  
**INT-8:** Export all data to JSON backup format  
**INT-9:** Export timeline to iCal format (for backup)

**Rationale:** Data portability = trust. Users own their data.

---

## References

**Product Brief:** `docs/product-brief-bmad2-2025-11-15.md`  
**Market Research:** `docs/research-market-competitive-2025-11-15.md`  
**Brainstorming Session:** `docs/bmm-brainstorming-session-2025-11-15.md`

---

## Next Steps

1. **Epic & Story Breakdown** - Run: `workflow create-epics-and-stories` to decompose FRs into implementable chunks  
2. **Architecture Design** - Run: `workflow create-architecture` for technical architecture decisions  
3. **UX Design** (Optional) - Run: `workflow ux-design` for detailed user flows and mockups

---

_This PRD captures Life.D's mission: **never miss tasks/events again** + detect invisible self-changes BEFORE external feedback._

_Built for Falk's ADHD brain. Personal tool first. Maybe shared later if it works._

