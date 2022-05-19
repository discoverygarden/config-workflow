# Config Workflow

Workflow for reconciling client configs from production.

## Usage

### Inputs

- `client-id`: The Jira project id for the client(Use uppercase).
- `repo`: Repository name with owner. Defaults to current.
- `head`: Head branch to merge. Deafults to current branch.
- `base`: Base branch to merge into. Defaults to the current repo's default branch.
- `labels`: A comma seperated list of labels to add to the pull request.
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
          client-id: DGI
          jira-url: "https://myjira.atlassian.net"
          jira-user: "user@example.com"
          jira-token: ${{ secrets.JIRA_API_TOKEN }}
          slack-webhook: ${{ secrets.SLACK_WEBHOOK }}
          github-token: ${{ secrets.GITHUB_TOKEN}}
```