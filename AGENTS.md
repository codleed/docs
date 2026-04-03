# AGENTS.md — LearningoPK Documentation Tracker

> **Purpose**: This file is the source-of-truth for what has been documented in the LearningoPK docs site. When code is pulled from GitHub, an agent diffs this file against the actual source code to determine what needs NEW, UPDATED, or DELETED documentation.

---

## How This Works

### For the Documentation Agent

1. **Before writing any docs**: Read this file to find undocumented items (status = `pending`)
2. **After writing docs**: Update the item's status to `documented` and record the content hash
3. **After code updates**: Run the diff workflow (see below) to detect changes

### Diff Workflow

```bash
# 1. Read current source files and compute hashes
# 2. Compare against TRACKED_* sections below
# 3. Generate a diff report of: NEW | CHANGED | DELETED items
# 4. Update documentation for changed/new items
# 5. Update hashes in this file
```

### Hash Format

Each tracked item uses a simple hash of its content for change detection:
- **API endpoints**: Hash of the route handler function signature + Zod schema
- **Components**: Hash of the component's exported interface (props, key logic)
- **Database tables**: Hash of the Drizzle `pgTable()` definition
- **E2E tests**: Hash of the test file's describe/it blocks

Hash format: `{md5_short_12chars}` — e.g., `a1b2c3d4e5f6`

When a hash doesn't match, the agent knows that item needs documentation review.

---

## TRACKED_API_ENDPOINTS

### Auth (`/api/auth/*`) — Better Auth managed
| Endpoint | Doc File | Status | Hash | Notes |
|----------|----------|--------|------|-------|
| POST /api/auth/sign-up/email | api/auth.mdx | `documented` | — | |
| POST /api/auth/sign-in/email | api/auth.mdx | `documented` | — | |
| POST /api/auth/sign-out | api/auth.mdx | `documented` | — | |
| GET /api/auth/get-session | api/auth.mdx | `documented` | — | |
| POST /api/auth/forget-password | api/auth.mdx | `documented` | — | Partially implemented per TASK-56 |
| POST /api/auth/reset-password | api/auth.mdx | `documented` | — | Partially implemented per TASK-56 |

### Health (`/api/health`)
| Endpoint | Doc File | Status | Hash | Notes |
|----------|----------|--------|------|-------|
| GET /api/health | api/health.mdx | `documented` | — | |

### Boards (`/api/boards`) — Not mounted in server.ts
| Endpoint | Doc File | Status | Hash | Notes |
|----------|----------|--------|------|-------|
| GET /api/boards | api/boards.mdx | `documented` | — | Router exists but not mounted |

### Classes (`/api/classes`) — Not mounted in server.ts
| Endpoint | Doc File | Status | Hash | Notes |
|----------|----------|--------|------|-------|
| GET /api/classes | api/classes.mdx | `documented` | — | Router exists but not mounted |

### Subjects (`/api/subjects`) — Not mounted in server.ts
| Endpoint | Doc File | Status | Hash | Notes |
|----------|----------|--------|------|-------|
| GET /api/subjects | api/subjects.mdx | `documented` | — | Router exists but not mounted |

### Institutes (`/api/institutes`) — Not mounted in server.ts
| Endpoint | Doc File | Status | Hash | Notes |
|----------|----------|--------|------|-------|
| GET /api/institutes | api/institutes.mdx | `documented` | — | Router exists but not mounted |

### Learn (`/api/learn`)
| Endpoint | Doc File | Status | Hash | Notes |
|----------|----------|--------|------|-------|
| GET /api/learn/:board/:grade/:subject | api/learn.mdx | `documented` | — | |
| GET /api/learn/:board/:grade/:subject/graph | api/learn.mdx | `documented` | — | Requires session |
| GET /api/learn/:board/:grade/:subject/:chapter | api/learn.mdx | `documented` | — | |

### Quiz (`/api/quiz`)
| Endpoint | Doc File | Status | Hash | Notes |
|----------|----------|--------|------|-------|
| POST /api/quiz/submit | api/quiz.mdx | `documented` | — | |

