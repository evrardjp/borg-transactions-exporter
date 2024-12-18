# Borg transactions prometheus exporter

A Prometheus exporter for monitoring BorgBackup repositories without their passphrases.
This reports the transaction happening on monitored repos, as this can be parsed without the passphrase.

This is appropriate for monitoring on a server in which you do not want to store credentials.
You should add other monitoring tools to check consistency with other exporters.

## Features
- Metrics for the last transaction number for each repository.
- Configurable via a JSON file for multiple repos

## Usage

1. Create a `config.json` file:
    ```json
    {
      "repos": ["/path/to/repo1", "/path/to/repo2"],
      "ip": "0.0.0.0",
      "port": 8080,
      "endpoint": "/metrics"
    }
    ```
2. Run the exporter:
    ```bash
    ./borgbackuptransactions_exporter -config=config.json
    ```

### Metrics exposed
- `borgbackup_last_transaction_number`

### How to scrape

```
scrape_configs:
  - job_name: "borgbackuptransactions_exporter"
    static_configs:
      - targets: ["localhost:8080"]
```
