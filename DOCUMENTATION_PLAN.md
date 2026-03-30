# LearningoPK Documentation Plan

> **Status**: Draft
> **Author**: Product Manager (Alex)
> **Last Updated**: 2026-03-30
> **Documentation Framework**: Mintlify (MDX + YAML frontmatter)
> **Source Project**: `learningopk/learningopk/`
> **Docs Output**: `docs/`

---

## 1. Executive Summary

This plan covers documentation for LearningoPK — a full-stack EdTech platform for Pakistani 9th/10th grade students. The project has **28 database tables**, **50+ API endpoints** across 15 route files, **100+ frontend components** across 12 component domains, **24 E2E test specs**, and Docker infrastructure.

Documentation will be created in 6 phases, ordered by what a developer needs first (overview) to what they need last (advanced features). Each phase builds on the previous.

---

## 2. Phase Plan

### Phase 1: Foundation (Priority: Critical)
**Goal**: Any developer can understand the project and run it locally in under 15 minutes.

| File | Status | Key Content | Dependencies |
|------|--------|-------------|-------------|
| `index.mdx` | EXISTS (needs rewrite) | Project overview, what it does, target users (Pakistani 9th/10th graders), core value proposition, feature highlights | None |
| `quickstart.mdx` | EXISTS (needs rewrite) | Prerequisites, clone, env setup, Docker up, seed DB, start dev, verify health endpoint | None |
| `architecture/system-overview.mdx` | EXISTS (needs rewrite) | High-level architecture diagram, request flow (Next.js SSR -> Express API -> PostgreSQL), role of each service | None |
| `architecture/tech-stack.mdx` | EXISTS (needs rewrite) | Tech choices table: Next.js 16, Express, Drizzle ORM, Better Auth, BullMQ, Mistral AI, shadcn/ui, Playwright | None |
| `architecture/database.mdx` | EXISTS (needs rewrite) | 28 tables: core schema, relationships, enums. Reference from `backend/src/lib/db/schema.ts` | None |

**Estimated scope**: 5 files to create/rewrite. ~2,500 words total.

---

### Phase 2: Backend API Documentation (Priority: Critical)
**Goal**: Every API endpoint is documented with method, path, auth requirements, request/response schemas, and error codes.

| File | Status | Key Content | Dependencies |
|------|--------|-------------|-------------|
| `api/auth.mdx` | EXISTS (needs rewrite) | Better Auth endpoints (signup, login, logout, session, forgot-password, reset-password) | Phase 1 |
| `api/learn.mdx` | EXISTS (needs rewrite) | Subject/chapter/exercise/flashcard CRUD, curriculum tree, chapter graph | Phase 1 |
| `api/quiz.mdx` | EXISTS (needs rewrite) | Quiz submission, scoring, quiz questions | Phase 1 |
| `api/mock-exams.mdx` | EXISTS (needs rewrite) | Mock exam listing, filtering, attempt tracking, solutions | Phase 1 |
| `api/progress.mdx` | EXISTS (needs rewrite) | Progress events, dashboard data, subject dashboard | Phase 1 |
| `api/ai-chat.mdx` | EXISTS (needs rewrite) | Streaming chat, sessions, messages, rate limiting, context injection | Phase 1 |
| `api/forum.mdx` | EXISTS (needs rewrite) | Threads CRUD, replies, voting, acceptance, filters, rate limiting | Phase 1 |
| `api/admin.mdx` | EXISTS (needs rewrite) | Overview, analytics, users, moderation, notifications, settings, content CRUD | Phase 1 |
| `api/health.mdx` | NEEDS CREATION | Health check endpoint for Postgres + Redis | Phase 1 |
| `api/profile.mdx` | NEEDS CREATION | Profile image upload (MinIO) | Phase 1 |
| `api/boards.mdx` | NEEDS CREATION | Board listing endpoint | Phase 1 |
| `api/classes.mdx` | NEEDS CREATION | Class listing endpoint | Phase 1 |
| `api/subjects.mdx` | NEEDS CREATION | Subject listing endpoint | Phase 1 |
| `api/institutes.mdx` | NEEDS CREATION | Institute listing endpoint | Phase 1 |
| `api/chapter-media.mdx` | NEEDS CREATION | Chapter summary media upload (MinIO) | Phase 1 |

**Estimated scope**: 15 files. ~8,000 words total.

---

