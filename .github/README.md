# GitHub Actions Workflows

## sync-openapi.yml

This workflow automatically syncs the OpenAPI documentation from the BlueHive API endpoint.

### Features

- **Automatic Sync**: Downloads the latest OpenAPI spec from `https://api.bluehive.com/docs/json`
- **Change Detection**: Only commits updates when the OpenAPI spec has actually changed
- **Scheduled Runs**: Runs daily at 6 AM UTC to keep documentation current
- **Manual Trigger**: Can be triggered manually via GitHub Actions UI
- **Smart Commits**: Includes API title and version in commit messages

### How it works

1. Downloads the latest OpenAPI JSON from the BlueHive API
2. Validates the downloaded content is valid JSON
3. Compares with the existing `api-reference/openapi.json` file
4. If changes are detected:
   - Backs up the existing file
   - Updates the OpenAPI spec file
   - Formats it nicely with jq
   - Commits and pushes the changes with descriptive commit message

### Triggering

The workflow runs automatically on:
- **Schedule**: Daily at 6 AM UTC
- **Manual trigger**: Via GitHub Actions UI
- **Push to main**: When the workflow file itself is modified (for testing)

### Error Handling

- Validates JSON content before processing
- Fails gracefully if the API endpoint is unreachable
- Only commits when actual changes are detected