# Update Solana

A GitHub action that generates a pull request to update a repo's dependencies so they remain in sync with the latest stable release of Solana.

## Usage

Below is an example of a Github workflow file that uses this action. 
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