### Phase 3: Frontend Documentation (Priority: High)
**Goal**: Developers understand the component architecture, routing, and how UI connects to APIs.

| File | Status | Key Content | Dependencies |
|------|--------|-------------|-------------|
| `frontend/overview.mdx` | EXISTS (needs rewrite) | App Router structure, route groups (`(learn)`, `(dashboard)`), layout hierarchy, component domains | Phase 1 |
| `frontend/dashboard.mdx` | EXISTS (needs rewrite) | Dashboard components (StatsCards, SubjectProgress, Streak, Heatmap, ActivityFeed), stats charts | Phase 2 |
| `frontend/learn.mdx` | EXISTS (needs rewrite) | Learn components (QuizRunner, FlashcardDeck, AI Chat Panel, ChapterWorkspace, ExerciseAccordion) | Phase 2 |
| `frontend/admin.mdx` | EXISTS (needs rewrite) | Admin panel (Command Center, Content CRUD, Forum Moderation, Analytics, Audit, Users, Settings) | Phase 2 |
| `frontend/auth.mdx` | NEEDS CREATION | Auth flow (Login, Register, Forgot Password), auth guards, session handling | Phase 2 |
| `frontend/forum.mdx` | NEEDS CREATION | Forum page (ThreadFeed, ThreadDetail, ThreadForm, ReplyList, ReplyForm, FilterBar) | Phase 2 |
| `frontend/mock-exams.mdx` | NEEDS CREATION | Past papers archive, exam mode UI, result details | Phase 2 |
| `frontend/stats.mdx` | NEEDS CREATION | Stats page (SubjectPerformance, QuizAccuracy, WeeklyGoals, ConsistencyCalendar, StudyVolume) | Phase 2 |
| `frontend/design-system.mdx` | NEEDS CREATION | shadcn/ui components (Button, Card, Badge, Input, Select), CVA patterns, Tailwind conventions | Phase 2 |

**Estimated scope**: 9 files. ~5,000 words total.

---

### Phase 4: Infrastructure & DevOps (Priority: High)
**Goal**: Developers can set up the full stack, understand Docker, caching, load balancing, and deployment.

| File | Status | Key Content | Dependencies |
|------|--------|-------------|-------------|
| `infra/docker.mdx` | EXISTS (needs rewrite) | Docker Compose services (Postgres 16, Redis 7, MinIO, PgBouncer, Nginx), port mapping, volumes | Phase 1 |
| `infra/environment.mdx` | EXISTS (needs rewrite) | All env vars: DATABASE_URL, REDIS_URL, BETTER_AUTH_*, MISTRAL_API_KEY, MINIO_*, FRONTEND_ORIGIN | Phase 1 |
| `infra/deployment.mdx` | EXISTS (needs rewrite) | Production deployment steps, nginx config, PgBouncer transaction-mode pooling, health checks | Phase 1 |
| `infra/caching.mdx` | NEEDS CREATION | Redis cache layer (typed keys, TTLs: subjects 1hr, chapters 30min, forum 5min), cache-through repository pattern | Phase 1 |
| `infra/load-balancing.mdx` | NEEDS CREATION | Nginx upstream config, rate limiting (100r/m user, 1000r/m IP), JWT pass-through, gzip | Phase 1 |
| `infra/background-jobs.mdx` | NEEDS CREATION | BullMQ setup, worker processes, job registry, dead-letter queue, retry policies | Phase 1 |

**Estimated scope**: 6 files. ~3,500 words total.

---

### Phase 5: Development Guides (Priority: High)
**Goal**: New contributors can write code, run tests, and submit PRs following project conventions.

| File | Status | Key Content | Dependencies |
|------|--------|-------------|-------------|
| `dev/setup.mdx` | EXISTS (needs rewrite) | Full dev setup: pnpm, Docker, env vars, seed, verify health, run E2E | Phase 1 |
| `dev/testing.mdx` | EXISTS (needs rewrite) | Unit tests (Vitest), integration tests (supertest), E2E (Playwright), test commands, writing guidelines | Phase 1 |
| `dev/contributing.mdx` | EXISTS (needs rewrite) | Branch naming, commit format (TASK-XX:), PR process, code review, AGENTS.md conventions | Phase 1 |
| `dev/code-style.mdx` | NEEDS CREATION | TypeScript strict, no `any`, ESM imports, naming conventions (routes kebab-case, tables snake_case, Zod CamelCase+Schema) | Phase 1 |
| `dev/database-guide.mdx` | NEEDS CREATION | Drizzle ORM patterns, migration workflow (generate + migrate), seeding, repository pattern | Phase 1 |
| `dev/e2e-testing.mdx` | NEEDS CREATION | Playwright setup, 24 E2E specs overview, writing new tests, debugging, CI integration | Phase 1 |

