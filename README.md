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
| Domain Expiry Reminder | Check domain registration expiry daily and notify Slack only for domains with fewer than 60 days left |
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

## Domain Expiry Reminder

Import `workflows/domain-expiry-reminder.json` and edit the arrays in **Configure Domains**:

```js
const domains = ['example.com', 'example.org'];
const registrars = ['Porkbun', 'babal.host'];
const warningDays = 60;
```

Entries match by index: `example.com` belongs to Porkbun and `example.org` belongs to babal.host. The arrays must have equal lengths, registrar labels must be nonempty, and domains must be unique. Use registrable domains without schemes or paths, and punycode for internationalized domains. Select Slack credentials and replace `YOUR_SLACK_CHANNEL` in **Send Domain Expiry Reminder**.

The workflow runs daily at 08:00 in your n8n workflow/instance timezone and checks every configured domain using the public [RDAP bootstrap service](https://about.rdap.org/). Registrar names are labels for the reminder, not account integrations; no registrar, SSH, or RDAP credentials are needed. If both registry and registrar expiration dates are published, it uses the earliest date.

One Slack message lists only domains with fewer than 60 remaining days, sorted by urgency, with their registrar and expiration date. Remaining days are rounded up; domains showing exactly 60 days are excluded. Already expired domains are included. If no domains qualify, no Slack message is sent.

Failed lookups and missing expiration dates are logged with `console.warn` in the Code node and excluded from Slack. Exclusion does not confirm that a domain is safe: some registries do not publish expiration dates through RDAP. Verify those dates with your registrar. Test the workflow before activating it.

## Contributing

Contributions of sanitized, reusable DevOps n8n workflows are welcome. Never include credentials, private infrastructure details, or other secrets in exported JSON.

## License

MIT. See [LICENSE](LICENSE).
