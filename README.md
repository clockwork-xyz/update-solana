# Update Solana

A GitHub action that updates a workspace's cargo dependencies to the latest stable release of Solana.

## Usage

Below is an example of a Github workflow that keeps a workspace's dependencies in sync with Solana stable channel releases. Once per day, this workflow will check if the repo's Solana dependencies are out-of-date and auto-generate a PR to update them using the [`create-pull-request`](https://github.com/marketplace/actions/create-pull-request) action. This PR can be reviewed, updated, and merged by the project's maintainers as they see fit. Notes on how this workflow behaves:
- If the workspace's Solana dependencies are out-of-date, the changes will be pushed to the `update-solana/stable` branch and a pull request created.
- If there are no changes, no pull request will be created and the action exits silently.
- If a pull request already exists it will be updated if necessary. If no update is required the action exits silently.
- If a pull request exists and new changes on the base branch make the pull request unnecessary (i.e. there is no longer a diff between the pull request branch and the base), the pull request is automatically closed. 


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
      - uses: clockwork-xyz/update-solana@v1.2.0
      - uses: peter-evans/create-pull-request@v4
        with:
          title: Update Solana to v${{ env.SOLANA_VERSION }}
          base: master
          branch: update-solana/stable
          commit-message: Update "solana-" dependencies to v${{ env.SOLANA_VERSION }}
          draft: false
          delete-branch: true
          labels: dependencies
          reviewers: nickgarfield

```


## Permissions

To use the `create-pull-request` action, you must explicitly allow GitHub Actions to create pull requests.
This setting can be found in a repository's settings under Actions > General > Workflow permissions. For repositories belonging to an organization, this setting can be managed by admins in organization settings under Actions > General > Workflow permissions.