**Estimated scope**: 6 files. ~3,000 words total.

---

### Phase 6: Advanced Features (Priority: Medium)
**Goal**: Understand the gamification, AI, and engagement systems that differentiate the product.

| File | Status | Key Content | Dependencies |
|------|--------|-------------|-------------|
| `ai-tools/xp-system.mdx` | NEEDS CREATION | XP awards (+5 chapter, +2 exercise, +10 flashcard, +25 quiz, +15 forum), 5-level system (Fresher→Board Topper), streak freeze | Phase 2 |
| `ai-tools/ai-tutor.mdx` | NEEDS CREATION | Mistral AI integration, Socratic method, streaming, rate limiting, context injection, usage logging | Phase 2 |
| `ai-tools/gamification.mdx` | NEEDS CREATION | Shareable result cards, study streaks, toast notifications, leaderboard (future), quiz duels (future) | Phase 2 |
| `essentials/markdown.mdx` | NEEDS CREATION | Markdown/Math rendering in chapter summaries (KaTeX), wiki links between chapters, accessibility | Phase 2 |

**Estimated scope**: 4 files. ~2,000 words total.

---

## 3. API Endpoint Inventory

### 3.1 Auth Routes (`/api/auth/*`)
Better Auth managed — exposes standard endpoints:
| Method | Path | Auth | Description |
|--------|------|------|-------------|
| POST | `/api/auth/sign-up/email` | None | Register with email/password |
| POST | `/api/auth/sign-in/email` | None | Login with email/password |
| POST | `/api/auth/sign-out` | Session | Logout, destroy session |
| GET | `/api/auth/get-session` | Cookie | Get current session info |
| POST | `/api/auth/forget-password` | None | Request password reset email |
| POST | `/api/auth/reset-password` | Token | Reset password with token |

### 3.2 Health Routes (`/api/health`)
| Method | Path | Auth | Description |
|--------|------|------|-------------|
| GET | `/api/health` | None | Check Postgres + Redis connectivity |

### 3.3 Boards Routes (`/api/boards`)
| Method | Path | Auth | Description |
|--------|------|------|-------------|
| GET | `/api/boards` | None | List all boards (id, name, slug) |

### 3.4 Classes Routes (`/api/classes`)
| Method | Path | Auth | Description |
|--------|------|------|-------------|
| GET | `/api/classes` | None | List all board classes (id, boardId, name, slug) |

### 3.5 Subjects Routes (`/api/subjects`)
| Method | Path | Auth | Description |
|--------|------|------|-------------|
| GET | `/api/subjects` | None | List all subjects with progress info |

### 3.6 Institutes Routes (`/api/institutes`)
| Method | Path | Auth | Description |
|--------|------|------|-------------|
| GET | `/api/institutes` | None | List all institutes |

### 3.7 Learn Routes (`/api/learn`)
| Method | Path | Auth | Description |
|--------|------|------|-------------|
| GET | `/api/learn/:board/:grade/:subject` | None | Get subject details + chapters list |
| GET | `/api/learn/:board/:grade/:subject/graph` | Session | Get subject chapter graph (student-scoped) |
| GET | `/api/learn/:board/:grade/:subject/:chapter` | None | Get chapter with exercises, flashcards, quiz |

### 3.8 Quiz Routes (`/api/quiz`)
| Method | Path | Auth | Description |
|--------|------|------|-------------|
| POST | `/api/quiz/submit` | Session | Submit quiz answers, get scored result |

### 3.9 Mock Exams Routes (`/api/mock-exams`)
| Method | Path | Auth | Description |
|--------|------|------|-------------|
| GET | `/api/mock-exams` | None | List mock exams with filters (boardId, grade, subjectId, year) |
| GET | `/api/mock-exams/filters/options` | None | Get filter options (distinct boards, grades, subjects, years) |
| GET | `/api/mock-exams/:id` | None | Get mock exam details with quiz info |
| GET | `/api/mock-exams/:id/attempts` | Session | Get user's attempts for a mock exam |
| GET | `/api/mock-exams/:id/questions` | Session | Get quiz questions with answers (requires completed attempt) |

