# rlsr-action
Github Action for rlsr.

## Usage
This action can be used in your GitHub workflows to install and use rlsr. Below is an example of how to use this action in your workflow:

```yaml
# .github/workflows/release.yml in a user's project
name: Create Release using Rlsr

on:
  push:
    tags:
      - 'v*.*.*' # Trigger on version tags like v1.0.0, v1.2.3

jobs:
  release:
    name: Create Release
    runs-on: ubuntu-latest # Or macos-latest, windows-latest
    permissions:
      contents: write # Needed to create GitHub releases

    steps:
      - name: Checkout code
        uses: actions/checkout@v4
        with:
          # Fetch all history and tags for changelog generation
          fetch-depth: 0

      - name: Run Rlsr Action
        uses: iamd3vil/rlsr-action@v1.0.0 # Use YOUR action repo and tag
        with:
          # Path to the rlsr config file IN THIS REPOSITORY
          config-path: 'rlsr.yml' # Or '.config/rlsr.yml', etc.
          # The GITHUB_TOKEN is automatically created by Actions
          github-token: ${{ secrets.GITHUB_TOKEN }}
          # Optional: Clean dist before build
          # rm-dist: 'true'
          # Optional: Skip publishing (for testing the build)
          # skip-publish: 'true'
```
