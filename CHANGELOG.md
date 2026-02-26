# Changelog

All notable changes to the Vereda MCP server will be documented in this file.

## [1.0.0] - 2026-02-26

### Added

- Initial release of the Vereda MCP server for Claude
- **Read tools:**
  - `ask_about_engineer` — Natural language questions about any team member
  - `get_engineer_insights` — Detailed engineer activity, sentiment, and AI-generated insights
  - `get_team_health_summary` — Team-wide health metrics and delivery stats
  - `get_standup_summary` — Standup aggregation with blocker detection
  - `get_pulse_survey_results` — Pulse survey responses and trends
  - `get_needs_attention` — Engineers who may need manager support
  - `get_team_risk_analysis` — Daily risk scoring for your team
  - `get_team_patterns` — Behavioral and delivery patterns over time
  - `get_career_context` — Engineer's level, growth trajectory, and history
- **Write tools:**
  - `prep_for_one_on_one` — AI-generated 1:1 talking points
  - `prep_for_performance_review` — Review prep grounded in months of data
  - `create_goal` / `update_goal_progress` — Goal management
  - `create_action_item` / `update_action_item` / `list_action_items` — Task tracking
  - `add_check_in_notes` — Add notes to scheduled check-ins
  - `create_note` / `search_notes` / `list_recent_notes` — Private manager notes
- OAuth 2.0 authentication
- PII filtering (no emails, external IDs, or contact info sent to Claude)
- Audit logging for all tool invocations