### 3.10 Progress Routes (`/api/progress`)
| Method | Path | Auth | Description |
|--------|------|------|-------------|
| POST | `/api/progress/events` | Session | Record progress event (chapter_visit, exercise_view, flashcard_complete, quiz_submit) |
| GET | `/api/progress/dashboard` | Session | Get user dashboard data (subjects, streak, activity, XP) |
| GET | `/api/progress/dashboard/:boardSlug/:grade/:subjectSlug` | Session | Get subject-specific progress detail |

### 3.11 AI Chat Routes (`/api/ai`)
| Method | Path | Auth | Description |
|--------|------|------|-------------|
| GET | `/api/ai/sessions` | Session | List user's AI chat sessions |
| GET | `/api/ai/sessions/:sessionId/messages` | Session | Get messages for a session |
| POST | `/api/ai/chat` | Session | Send chat message, stream AI response (rate limited) |

### 3.12 Forum Routes (`/api/forum`)
| Method | Path | Auth | Description |
|--------|------|------|-------------|
| GET | `/api/forum/filters` | None | Get forum filter metadata (boards, classes, subjects, chapters) |
| GET | `/api/forum/threads` | None | List threads with filters (board, grade, subjectId, chapterId, q, solved) |
| GET | `/api/forum/threads/:threadId` | Optional | Get thread detail with replies + viewer votes |
| POST | `/api/forum/threads` | Session | Create a new thread (rate limited) |
| POST | `/api/forum/threads/:threadId/replies` | Session | Reply to a thread (rate limited, supports nested replies) |
| POST | `/api/forum/replies/:replyId/vote` | Session | Vote on a reply (upvote/downvote, rate limited) |
| POST | `/api/forum/replies/:replyId/accept` | Session | Accept a reply as answer (rate limited) |

### 3.13 Profile Routes (`/api/profile`)
| Method | Path | Auth | Description |
|--------|------|------|-------------|
| PUT | `/api/profile/me/profile-image` | Session | Upload profile image (Max 2MB, stores in MinIO) |

### 3.14 Chapter Media Routes (`/api/chapter-media`)
| Method | Path | Auth | Description |
|--------|------|------|-------------|
| POST | `/api/chapter-media/chapters/:chapterId/summary-media` | Admin | Upload chapter summary image (Max 10MB, stores in MinIO) |

### 3.15 Admin Routes (`/api/admin`) — All require admin role
| Method | Path | Description |
|--------|------|-------------|
| GET | `/api/admin/overview` | Admin dashboard KPIs + alerts |
| GET | `/api/admin/analytics/overview` | Active students, quiz stats, subject performance |
| GET | `/api/admin/content/curriculum` | Full curriculum tree (boards -> classes -> subjects -> chapters) |
| POST | `/api/admin/content/boards` | Create board |
| POST | `/api/admin/content/boards/:id/update` | Update board |
| POST | `/api/admin/content/boards/:id/delete` | Delete board |
| POST | `/api/admin/content/classes` | Create class |
| POST | `/api/admin/content/classes/:id/update` | Update class |
| POST | `/api/admin/content/classes/:id/delete` | Delete class |
| POST | `/api/admin/content/subjects` | Create subject |
| POST | `/api/admin/content/chapters` | Create chapter |
| POST | `/api/admin/content/chapters/:id/update` | Update chapter |
| POST | `/api/admin/content/chapters/:id/delete` | Delete chapter |
| POST | `/api/admin/content/chapters/:id/rename` | Rename chapter (title + slug) |
| POST | `/api/admin/content/chapters/:id/publish` | Publish/unpublish chapter |
| POST | `/api/admin/content/chapters/:id/summary` | Update chapter summary |
| GET | `/api/admin/content/chapters/:id/summary` | Get chapter summary |
| GET | `/api/admin/content/chapters/:id/links` | Get chapter wiki-links (outgoing + backlinks) |
| GET | `/api/admin/content/chapters` | List all chapters with metadata |
| GET | `/api/admin/content/chapters/graph` | Chapter link graph (nodes + edges) |
| GET | `/api/admin/content/chapters/link-suggestions` | Search chapters for link suggestions |
| POST | `/api/admin/content/exercises` | Create exercise |
| POST | `/api/admin/content/exercises/:id/update` | Update exercise |
| POST | `/api/admin/content/exercises/:id/delete` | Delete exercise |
| GET | `/api/admin/content/exercises` | List exercises (optional chapterId filter) |
| GET | `/api/admin/users` | List users (paginated, filterable by role/status/search) |
| POST | `/api/admin/users/:id/role` | Update user role |
| POST | `/api/admin/users/:id/suspension` | Suspend/reactivate user |
| GET | `/api/admin/community/threads` | List forum threads for moderation |
| POST | `/api/admin/forum/threads/:threadId/pin` | Pin/unpin forum thread |
| GET | `/api/admin/moderation/flags` | List moderation flags |
| POST | `/api/admin/moderation/flags/:id/resolve` | Resolve moderation flag |
| GET | `/api/admin/notifications` | List admin notifications |
| POST | `/api/admin/notifications` | Create/send notification broadcast |
| GET | `/api/admin/settings` | List admin settings |
| POST | `/api/admin/settings/:key` | Update admin setting |
| GET | `/api/admin/audit/content` | List content audit logs |
| GET | `/api/admin/audit/forum` | List forum audit logs |
| GET | `/api/admin/audit/moderation` | List moderation audit logs |
| GET | `/api/admin/audit/notifications` | List notifications audit logs |
| GET | `/api/admin/audit/settings` | List settings audit logs |
| GET | `/api/admin/audit/users` | List users audit logs |
| GET | `/api/admin/audit` | Aggregated audit log (filterable) |