### Mock Exams (`/api/mock-exams`)
| Endpoint | Doc File | Status | Hash | Notes |
|----------|----------|--------|------|-------|
| GET /api/mock-exams | api/mock-exams.mdx | `documented` | — | |
| GET /api/mock-exams/filters/options | api/mock-exams.mdx | `documented` | — | |
| GET /api/mock-exams/:id | api/mock-exams.mdx | `documented` | — | |
| GET /api/mock-exams/:id/attempts | api/mock-exams.mdx | `documented` | — | |
| GET /api/mock-exams/:id/questions | api/mock-exams.mdx | `documented` | — | Requires completed attempt |

### Progress (`/api/progress`)
| Endpoint | Doc File | Status | Hash | Notes |
|----------|----------|--------|------|-------|
| POST /api/progress/events | api/progress.mdx | `documented` | — | 4 event types |
| GET /api/progress/dashboard | api/progress.mdx | `documented` | — | |
| GET /api/progress/dashboard/:boardSlug/:grade/:subjectSlug | api/progress.mdx | `documented` | — | |

### AI Chat (`/api/ai`)
| Endpoint | Doc File | Status | Hash | Notes |
|----------|----------|--------|------|-------|
| GET /api/ai/sessions | api/ai-chat.mdx | `documented` | — | |
| GET /api/ai/sessions/:sessionId/messages | api/ai-chat.mdx | `documented` | — | |
| POST /api/ai/chat | api/ai-chat.mdx | `documented` | — | Streaming, rate limited |

### Forum (`/api/forum`)
| Endpoint | Doc File | Status | Hash | Notes |
|----------|----------|--------|------|-------|
| GET /api/forum/filters | api/forum.mdx | `documented` | — | |
| GET /api/forum/threads | api/forum.mdx | `documented` | — | |
| GET /api/forum/threads/:threadId | api/forum.mdx | `documented` | — | Optional auth |
| POST /api/forum/threads | api/forum.mdx | `documented` | — | Rate limited |
| POST /api/forum/threads/:threadId/replies | api/forum.mdx | `documented` | — | Rate limited |
| POST /api/forum/replies/:replyId/vote | api/forum.mdx | `documented` | — | Rate limited |
| POST /api/forum/replies/:replyId/accept | api/forum.mdx | `documented` | — | Rate limited |

### Profile (`/api/users`)
| Endpoint | Doc File | Status | Hash | Notes |
|----------|----------|--------|------|-------|
| PUT /api/users/me/profile-image | api/profile.mdx | `documented` | — | MinIO, max 2MB |

### Chapter Media (`/api/admin/content`)
| Endpoint | Doc File | Status | Hash | Notes |
|----------|----------|--------|------|-------|
| POST /api/admin/content/chapters/:chapterId/summary-media | api/chapter-media.mdx | `documented` | — | Admin only, MinIO, max 10MB |
| POST /api/admin/content/chapters/:chapterId/presigned-upload | api/chapter-media.mdx | `documented` | — | Get presigned PUT URL |
| POST /api/admin/content/chapters/:chapterId/media/confirm | api/chapter-media.mdx | `documented` | — | Confirm presigned upload |
| GET /api/admin/content/chapters/:chapterId/media | api/chapter-media.mdx | `documented` | — | List media for chapter |
| DELETE /api/admin/content/chapters/:chapterId/media/:mediaId | api/chapter-media.mdx | `documented` | — | Delete media |

