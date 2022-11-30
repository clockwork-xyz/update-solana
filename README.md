# Update Solana

A GitHub action that auto-generates a PR to keep a workspace's cargo dependencies up-to-date with the latest stable release of Solana.

## Usage

Below is an example of a Github workflow that calls the `update-solana` action once per day. 
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

How is how the action behaves:
- If the workspace's Solana dependencies are out-of-date, the changes will be pushed to a new branch and a pull request created.
- If there are no changes, no pull request will be created and the action exits silently.
- If a pull request already exists it will be updated if necessary. If no update is required the action exits silently.
- If a pull request exists and new changes on the base branch make the pull request unnecessary (i.e. there is no longer a diff between the pull request branch and the base), the pull request is automatically closed. 


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