**Total unique API endpoints: 62**

---

## 4. Frontend Component Inventory

### 4.1 UI Primitives (`components/ui/`) — 7 components
`badge.tsx`, `button.tsx`, `card.tsx`, `checkbox.tsx`, `confirm-dialog.tsx`, `input.tsx`, `select.tsx`

### 4.2 Auth Components (`components/auth/`) — 8 components
`auth-guard-message.tsx`, `auth-layout.tsx`, `bento-auth-field.tsx`, `form-field.tsx`, `hero-illustration.tsx`, `login-form.tsx`, `logout-button.tsx`, `password-input.tsx`, `register-form.tsx`

### 4.3 Learn Components (`components/learn/`) — 22 components
`ai-chat-panel.tsx`, `ask-ai-button.tsx`, `chapter-card.tsx`, `chapter-exercises-with-ai.tsx`, `chapter-progress-tracker.tsx`, `chapter-study-content-with-ai.tsx`, `chapter-study-workspace.tsx`, `exercise-accordion.tsx`, `exercise-item.tsx`, `exercise-solution-panel.tsx`, `flashcard-card.tsx`, `flashcard-deck.tsx`, `markdown-content.tsx`, `markdown-math-renderer.tsx`, `mock-exam-result-details.tsx`, `question-navigator.tsx`, `quest-exercises-view.tsx`, `quest-flashcard-view.tsx`, `quest-header.tsx`, `quest-quiz-view.tsx`, `quest-summary-view.tsx`, `quest-tab-bar.tsx`, `quiz-question-card.tsx`, `quiz-question-review-list.tsx`, `quiz-result-summary.tsx`, `quiz-runner.tsx`, `quiz-timer.tsx`, `shareable-result-card.tsx`, `subject-header.tsx`, `subject-view-switcher.tsx`

### 4.4 Dashboard Components (`components/dashboard/`) — 11 components
`DashboardClient.tsx`, `StatsCards.tsx`, `dashboard-chrome-layout.tsx`, `dashboard-notifications-control.tsx`, `dashboard-settings-panel.tsx`, `recent-activity-feed.tsx`, `streak-card.tsx`, `subject-progress-card.tsx`, `subject-progress-table.tsx`, `weekly-activity-heatmap.tsx`, `welcome-card.tsx`

### 4.5 Stats Components (`components/stats/`) — 10 components
`daily-streak-heatmap.tsx`, `quiz-accuracy-trend.tsx`, `stats-consistency-calendar.tsx`, `stats-focus-areas.tsx`, `stats-goals.tsx`, `stats-hero-kpi-strip.tsx`, `stats-quiz-performance-chart.tsx`, `stats-study-volume-chart.tsx`, `stats-subject-performance-grid.tsx`, `stats-weekly-goals.tsx`, `subject-progress-overview.tsx`, `weekly-trend.tsx`

### 4.6 Forum Components (`components/forum/`) — 9 components
`forum-filter-bar.tsx`, `forum-reply-actions.tsx`, `forum-reply-form.tsx`, `forum-reply-list.tsx`, `forum-thread-card.tsx`, `forum-thread-feed.tsx`, `forum-thread-form.tsx`, `forum-thread-header.tsx`, `forum-thread-list.tsx`

