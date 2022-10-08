---
title:  "Github Action Tricks"
excerpt: ""
tags: "gh-pages, github pages, github, gh-actions, github actions"
---

## Checking out Multiple Repos

You can check out multiple repos in your action, this is useful when you want to have something like content in one repository and templates in another repository.

In the `jobs` section of the actional yaml you use the Github action `actions/checkout@v#` (where `#` is the version number), you can check out multiple repos, they will be processed in the order they're written:

```yaml

jobs:
  # Build job
  build:
    runs-on: ubuntu-latest
    env:
      working-directory: ./
    steps:
        # 1. Checkout a different repo:
      - name: Checkout queue-bit/go-pubsite
        uses: actions/checkout@v3
        with:
          repository: queue-bit/go-pubsite
          path: './'
        # 2. Checkout the current repo:
      - name: Checkout repo
        uses: actions/checkout@v3
        with:
          path: './content'

```