### Admin (`/api/admin`) — All require admin role
| Endpoint | Doc File | Status | Hash | Notes |
|----------|----------|--------|------|-------|
| GET /api/admin/overview | api/admin.mdx | `documented` | — | |
| GET /api/admin/analytics/overview | api/admin.mdx | `documented` | — | |
| GET /api/admin/content/curriculum | api/admin.mdx | `documented` | — | |
| POST /api/admin/content/boards | api/admin.mdx | `documented` | — | |
| POST /api/admin/content/boards/:id/update | api/admin.mdx | `documented` | — | |
| POST /api/admin/content/boards/:id/delete | api/admin.mdx | `documented` | — | |
| POST /api/admin/content/classes | api/admin.mdx | `documented` | — | |
| POST /api/admin/content/classes/:id/update | api/admin.mdx | `documented` | — | |
| POST /api/admin/content/classes/:id/delete | api/admin.mdx | `documented` | — | |
| POST /api/admin/content/subjects | api/admin.mdx | `documented` | — | |
| POST /api/admin/content/chapters | api/admin.mdx | `documented` | — | |
| POST /api/admin/content/chapters/:id/update | api/admin.mdx | `documented` | — | |
| POST /api/admin/content/chapters/:id/delete | api/admin.mdx | `documented` | — | |
| POST /api/admin/content/chapters/:id/rename | api/admin.mdx | `documented` | — | |
| POST /api/admin/content/chapters/:id/publish | api/admin.mdx | `documented` | — | |
| POST /api/admin/content/chapters/:id/summary | api/admin.mdx | `documented` | — | |
| GET /api/admin/content/chapters/:id/summary | api/admin.mdx | `documented` | — | |
| GET /api/admin/content/chapters/:id/links | api/admin.mdx | `documented` | — | |
| GET /api/admin/content/chapters | api/admin.mdx | `documented` | — | |
| GET /api/admin/content/chapters/graph | api/admin.mdx | `documented` | — | |
| GET /api/admin/content/chapters/link-suggestions | api/admin.mdx | `documented` | — | |
| POST /api/admin/content/exercises | api/admin.mdx | `documented` | — | |
| POST /api/admin/content/exercises/:id/update | api/admin.mdx | `documented` | — | |
| POST /api/admin/content/exercises/:id/delete | api/admin.mdx | `documented` | — | |
| GET /api/admin/content/exercises | api/admin.mdx | `documented` | — | |
| GET /api/admin/users | api/admin.mdx | `documented` | — | |
| POST /api/admin/users/:id/role | api/admin.mdx | `documented` | — | |
| POST /api/admin/users/:id/suspension | api/admin.mdx | `documented` | — | |
| GET /api/admin/community/threads | api/admin.mdx | `documented` | — | |
| POST /api/admin/forum/threads/:threadId/pin | api/admin.mdx | `documented` | — | |
| GET /api/admin/moderation/flags | api/admin.mdx | `documented` | — | |
| POST /api/admin/moderation/flags/:id/resolve | api/admin.mdx | `documented` | — | |
| GET /api/admin/notifications | api/admin.mdx | `documented` | — | |
| POST /api/admin/notifications | api/admin.mdx | `documented` | — | |
| GET /api/admin/settings | api/admin.mdx | `documented` | — | |
| POST /api/admin/settings/:key | api/admin.mdx | `documented` | — | |
| GET /api/admin/audit/content | api/admin.mdx | `documented` | — | |
| GET /api/admin/audit/forum | api/admin.mdx | `documented` | — | |
| GET /api/admin/audit/moderation | api/admin.mdx | `documented` | — | |
| GET /api/admin/audit/notifications | api/admin.mdx | `documented` | — | |
| GET /api/admin/audit/settings | api/admin.mdx | `documented` | — | |
| GET /api/admin/audit/users | api/admin.mdx | `documented` | — | |
| GET /api/admin/audit | api/admin.mdx | `documented` | — | Aggregated |

---

## TRACKED_FRONTEND_COMPONENTS

### UI Components (`components/ui/`)
| Component | Doc File | Status | Hash | Notes |
|-----------|----------|--------|------|-------|
| badge.tsx | frontend/design-system.mdx | `documented` | — | CVA-based |
| button.tsx | frontend/design-system.mdx | `documented` | — | CVA-based |
| card.tsx | frontend/design-system.mdx | `documented` | — | |
| checkbox.tsx | frontend/design-system.mdx | `documented` | — | |
| confirm-dialog.tsx | frontend/design-system.mdx | `documented` | — | |
| input.tsx | frontend/design-system.mdx | `documented` | — | |
| select.tsx | frontend/design-system.mdx | `documented` | — | |