### 4.7 Admin Components (`components/admin/`) — 14 components
`action-button.tsx`, `admin-analytics-panel.tsx`, `admin-analytics-subject-table.tsx`, `admin-audit-log-list.tsx`, `admin-audit-panel.tsx`, `admin-audit-table.tsx`, `admin-command-center-panel.tsx`, `admin-community-panel.tsx`, `admin-content-panel.tsx`, `admin-curriculum-builder.tsx`, `admin-forum-panel.tsx`, `admin-guard.tsx`, `admin-moderation-panel.tsx`, `admin-users-table.tsx`

### 4.8 Foundation Components (`components/foundation/`) — 4 components
`app-shell.tsx`, `auth-layout-wrapper.tsx`, `dashboard-primitives.tsx`, `left-rail.tsx`

### 4.9 Other Components
- `components/ai/ai-tutor-chat.tsx` — AI tutor chat interface
- `components/graph/chapter-link-graph.tsx` — Chapter link visualization
- `components/layout/page-container.tsx` — Page layout wrapper
- `components/navigation/breadcrumbs.tsx` — Breadcrumb navigation

**Total frontend components: 86+**

---

## 5. E2E Test Specs Inventory (24 specs)

| Spec File | Domain | What It Covers |
|-----------|--------|----------------|
| `smoke.spec.ts` | Core | Basic smoke test for critical flows |
| `phase1-forum-dashboard-chrome.spec.ts` | Forum + Dashboard | Forum feed + dashboard chrome layout |
| `phase2-auth-dashboard.spec.ts` | Auth + Dashboard | Auth flow + dashboard rendering |
| `phase3-auth-layout-routes.spec.ts` | Auth | Auth layout + route protection |
| `auth-resilience.spec.ts` | Auth | Auth service outage behavior |
| `admin-left-rail.spec.ts` | Admin | Admin left rail navigation |
| `admin-phase1-shell.spec.ts` | Admin | Admin shell initialization |
| `admin-phase2-moderation-users.spec.ts` | Admin | Moderation + user management |
| `admin-phase3-community-analytics.spec.ts` | Admin | Community + analytics panels |
| `admin-phase4-notifications-settings.spec.ts` | Admin | Notifications + settings |
| `admin-phase5-users-lifecycle.spec.ts` | Admin | User lifecycle (suspend/reactivate) |
| `admin-phase6-audit-center.spec.ts` | Admin | Audit log center |
| `admin-phase7-command-center.spec.ts` | Admin | Command center dashboard |
| `admin-phase8-curriculum-builder.spec.ts` | Admin | Curriculum CRUD builder |
| `admin-summary-editor-codemirror.spec.ts` | Admin | Summary editor (CodeMirror) |
| `admin-summary-editor-performance.spec.ts` | Admin | Summary editor performance |
| `admin-summary-graph.spec.ts` | Admin | Chapter link graph visualization |
| `admin-summary-wikilinks.spec.ts` | Admin | Wiki-links resolution |
| `stats-screen.spec.ts` | Stats | Stats page rendering |
| `student-subject-graph.spec.ts` | Learn | Student subject graph |
| `student-subject-graph-performance.spec.ts` | Learn | Subject graph performance |
| `student-subject-page-baseline-performance.spec.ts` | Learn | Subject page baseline perf |
| `theme-light.spec.ts` | UI | Light theme rendering |
| `ui-quality.spec.ts` | UI | UI quality audit |

---

## 6. Database Tables Inventory (28 tables)

