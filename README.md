# Blog

A simple Jekyll blog hosted on GitHub Pages.

## Creating New Posts

Create new markdown files in `_posts/` with the format: `YYYY-MM-DD-title.md`

Front matter example:
```yaml
---
layout: post
title: "Your Post Title"
date: 2026-02-17 10:00:00 +0000
categories: your-category
tags: [tag1, tag2]
---
```

## Local Development

Install dependencies:
```bash
gem install bundler
bundle install
```

Run locally:
```bash
bundle exec jekyll serve
```

Visit: http://localhost:4000