### Auth Components (`components/auth/`)
| Component | Doc File | Status | Hash | Notes |
|-----------|----------|--------|------|-------|
| auth-guard-message.tsx | frontend/auth.mdx | `documented` | — | |
| auth-layout.tsx | frontend/auth.mdx | `documented` | — | |
| bento_auth-field.tsx | frontend/auth.mdx | `documented` | — | |
| form-field.tsx | frontend/auth.mdx | `documented` | — | |
| hero-illustration.tsx | frontend/auth.mdx | `documented` | — | |
| login-form.tsx | frontend/auth.mdx | `documented` | — | |
| logout-button.tsx | frontend/auth.mdx | `documented` | — | |
| password-input.tsx | frontend/auth.mdx | `documented` | — | |
| register-form.tsx | frontend/auth.mdx | `documented` | — | |

### Learn Components (`components/learn/`)
| Component | Doc File | Status | Hash | Notes |
|-----------|----------|--------|------|-------|
| ai-chat-panel.tsx | frontend/learn.mdx | `documented` | — | Streaming + focus management |
| ask-ai-button.tsx | frontend/learn.mdx | `documented` | — | |
| chapter-card.tsx | frontend/learn.mdx | `documented` | — | |
| chapter-exercises-with-ai.tsx | frontend/learn.mdx | `documented` | — | |
| chapter-progress-tracker.tsx | frontend/learn.mdx | `documented` | — | |
| chapter-study-content-with-ai.tsx | frontend/learn.mdx | `documented` | — | |
| chapter-study-workspace.tsx | frontend/learn.mdx | `documented` | — | |
| exercise-accordion.tsx | frontend/learn.mdx | `documented` | — | |
| exercise-item.tsx | frontend/learn.mdx | `documented` | — | |
| exercise-solution-panel.tsx | frontend/learn.mdx | `documented` | — | |
| flashcard-card.tsx | frontend/learn.mdx | `documented` | — | |
| flashcard-deck.tsx | frontend/learn.mdx | `documented` | — | 3D flip animation |
| markdown-content.tsx | frontend/learn.mdx | `documented` | — | |
| markdown-math-renderer.tsx | frontend/learn.mdx | `documented` | — | KaTeX + accessibility |
| mock-exam-result-details.tsx | frontend/mock-exams.mdx | `documented` | — | |
| question-navigator.tsx | frontend/mock-exams.mdx | `documented` | — | |
| quest-exercises-view.tsx | frontend/learn.mdx | `documented` | — | |
| quest-flashcard-view.tsx | frontend/learn.mdx | `documented` | — | |
| quest-header.tsx | frontend/learn.mdx | `documented` | — | |
| quest-quiz-view.tsx | frontend/learn.mdx | `documented` | — | |
| quest-summary-view.tsx | frontend/learn.mdx | `documented` | — | |
| quest-tab-bar.tsx | frontend/learn.mdx | `documented` | — | |
| quiz-question-card.tsx | frontend/learn.mdx | `documented` | — | Keyboard accessible |
| quiz-question-review-list.tsx | frontend/learn.mdx | `documented` | — | |
| quiz-result-summary.tsx | frontend/learn.mdx | `documented` | — | |
| quiz-runner.tsx | frontend/learn.mdx | `documented` | — | aria-live region |
| quiz-timer.tsx | frontend/learn.mdx | `documented` | — | |
| shareable-result-card.tsx | frontend/learn.mdx | `documented` | — | html-to-image |
| subject-header.tsx | frontend/learn.mdx | `documented` | — | |
| subject-view-switcher.tsx | frontend/learn.mdx | `documented` | — | |

