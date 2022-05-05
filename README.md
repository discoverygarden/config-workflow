# Config Workflow

Workflow for reconciling client configs from production.

## Usage

### Inputs

- `jira-url`: Base URL the Jira instance. 
- `jira-user`: Email of the Jira API user.
- `jira-token`: API token of the Jira API user.
- `github-token`: GitHub access token
- `slack-webhook`: Optional Slack webhook URL to receive notifications.

### Example Workflow

```yaml
name: Reconcile Config
on:
  push:
  branches: ['prod-*']

jobs:
  reconcile-config:
    runs-on: ubuntu-latest
    steps:
      - uses: discoverygarden/config-workflow@main
        with:
          jira-url: "https://myjira.atlassian.net"
          jira-user: "user@example.com"
          jira-token: ${{ secrets.JIRA_API_TOKEN }}
          slack-webhook: ${{ secrets.SLACK_WEBHOOK }}
          github-token: ${{ secrets.GITHUB_TOKEN}}
```