| Table | Domain | Description |
|-------|--------|-------------|
| `user` | Auth | User accounts (id, name, email, role, xp, level, streak, status) |
| `session` | Auth | Active sessions (Better Auth managed) |
| `account` | Auth | Auth accounts (Better Auth managed) |
| `verification` | Auth | Email verification tokens |
| `boards` | Curriculum | Education boards (Federal, Punjab, Sindh) |
| `board_classes` | Curriculum | Grade classes per board |
| `subjects` | Curriculum | Subjects per board/class |
| `chapters` | Curriculum | Chapters per subject (title, slug, summary, isPublished) |
| `exercises` | Content | Exercise questions + solutions per chapter |
| `flashcards` | Content | Flashcard decks per chapter |
| `quizzes` | Assessment | Quizzes (chapter_quiz, mock_exam) |
| `quiz_questions` | Assessment | MCQ questions per quiz |
| `quiz_attempts` | Assessment | User quiz submissions + scores |
| `user_progress` | Tracking | Progress events (visit, exercise, flashcard, quiz) |
| `ai_chat_sessions` | AI | Chat session metadata |
| `ai_messages` | AI | Individual messages (user/assistant) |
| `ai_usage_logs` | AI | Token usage tracking |
| `forum_threads` | Community | Forum discussion threads |
| `forum_replies` | Community | Replies to threads (supports nesting) |
| `forum_votes` | Community | Upvote/downvote on replies |
| `mock_exams` | Assessment | Past paper exams linked to quizzes |
| `chapter_title_aliases` | Content | Chapter title aliases for wiki-link resolution |
| `chapter_summary_links` | Content | Wiki-links between chapter summaries |
| `chapter_summary_media` | Content | Uploaded media for chapter summaries |
| `moderation_flags` | Admin | Content moderation flags |
| `admin_audit_logs` | Admin | Admin action audit trail |
| `admin_notifications` | Admin | Broadcast notifications |
| `admin_settings` | Admin | Platform configuration key-value |
| `institutes` | Content | Educational institutes |

---

## 7. CHANGELOG / UPDATE Tracking Mechanism

See `AGENTS.md` in this docs directory for the full tracking system. Summary:

1. **Source-of-truth file**: `AGENTS.md` tracks every documented item (file, API endpoint, component, table) with a status hash
2. **Diff workflow**: When code is pulled from GitHub, an agent reads `AGENTS.md`, compares tracked hashes against current source, and identifies NEW/CHANGED/DELETED items
3. **Granular tracking**: Per-endpoint, per-component, per-table granularity — not per-file
4. **Update triggers**: Any change to `backend/src/routes/*.ts`, `frontend/src/components/**/*.tsx`, `backend/src/lib/db/schema.ts`, or `frontend/tests/e2e/*.spec.ts` triggers documentation review

---

## 8. docs.json Navigation Updates Required

After all phases complete, `docs.json` needs these additions:

```json
{
  "tab": "Backend API",
  "groups": [
    // Add these new pages:
    "api/health",
    "api/profile",
    "api/boards",
    "api/classes",
    "api/subjects",
    "api/institutes",
    "api/chapter-media"
  ]
},
{
  "tab": "Frontend",
  "groups": [
    // Add these new pages:
    "frontend/auth",
    "frontend/forum",
    "frontend/mock-exams",
    "frontend/stats",
    "frontend/design-system"
  ]
},
{
  "tab": "Infrastructure",
  "groups": [
    // Add these new pages:
    "infra/caching",
    "infra/load-balancing",
    "infra/background-jobs"
  ]
},
{
  "tab": "Development",
  "groups": [
    // Add these new pages:
    "dev/code-style",
    "dev/database-guide",
    "dev/e2e-testing"
  ]
}
```

---

## 9. Execution Order & Timeline

| Week | Phase | Deliverables | Owner |
|------|-------|-------------|-------|
| 1 | Phase 1: Foundation | 5 files (index, quickstart, 3 architecture) | Docs Agent |
| 2-3 | Phase 2: API Docs | 15 files (all API endpoints) | Docs Agent |
| 4 | Phase 3: Frontend | 9 files (all frontend docs) | Docs Agent |
| 5 | Phase 4: Infra | 6 files (Docker, env, deployment, caching, nginx, jobs) | Docs Agent |
| 5-6 | Phase 5: Dev Guides | 6 files (setup, testing, contributing, code-style, DB, E2E) | Docs Agent |
| 6 | Phase 6: Advanced | 4 files (XP, AI tutor, gamification, markdown) | Docs Agent |

**Total**: 45 documentation files, ~24,000 words, ~6 weeks

---

## 10. Risks & Mitigations

| Risk | Impact | Mitigation |
|------|--------|------------|
| Source code changes during documentation | Docs become stale | AGENTS.md tracking mechanism catches diffs |
| API contract drift | Wrong endpoint docs | Reference `api-contracts.md` + actual route files |
| Component renaming | Broken frontend docs | AGENTS.md tracks component file hashes |
| Mintlify format errors | Docs don't render | Run `mint broken-links` after each phase |
| Scope creep from "nice to have" pages | Timeline slips | Phase 6 items are explicitly deprioritized |