### Dashboard Components (`components/dashboard/`)
| Component | Doc File | Status | Hash | Notes |
|-----------|----------|--------|------|-------|
| DashboardClient.tsx | frontend/dashboard.mdx | `documented` | — | |
| StatsCards.tsx | frontend/dashboard.mdx | `documented` | — | |
| dashboard-chrome-layout.tsx | frontend/dashboard.mdx | `documented` | — | |
| dashboard-notifications-control.tsx | frontend/dashboard.mdx | `documented` | — | |
| dashboard-settings-panel.tsx | frontend/dashboard.mdx | `documented` | — | |
| recent-activity-feed.tsx | frontend/dashboard.mdx | `documented` | — | |
| streak-card.tsx | frontend/dashboard.mdx | `documented` | — | |
| subject-progress-card.tsx | frontend/dashboard.mdx | `documented` | — | |
| subject-progress-table.tsx | frontend/dashboard.mdx | `documented` | — | |
| weekly-activity-heatmap.tsx | frontend/dashboard.mdx | `documented` | — | |
| welcome-card.tsx | frontend/dashboard.mdx | `documented` | — | |

### Stats Components (`components/stats/`)
| Component | Doc File | Status | Hash | Notes |
|-----------|----------|--------|------|-------|
| daily-streak-heatmap.tsx | frontend/stats.mdx | `documented` | — | |
| quiz-accuracy-trend.tsx | frontend/stats.mdx | `documented` | — | |
| stats-consistency-calendar.tsx | frontend/stats.mdx | `documented` | — | |
| stats-focus-areas.tsx | frontend/stats.mdx | `documented` | — | |
| stats-goals.tsx | frontend/stats.mdx | `documented` | — | |
| stats-hero-kpi-strip.tsx | frontend/stats.mdx | `documented` | — | |
| stats-quiz-performance-chart.tsx | frontend/stats.mdx | `documented` | — | |
| stats-study-volume-chart.tsx | frontend/stats.mdx | `documented` | — | |
| stats-subject-performance-grid.tsx | frontend/stats.mdx | `documented` | — | |
| stats-weekly-goals.tsx | frontend/stats.mdx | `documented` | — | |
| subject-progress-overview.tsx | frontend/stats.mdx | `documented` | — | |
| weekly-trend.tsx | frontend/stats.mdx | `documented` | — | |

### Forum Components (`components/forum/`)
| Component | Doc File | Status | Hash | Notes |
|-----------|----------|--------|------|-------|
| forum-filter-bar.tsx | frontend/forum.mdx | `documented` | — | |
| forum-reply-actions.tsx | frontend/forum.mdx | `documented` | — | |
| forum-reply-form.tsx | frontend/forum.mdx | `documented` | — | |
| forum-reply-list.tsx | frontend/forum.mdx | `documented` | — | |
| forum-thread-card.tsx | frontend/forum.mdx | `documented` | — | |
| forum-thread-feed.tsx | frontend/forum.mdx | `documented` | — | |
| forum-thread-form.tsx | frontend/forum.mdx | `documented` | — | |
| forum-thread-header.tsx | frontend/forum.mdx | `documented` | — | |
| forum-thread-list.tsx | frontend/forum.mdx | `documented` | — | |

### Admin Components (`components/admin/`)
| Component | Doc File | Status | Hash | Notes |
|-----------|----------|--------|------|-------|
| action-button.tsx | frontend/admin.mdx | `documented` | — | |
| admin-analytics-panel.tsx | frontend/admin.mdx | `documented` | — | |
| admin-analytics-subject-table.tsx | frontend/admin.mdx | `documented` | — | |
| admin-audit-log-list.tsx | frontend/admin.mdx | `documented` | — | |
| admin-audit-panel.tsx | frontend/admin.mdx | `documented` | — | |
| admin-audit-table.tsx | frontend/admin.mdx | `documented` | — | |
| admin-command-center-panel.tsx | frontend/admin.mdx | `documented` | — | |
| admin-community-panel.tsx | frontend/admin.mdx | `documented` | — | |
| admin-content-panel.tsx | frontend/admin.mdx | `documented` | — | |
| admin-curriculum-builder.tsx | frontend/admin.mdx | `documented` | — | |
| admin-forum-panel.tsx | frontend/admin.mdx | `documented` | — | |
| admin-guard.tsx | frontend/admin.mdx | `documented` | — | |
| admin-moderation-panel.tsx | frontend/admin.mdx | `documented` | — | |
| admin-users-table.tsx | frontend/admin.mdx | `documented` | — | |

