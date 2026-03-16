# Jira Peer Review Auto-Assignment 

Automatically assigns a peer reviewer when a Jira story is moved to the **Peer Review** column — picking the team member with the lowest in-progress story point load.

## How It Works

1. A story is moved to **Peer Review** on the Jira board
2. Jira Automation fires a webhook to n8n
3. n8n fetches all in-progress issues and tallies story points per team member
4. The original author is excluded
5. The team member with the fewest in-progress points is assigned as reviewer
6. A Jira comment is posted on the ticket
7. A Slack DM is sent to the assigned reviewer

## Stack

- **n8n** — workflow orchestration (self-hosted via Docker)
- **Jira REST API** — fetching issues, assigning reviewers, posting comments
- **Jira Automation** — webhook trigger on status transition
- **Slack API** — DM notification to reviewer
- **ngrok** — local tunnel for development (Phase 1 only)
