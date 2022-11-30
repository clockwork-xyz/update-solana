# Update Solana

A GitHub action that generates a pull request to update a repo's dependencies so they remain in sync with the latest stable release of Solana.

## Usage

Below is an example of a Github workflow that runs once per day and generates a PR if any of the repo's Solana dependencies are behind the stable release. 

```yaml
name: Update Solana

on:
  schedule: 
    - cron: "00 00 * * *" # Run this worflow daily
  workflow_dispatch:

jobs:
  update-solana:
    name: Update Solana
    runs-on: ubuntu-latest
    timeout-minutes: 30
    steps:
      - uses: actions/checkout@v2
      - uses: clockwork-xyz/update-solana@v1
```

### Action inputs

All inputs are **optional**. If not set, sensible defaults will be used.

| Name | Description | Default |
| --- | --- | --- |
| `labels` | A comma or newline-separated list of labels added to the PR. | |
| `reviewers` | A comma or newline-separated list of reviewers (GitHub usernames) to request a review from. | |

## Permissions

For this action to work you must explicitly allow GitHub Actions to create pull requests.
This setting can be found in a repository's settings under Actions > General > Workflow permissions.

For repositories belonging to an organization, this setting can be managed by admins in organization settings under Actions > General > Workflow permissions.
