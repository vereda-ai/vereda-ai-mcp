# Security Policy

## Reporting a Vulnerability

If you discover a security vulnerability related to the Vereda MCP server, please report it responsibly.

**Email:** security@vereda.ai

Please include:

- A description of the vulnerability
- Steps to reproduce (if applicable)
- Any potential impact

We will acknowledge your report within 48 hours and aim to resolve confirmed vulnerabilities promptly.

## How We Handle Data

### What is sent to Claude

When you use Vereda tools through Claude, the following data may be included in tool responses:

- Engineer names (first and last)
- Team and division names
- Standup responses (what people are working on, blockers)
- Goal titles, descriptions, and progress
- Action item titles and statuses
- AI-generated insights and summaries
- Aggregated metrics (delivery stats, participation rates)

### What is never sent to Claude

- Email addresses
- External account IDs (Slack, Jira, GitHub, Linear)
- Phone numbers or contact information
- Authentication credentials
- Billing or payment data

### Authentication

- OAuth 2.0 is used to authenticate your Vereda account with Claude
- Tokens are scoped to your organization
- All API requests are authenticated and authorized against your organization's data

### Audit Logging

- All MCP tool invocations are logged
- Logs include the tool called, parameters, and timestamp
- Logs are scoped to your organization and accessible to admins

## Supported Versions

This is a hosted service. The latest version at `https://app.vereda.ai/api/mcp` is always the supported version.