### Foundation Components (`components/foundation/`)
| Component | Doc File | Status | Hash | Notes |
|-----------|----------|--------|------|-------|
| app-shell.tsx | frontend/overview.mdx | `documented` | — | |
| auth-layout-wrapper.tsx | frontend/auth.mdx | `documented` | — | |
| dashboard-primitives.tsx | frontend/dashboard.mdx | `documented` | — | |
| left-rail.tsx | frontend/overview.mdx | `documented` | — | |

### Other Components
| Component | Doc File | Status | Hash | Notes |
|-----------|----------|--------|------|-------|
| ai/ai-tutor-chat.tsx | ai-tools/ai-tutor.mdx | `pending` | — | |
| graph/chapter-link-graph.tsx | frontend/learn.mdx | `documented` | — | |
| layout/page-container.tsx | frontend/overview.mdx | `documented` | — | |
| navigation/breadcrumbs.tsx | frontend/overview.mdx | `documented` | — | |

---

## TRACKED_DATABASE_TABLES

| Table | Doc File | Status | Hash | Notes |
|-------|----------|--------|------|-------|
| user | architecture/database.mdx | `documented` | — | |
| session | architecture/database.mdx | `documented` | — | Better Auth |
| account | architecture/database.mdx | `documented` | — | Better Auth |
| verification | architecture/database.mdx | `documented` | — | Better Auth |
| boards | architecture/database.mdx | `documented` | — | |
| board_classes | architecture/database.mdx | `documented` | — | |
| subjects | architecture/database.mdx | `documented` | — | |
| chapters | architecture/database.mdx | `documented` | — | |
| exercises | architecture/database.mdx | `documented` | — | |
| flashcards | architecture/database.mdx | `documented` | — | |
| quizzes | architecture/database.mdx | `documented` | — | |
| quiz_questions | architecture/database.mdx | `documented` | — | |
| quiz_attempts | architecture/database.mdx | `documented` | — | |
| user_progress | architecture/database.mdx | `documented` | — | |
| ai_chat_sessions | architecture/database.mdx | `documented` | — | |
| ai_messages | architecture/database.mdx | `documented` | — | |
| ai_usage_logs | architecture/database.mdx | `documented` | — | |
| forum_threads | architecture/database.mdx | `documented` | — | |
| forum_replies | architecture/database.mdx | `documented` | — | |
| forum_reply_votes | architecture/database.mdx | `documented` | — | Renamed from forum_votes |
| mock_exams | architecture/database.mdx | `documented` | — | |
| chapter_title_aliases | architecture/database.mdx | `documented` | — | |
| chapter_summary_links | architecture/database.mdx | `documented` | — | |
| chapter_summary_media | architecture/database.mdx | `documented` | — | |
| moderation_flags | architecture/database.mdx | `documented` | — | |
| admin_audit_logs | architecture/database.mdx | `documented` | — | |
| admin_notifications | architecture/database.mdx | `documented` | — | |
| admin_settings | architecture/database.mdx | `documented` | — | |
| institutes | architecture/database.mdx | `documented` | — | |
| content_sources | architecture/database.mdx | `documented` | — | |

---

## TRACKED_E2E_TESTS

