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