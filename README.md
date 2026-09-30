# n8n DevOps Workflows

A collection of reusable n8n workflows for DevOps monitoring, backups, GitHub automation, server health checks, and Slack notifications.

| Workflow | Description |
|---|---|
| GitHub PR Slack Alert | Notify Slack when a PR is opened or reopened |
| Disk Usage Alert | Alert when `/` reaches 90% |
| Docker Restarting Alert | Detect restarting containers |
| PostgreSQL Backup | Back up Docker Postgres to S3 |
| EOD Reminder | Send a weekday EOD Slack reminder |
| Docker Health | Detect unhealthy or exited containers |
| Memory Alert | Alert on high RAM usage |
| CPU Alert | Alert on high CPU usage |
| SSL Expiry | Warn before SSL expiration |
| Service Alert | Detect stopped systemd services |
| Backup Failure Alert | Detect missing, empty, or stale S3 backups |

## Usage

1. Download the desired JSON file.
2. Open n8n.
3. Import the workflow from file.
4. Select your credentials.
5. Configure the server, repository, channel, and other placeholders.
6. Test the workflow.
7. Activate it.

## Credentials

These workflows intentionally contain no credentials or credential IDs. After importing, manually select the required GitHub, SSH, or Slack credentials. Remote backup workflows expect the AWS CLI to already be configured securely on the target server.

## Contributing

Contributions of sanitized, reusable DevOps n8n workflows are welcome. Never include credentials, private infrastructure details, or other secrets in exported JSON.

## License

MIT. See [LICENSE](LICENSE).