| Spec File | Doc File | Status | Hash | Notes |
|-----------|----------|--------|------|-------|
| smoke.spec.ts | dev/testing.mdx | `documented` | — | |
| auth-resilience.spec.ts | dev/testing.mdx | `documented` | — | |
| phase1-forum-dashboard-chrome.spec.ts | dev/testing.mdx | `documented` | — | |
| phase2-auth-dashboard.spec.ts | dev/testing.mdx | `documented` | — | |
| phase3-auth-layout-routes.spec.ts | dev/testing.mdx | `documented` | — | |
| theme-light.spec.ts | dev/testing.mdx | `documented` | — | |
| ui-quality.spec.ts | dev/testing.mdx | `documented` | — | |
| stats-screen.spec.ts | dev/testing.mdx | `documented` | — | |
| student-subject-graph-performance.spec.ts | dev/testing.mdx | `documented` | — | |
| student-subject-graph.spec.ts | dev/testing.mdx | `documented` | — | |
| student-subject-page-baseline-performance.spec.ts | dev/testing.mdx | `documented` | — | |
| admin-left-rail.spec.ts | dev/testing.mdx | `documented` | — | |
| admin-phase1-shell.spec.ts | dev/testing.mdx | `documented` | — | |
| admin-phase2-moderation-users.spec.ts | dev/testing.mdx | `documented` | — | |
| admin-phase3-community-analytics.spec.ts | dev/testing.mdx | `documented` | — | |
| admin-phase4-notifications-settings.spec.ts | dev/testing.mdx | `documented` | — | |
| admin-phase5-users-lifecycle.spec.ts | dev/testing.mdx | `documented` | — | |
| admin-phase6-audit-center.spec.ts | dev/testing.mdx | `documented` | — | |
| admin-phase7-command-center.spec.ts | dev/testing.mdx | `documented` | — | |
| admin-phase8-curriculum-builder.spec.ts | dev/testing.mdx | `documented` | — | |
| admin-summary-editor-codemirror.spec.ts | dev/testing.mdx | `documented` | — | |
| admin-summary-editor-performance.spec.ts | dev/testing.mdx | `documented` | — | |
| admin-summary-graph.spec.ts | dev/testing.mdx | `documented` | — | |
| admin-summary-wikilinks.spec.ts | dev/testing.mdx | `documented` | — | |
| global-setup.mjs | dev/testing.mdx | `documented` | — | Test setup helper |

---

## TRACKED_INFRA_FILES

| Source File | Doc File | Status | Hash | Notes |
|-------------|----------|--------|------|-------|
| docker-compose.yml | infra/docker.mdx | `documented` | — | Postgres, PgBouncer, Redis, MinIO, Nginx, Backend |
| infra/nginx.conf | infra/load-balancing.mdx | `documented` | — | |
| backend/src/lib/queue.ts | infra/background-jobs.mdx | `documented` | — | BullMQ |
| backend/src/lib/cache/cache.service.ts | infra/caching.mdx | `documented` | — | |
| backend/.env.example | infra/environment.mdx | `documented` | — | |
| frontend/.env.local.example | infra/environment.mdx | `documented` | — | |

---

## TRACKED_GUIDES

| Guide Topic | Doc File | Status | Hash |
|-------------|----------|--------|------|
| Project setup | dev/setup.mdx | `documented` | — |
| Testing overview | dev/testing.mdx | `documented` | — |
| Contributing | dev/contributing.mdx | `documented` | — |
| Code style | dev/code-style.mdx | `documented` | — |
| Database workflow | dev/database-guide.mdx | `documented` | — |
| E2E testing guide | dev/e2e-testing.mdx | `documented` | — |

---

## STATUS_DEFINITIONS

| Status | Meaning | Action Required |
|--------|---------|-----------------|
| `pending` | Item exists in code but has no documentation | Create documentation |
| `documented` | Item is documented and hash matches current code | No action |
| `stale` | Item hash doesn't match current code | Update documentation |
| `deprecated` | Item was removed from code | Remove or archive documentation |

---

## COMMIT TRACKING

This section tracks the last documented commit from the learningopk repository. When you pull new code from GitHub, compare the current HEAD against this hash to determine what changed.

| Field | Value |
|-------|-------|
| **Last Documented Commit** | `80339009530c6af406919982486a0aea0487517f` |
| **Commit Message** | `Merge pull request #11 from codleed/feature/sidebar-icon-centering` |
| **Documented On** | 2026-03-30 |
| **Documentation Version** | 1.0.0 |

