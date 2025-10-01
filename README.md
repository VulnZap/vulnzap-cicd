# VulnZap CLI Scan Action

This GitHub Action runs a VulnZap scan via the VulnZap CLI and streams results in the job logs. The action auto-detects repository URL, branch, and commit from the GitHub context; you only provide the API key.

## Usage

```yaml
name: VulnZap Security Scan

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  security-scan:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Run VulnZap Scan
      - uses: VulnZap/vulnzap-cicd@v1
        with:
          api-key: ${{ secrets.VULNZAP_API_KEY }}
```

## Inputs

| Name      | Description                | Required |
|-----------|----------------------------|----------|
| `api-key` | Your VulnZap API Key.      | `true`   |

## Notes

- The action derives the repository URL as `https://github.com/${GITHUB_REPOSITORY}` and also passes `GITHUB_REF_NAME` and `GITHUB_SHA` to the CLI when present.
- Make sure Docker/network access is available so `npx vulnzap@latest` can install and run.

## Secrets

Add your VulnZap API Key as a secret in your repository:

1. Go to your repository's Settings → Secrets and variables → Actions
2. Click New repository secret
3. Name it `VULNZAP_CICD_API_KEY`
4. Paste your API key value and save
