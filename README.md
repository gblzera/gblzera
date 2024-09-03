name: Update README Languages

on:
  # Triggers the workflow on push or pull request events but only for the default branch
  push:
    branches:
      - main
  # Also allow this workflow to be triggered manually from the Actions tab
  workflow_dispatch:

jobs:
  update-readme:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repository
        uses: actions/checkout@v2

      - name: Update README
        uses: anuraghazra/github-readme-stats@latest
        with:
          username: gblzera
          token: ${{ secrets.GITHUB_TOKEN }}
          template: markdown
          layout: compact

      - name: Commit and Push Changes
        run: |
          git config --global user.name "github-actions[bot]"
          git config --global user.email "41898282+github-actions[bot]@users.noreply.github.com"
          git add .
          git commit -m "Updated README with new languages"
          git push