### How to Detect New Changes

After pulling new code from GitHub, run this workflow:

```bash
# 1. Get the current HEAD commit in learningopk
cd learningopk && git log -1 --format="%H"

# 2. Compare against the Last Documented Commit above
git diff 80339009530c6af406919982486a0aea0487517f..HEAD --name-only

# 3. Focus on these paths (they affect documentation):
#    - backend/src/routes/*.ts        → API docs
#    - backend/src/lib/db/schema.ts   → Database docs
#    - backend/src/services/*.ts      → Feature docs
#    - backend/src/workers/*.ts       → Infrastructure docs
#    - frontend/src/components/**/*.tsx → Frontend docs
#    - frontend/app/**/*.tsx           → Frontend page docs
#    - frontend/tests/e2e/*.spec.ts   → Testing docs
#    - docker-compose.yml             → Infrastructure docs

# 4. For each changed file, read the corresponding doc file and update it
# 5. Update the Last Documented Commit hash above
```

### Update Checklist After Each Pull

- [ ] Run `git diff` against last documented commit
- [ ] Identify NEW endpoints/components/tables not in TRACKED_* sections
- [ ] Identify CHANGED endpoints/components/tables (hash mismatch)
- [ ] Update or create documentation for new/changed items
- [ ] Add new items to TRACKED_* sections with status `documented`
- [ ] Update the Last Documented Commit hash above
- [ ] Update the CHANGE LOG below

---

## CHANGE LOG

| Date | Change | Affected Items |
|------|--------|----------------|
| 2026-04-04 | Synced documentation with current learningopk codebase | All docs updated to match 22 tables, correct mount points, all endpoints |
| 2026-04-04 | Fixed AI Chat mount point | `/api/ai-chat/*` → `/api/ai/*` in ai-chat.mdx, overview.mdx |
| 2026-04-04 | Fixed Profile API path | `/api/profile/me/profile-image` → `/api/users/me/profile-image` in auth.mdx |
| 2026-04-04 | Added missing chapter-media endpoints | presigned-upload, confirm, list, delete |
| 2026-04-04 | Added missing admin endpoints | subjects delete, quiz CRUD, quiz-questions CRUD, flashcards CRUD/reorder, jobs |
| 2026-04-04 | Updated table count | 28 → 22 tables (actual count from schema.ts) |
| 2026-04-04 | Updated forum_votes → forum_reply_votes | Table renamed in codebase |
| 2026-04-04 | Added content_sources table | New table tracked |
| 2026-04-04 | Updated E2E test count | 24 → 25 specs (added global-setup.mjs) |
| 2026-04-04 | Marked boards/classes/subjects/institutes as not mounted | Routers exist but not mounted in server.ts |
| 2026-03-30 | Initial documentation creation | All 62 API endpoints, 86 components, 28 tables, 24 E2E specs |
| 2026-03-30 | Status update — documented items identified | 151 items updated from `pending` to `documented` |
| 2026-03-30 | Created frontend/auth.mdx, forum.mdx, mock-exams.mdx, stats.mdx, design-system.mdx | 39 components updated from `pending` to `documented` |
| 2026-03-30 | Created api/health, boards, classes, subjects, institutes, profile, chapter-media docs | 7 API endpoint groups documented |
| 2026-03-30 | Created api/database.mdx | 28 tables fully documented |
| 2026-03-30 | Created infra/caching, load-balancing, background-jobs docs | 3 infrastructure files documented |
| 2026-03-30 | Created dev/code-style, database-guide, e2e-testing docs | 3 development guides documented |
| 2026-03-30 | Created features/gamification, ai-tutor, forum, progress docs | 4 feature docs created |
| 2026-03-30 | Updated docs.json navigation | 6 tabs, 16 groups, 40+ pages |
| 2026-03-30 | Removed Mintlify starter kit files | 6 directories, 4 files deleted |
