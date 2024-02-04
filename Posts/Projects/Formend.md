---
title: Formend
description: A backend I built to help me handle form submissions
tags:
  - Flask
  - Python
  - Postgres
live_url: "https://formend.oneminch.dev"
source_url: "https://github.com/oneminch/Formend"
image: "https://raw.githubusercontent.com/oneminch/Formend/main/public/screenshot.png"
icon: "https://raw.githubusercontent.com/oneminch/Formend/main/public/logo.svg"
nav_order: 3
---

## What

Formend is a backend I built to manage form submissions.

## Why

I have used several form endpoint tools to handle form submissions for my portfolio and side-projects. Even though these tools are convenient to set up and use, they are not customizable to developer needs. I built Formend to meet such needs.

## How

I used Flask serverless functions as a backend framework and Postgres as a database. A form submission to any allowed endpoint on Formend is stored to a database table dynamically created for that endpoint. After the form data is stored, an email notification with the form body is sent to a pre-configured address. The project is powered by the Vercel platform.

## Tech Stack

- **Framework**: `Flask (Python)`
- **Database**: `PostgreSQL`
- **Deployment**: `Vercel`
