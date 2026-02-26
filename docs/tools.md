# Vereda MCP Tools — Detailed Reference

All tools are available at `https://app.vereda.ai/api/mcp` via OAuth 2.0 authentication.

---

## ask_about_engineer

Ask a natural language question about an engineer and get a direct AI-synthesized answer. Fetches comprehensive engineer data (goals, action items, check-ins, git activity, Jira/Linear tickets, daily insights) and uses AI to answer the specific question accurately.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `engineer_identifier` | string | Yes | Engineer name or email |
| `question` | string | Yes | Natural language question about the engineer |

**Example:** "What blockers has Sarah mentioned this week?"

**Returns:** An AI-generated direct answer referencing specific details from the engineer's data.

---

## prep_for_one_on_one

Prepare for a 1:1 meeting with an engineer by gathering all relevant data in one call. Pulls recent standups, goal progress, open action items, sentiment data, AI insights, and private notes into structured talking points.

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| `engineer_name` | string | One of name/email required | — | Full or partial name (case-insensitive) |
| `engineer_email` | string | One of name/email required | — | Email address |
| `lookback_days` | number | No | 14 | Days of history to include |

**Returns:** Comprehensive prep document with recent activity, goals, action items, standup highlights, private notes, AI insights, and suggested discussion topics.

---

## prep_for_performance_review

Prepare for a formal performance review with comprehensive data over a longer review period. Includes competency gap analysis and career ladder context.

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| `engineer_name` | string | Yes | — | Full or partial engineer name |
| `engineer_email` | string | No | — | Alternative to name |
| `review_period_days` | number | No | 90 | Review period (90 = quarterly, 365 = annual) |

**Returns:** Goals completed/in-progress/at-risk, competency expectations with gap analysis, activity patterns, action item completion rate, past review summaries, and suggested discussion points.

---

## get_engineer_insights

Get synthesized performance insights for an engineer including activity details, goals, check-ins, competency context, and actionable links to PRs/tickets.

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| `engineer_identifier` | string | Yes | — | Engineer email or full name |
| `timeframe_days` | number | No | 14 | Days to look back (max: 90) |

**Returns:** Engineer profile, goal summary, recent check-in highlights, activity patterns (PR/commit/review counts), detailed recent PRs with GitHub URLs, commits, Jira/Linear tickets, AI insights, private notes, and competency level context.

---

## get_team_health_summary

Get team-level health metrics, delivery stats, and AI-generated insights.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `team_identifier` | string | No | Team name or ID (auto-selected if only one team) |

**Returns:** Team metadata, member list with levels, weekly standup/blocker counts, AI-generated team summary, team highlights, per-engineer highlights, and recommendations.

---

## get_standup_summary

Get standup data for a team or individual engineer. Returns full standup content for all team members in the timeframe.

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| `engineer_identifier` | string | No | — | Engineer email or name (omit for team-level) |
| `team_identifier` | string | No | — | Team name or ID |
| `timeframe_days` | number | No | 14 | Days to look back (max: 30) |

**Returns:** Standup entries with content, dates, source type, participation stats per member, and update counts.

---

## get_pulse_survey_results

Get anonymized, aggregated pulse survey results for your organization or team. Never exposes individual responses.

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| `scope` | `'organization'` \| `'team'` | No | `'organization'` | Org-wide or team-specific |
| `team_identifier` | string | No | — | Required if scope is `'team'` |
| `periods` | number | No | 3 | Historical periods for trending (max: 6) |

**Returns:** Aggregated scores (engagement, satisfaction, manager relationship, growth, work-life balance), stay intent distribution, response rates, trend data, team breakdown, and AI-generated themes.

---

## get_needs_attention

Get engineers who need immediate manager attention based on active signals and escalations.

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| `team_identifier` | string | No | — | Team name or ID (optional if one team) |
| `include_acknowledged` | boolean | No | false | Include already-acknowledged signals |

**Returns:** Engineers needing attention with risk level, signals, and conversation starters. Urgent and pending escalations. Signal breakdown by type.

---

## get_team_risk_analysis

Get risk analysis for your team. Risk scores 0-100 with levels LOW/MODERATE/HIGH.

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| `team_identifier` | string | No | — | Team name or ID (optional if one team) |
| `date` | string | No | Most recent | Analysis date (YYYY-MM-DD) |

**Returns:** Per-engineer risk scores and levels, risk categories (activity_gap, sentiment_decline, velocity_decrease, blocker_accumulation), team average, and recommendations.

---

## get_team_patterns

Get team-wide patterns, shared blockers, and positive signals.

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| `team_identifier` | string | No | — | Team name or ID (optional if one team) |
| `timeframe_days` | number | No | 7 | Days to look back |

**Returns:** Shared blockers, team-wide behavioral patterns, positive signals (velocity increases, goal completions, sentiment improvements), coaching opportunities, and suggested actions.

---

## get_career_context

Get career development context for an engineer including level expectations, competency matrix, and promotion gap analysis.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `engineer_name` | string | Yes | Full or partial engineer name |
| `engineer_email` | string | No | Alternative to name |

**Returns:** Current level and competency expectations, full career ladder, next level requirements with gap analysis, career-focused goals, and AI-generated career discussion prompts.

