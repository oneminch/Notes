---
title: "EncryptedList"
description: A passion project I built to catalog secure-by-default tools
tags:
  - Vue
  - Airtable
  - VueX
  - Vue Router
live_url: "https://encryptedlist.xyz"
source_url: "https://github.com/oneminch/EncryptedList"
image: "https://raw.githubusercontent.com/oneminch/EncryptedList/main/public/screenshot.png"
icon: "https://raw.githubusercontent.com/oneminch/EncryptedList/main/public/logo.svg"
nav_order: 1
---

## What

EncryptedList is collection of software products & services that offer zero-knowledge or end-to-end encryption.

## Why

I'm interested in tools that are private and secure by design, so I wanted to build a full-stack website to catalog software services that are secure by default where people can search, filter, or submit new items.

## How

[The first version of the website](https://oneminch.github.io/EncryptedList-v1/) was static. I created a simple HTML & CSS page with a couple of dropdowns for filtering items. I used a flat JSON file to store the data and JavaScript to fetch the contents of this file to render them on the page. Managing data in a static JSON file was tedious, and this led to the development of the second version.

[The second (current) version of EncryptedList](https://encryptedlist.xyz/) is an SPA that uses Vue.js for the UI and Airtable for data. I used serverless functions on Vercel to connect the Airtable API and the UI. I also implemented features such as client-side search, filtering, and form submissions powered by GitHub Issues.

> Due to most logic being done on the client-side, the current version of the project has some performance issues. I plan to fix those issues in the next major version of the project by writing more semantic code, utilizing techniques such as SSR, and using less client-side JavaScript.

## Tech Stack

- **Frontend**: `Vue`, `Vue Router`, `VueX`
- **Backend**: `Airtable`, `Serverless Functions`
- **Deployment**: `Vercel`

## Status

This is my first major Vue project, and as of 2024, it receives thousands of regular visits.

I am currently developing the third version, and I plan to add new features such as pagination, optimized search and sorting, caching, and features suggested by users such as multi-tag filtering.
