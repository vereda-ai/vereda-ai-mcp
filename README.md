# Vereda AI — MCP Server for Claude

Connect Claude to your engineering team's performance data. Ask about standups, prepare for 1:1s, track goals, detect burnout risk, and manage action items — all from Claude.

## What You Can Do

| Ask Claude... | What happens |
|---|---|
| "Prepare me for my 1:1 with Sarah" | Pulls recent standups, goals, sentiment, and blockers into talking points |
| "Summarize this week's standups" | Aggregates standup responses with blocker detection and trends |
| "Who on my team needs attention?" | Surfaces engineers showing signs of disengagement or risk |
| "What has Jake been working on?" | Shows recent standup updates, goal progress, and activity |
| "How is my team doing?" | Team health summary with participation, sentiment, and patterns |
| "Create an action item for Maria" | Creates a tracked task directly in Vereda |
| "Update the API migration goal to 75%" | Updates goal progress |

## Available Tools

### Read tools

- **`ask_about_engineer`** — Natural language questions about any team member
- **`get_engineer_insights`** — Detailed engineer activity and sentiment data
- **`get_team_health_summary`** — Team-wide health metrics
- **`get_standup_summary`** — Standup aggregation with blocker detection
- **`get_pulse_survey_results`** — Pulse survey responses and trends
- **`get_needs_attention`** — Engineers who may need manager support
- **`get_team_risk_analysis`** — Daily risk scoring for your team
- **`get_team_patterns`** — Behavioral and delivery patterns over time
- **`get_career_context`** — Engineer's level, growth trajectory, and history

### Write tools

- **`prep_for_one_on_one`** — AI-generated 1:1 talking points
- **`prep_for_performance_review`** — Review prep grounded in months of data
- **`create_goal`** / **`update_goal_progress`** — Goal management
- **`create_action_item`** / **`update_action_item`** / **`list_action_items`** — Task tracking
- **`add_check_in_notes`** — Add notes to scheduled check-ins
- **`create_note`** / **`search_notes`** / **`list_recent_notes`** — Private manager notes

## Setup

### 1. Create a Vereda account

Sign up at [app.vereda.ai](https://app.vereda.ai). Standups are free for your whole team.

### 2. Connect to Claude

Add the Vereda MCP server in your Claude settings:

**Server URL:** `https://app.vereda.ai/api/mcp`

Authentication is handled via OAuth — Claude will prompt you to authorize your Vereda account on first use.

### 3. Start asking questions

Once connected, just ask Claude about your team. It will automatically use the right Vereda tools.

## Privacy

- No PII (emails, external account IDs) is sent to Claude — only names, team context, and work data
- All tool invocations are audit-logged
- Data stays within your organization's scope

## Links

- [Vereda AI](https://www.vereda.ai)
- [Pricing](https://www.vereda.ai/pricing) — Free standups for your whole team. Pro at $15/seat/month.
- [Compare to other tools](https://www.vereda.ai/compare/lattice-alternative)

## License

MIT