---

## create_goal

Create a new career development goal for an engineer. Prompts for SMART criteria if the goal is incomplete.

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| `engineerName` | string | No | — | Engineer name (defaults to calling user) |
| `engineerId` | string | No | — | Engineer ID if known |
| `title` | string | Yes | — | Goal title (min 5 characters) |
| `description` | string | No | — | What success looks like |
| `successCriteria` | string | No | — | Measurable criteria for completion |
| `dueDate` | string | No | — | ISO date or natural language ("end of Q2") |
| `quarterLabel` | string | No | — | Quarter label (e.g., "Q1 2025") |
| `priority` | `'high'` \| `'medium'` \| `'low'` | No | `'medium'` | Priority level |
| `competencyTopics` | string[] | No | — | Competency topics to link (fuzzy matched) |
| `tags` | string[] | No | — | Tags for organizing |

**Returns:** Created goal with all fields. If SMART criteria are incomplete, returns a `needs_more_info` response prompting for missing fields.

---

## update_goal_progress

Add a progress note to a goal or update its status. Fuzzy matches engineer names and goal titles.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `goalId` | string | No | Goal ID if known |
| `goalTitle` | string | No | Title or keywords to find the goal |
| `engineerId` | string | No | Engineer ID if known |
| `engineerName` | string | No | Engineer name (used with goalTitle) |
| `note` | string | Yes | Progress note describing what was accomplished |
| `progressDelta` | integer (-10 to +10) | No | Change in progress |
| `sentiment` | `'positive'` \| `'neutral'` \| `'negative'` | No | Sentiment of the update |
| `status` | `'active'` \| `'completed'` \| `'archived'` | No | New status (only if explicitly changing) |

**Returns:** Updated goal and the new progress note.

---

## create_action_item

Create a short-term action item (task/follow-up) for an engineer.

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| `engineerName` | string | One of name/id required | — | Engineer name |
| `engineerId` | string | One of name/id required | — | Engineer ID |
| `title` | string | Yes | — | Brief task description (min 3 characters) |
| `description` | string | No | — | Additional details |
| `dueDate` | string | No | — | YYYY-MM-DD or natural language ("Friday", "next week") |
| `severity` | `'high'` \| `'medium'` \| `'low'` | No | `'medium'` | Priority level |
| `linkedGoalTitle` | string | No | — | Link to an active goal by title (fuzzy matched) |

**Returns:** Created action item with ID, title, severity, status, dueDate, and linkedGoal.

---

## update_action_item

Update an existing action item's status, details, or mark it complete.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `actionItemId` | string | No | Action item ID if known |
| `engineerName` | string | No | Engineer name to find their items |
| `actionItemTitle` | string | No | Title or keywords (used with engineerName) |
| `status` | `'active'` \| `'in_progress'` \| `'completed'` \| `'cancelled'` | No | New status |
| `title` | string | No | Updated title |
| `description` | string | No | Updated description |
| `dueDate` | string | No | New due date |
| `severity` | `'high'` \| `'medium'` \| `'low'` | No | Updated priority |

**Returns:** Updated action item.

---

## list_action_items

List action items for an engineer, optionally filtered by status.

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| `engineerName` | string | Yes | — | Engineer name |
| `engineerId` | string | No | — | Engineer ID if known |
| `status` | `'active'` \| `'in_progress'` \| `'completed'` \| `'cancelled'` \| `'all'` | No | `'active'` | Filter by status |
| `includeOverdueOnly` | boolean | No | false | Only show overdue items |

**Returns:** Up to 10 action items with overdue/high-priority counts.

---

## add_check_in_notes

Add notes to a 1:1 check-in with an engineer. Creates or updates the check-in for a given date.

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| `engineerName` | string | Yes | — | Engineer you had a 1:1 with |
| `engineerId` | string | No | — | Engineer ID if known |
| `date` | string | No | Today | Date of check-in (YYYY-MM-DD) |
| `sharedNotes` | string | No | — | Notes visible to both manager and engineer |
| `privateNotes` | string | No | — | Notes only visible to the manager |
| `topics` | object[] | No | — | Structured topics (title, notes, isPrivate) |

**Returns:** Confirmation with outstanding items: goals not updated in 14+ days, overdue goals, and overdue/high-priority action items.

---

## create_note

Save a private note. Notes are automatically tagged with people, projects, topics, and links in the background.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `content` | string | Yes | Note content (free-form text) |

**Returns:** Note ID, content preview, and creation timestamp.

---

## search_notes

Search across your private notes using natural language. Returns matching notes with an AI-synthesized summary cross-referencing check-ins, action items, and goals.

| Parameter | Type | Required | Description |
|---|---|---|---|
| `query` | string | Yes | Natural language search query |
| `timeframe` | `'1d'` \| `'7d'` \| `'30d'` \| `'90d'` \| `'1y'` | No | Time range to search |

**Returns:** AI synthesis of matching notes cross-referenced with team data, and list of matching notes with tags.

---

## list_recent_notes

List your most recent private notes.

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| `limit` | number | No | 10 | Number of notes to return (max: 25) |

**Returns:** Total note count and list of notes with content, tags, and timestamps.
