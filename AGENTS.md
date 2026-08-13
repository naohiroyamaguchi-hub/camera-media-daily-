name: Daily Camera Media News

on:
  schedule:
    - cron: "0 23 * * *"
  workflow_dispatch:

jobs:
  run:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - uses: actions/setup-python@v5
        with:
          python-version: "3.12"

      - run: pip install -r requirements.txt

      - run: python -m src.main
        env:
          OPENAI_API_KEY: ${{ secrets.OPENAI_API_KEY }}
          MS_TENANT_ID: ${{ secrets.MS_TENANT_ID }}
          MS_CLIENT_ID: ${{ secrets.MS_CLIENT_ID }}
          MS_CLIENT_SECRET: ${{ secrets.MS_CLIENT_SECRET }}
