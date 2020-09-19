+++
date = "2020-09-19"
title = "Hugo CMS hosten op Github pages"
slug = "hugo-cms-hosten-op-github-pages" 
tags = ["hugo"]
categories = []
series = ["CMS", "Hugo", "Hosting"]

+++

## Introduction



```shell
.github/workflows/main.yaml
```



```yaml
name: Publish to Github Pages

on:
  push:
    branches: [ master ]
  pull_request:
    branches: [ master ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2
        with:
          submodules: true  # Fetch Hugo themes (true OR recursive)
          fetch-depth: 0    # Fetch all history for .GitInfo and .Lastmod

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: '0.75.1'
          extended: true

      - name: Build
        run: hugo --minify

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public

```

