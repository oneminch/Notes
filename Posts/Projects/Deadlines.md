---
title: Deadlines
description: An offline deadline tracker I built to track school deadlines
tags:
  - Vue.js
  - localForage
live_url: "https://deadlines.oneminch.dev"
source_url: "https://github.com/oneminch/Deadlines"
image: "https://raw.githubusercontent.com/oneminch/Deadlines/main/public/screenshot.png"
icon: "https://raw.githubusercontent.com/oneminch/Deadlines/main/public/logo.svg"
nav_order: 5
---

## What

Deadlines is an offline deadline tracker I built to track school deadlines.

## Why

I built Deadlines primarily to solidify my knowledge of Vue.js as I was learning it at the time, and I had the need for a simple way to track assignment and project deadlines in college.

## How

I used Vue for the UI and localForage to store data. As it is a local (offline) web app, all data is stored in the browser. localForage provides a simple wrapper around browser storage APIs, so this allowed consistent cross-browser storage. Data can be imported from and exported to a JSON file. It also has dark mode.

## Tech Stack

- **Frontend**: `Vue`
- **Data**: `localForage`
- **Deployment**: `Cloudflare Pages`
