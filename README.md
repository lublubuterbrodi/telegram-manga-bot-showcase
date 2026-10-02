# Telegram Catalog Bot & Mini App

![Node.js](https://img.shields.io/badge/Node.js-Production-339933?logo=node.js&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-5.x-3178C6?logo=typescript&logoColor=white)
![grammY](https://img.shields.io/badge/grammY-Telegram_Bot-26A5E4?logo=telegram&logoColor=white)
![React](https://img.shields.io/badge/React-Mini_App-61DAFB?logo=react&logoColor=black)
![SQLite](https://img.shields.io/badge/SQLite-Database-003B57?logo=sqlite&logoColor=white)
![Vercel](https://img.shields.io/badge/Vercel-Deployment-000000?logo=vercel&logoColor=white)
![PM2](https://img.shields.io/badge/PM2-Production-2B037A)
![VPS](https://img.shields.io/badge/VPS-Contabo-FF6B00)

A production Telegram-based content platform combining an automated **Telegram bot** with a **Telegram Mini App**.

The bot handles content ingestion, scheduled catalog publishing, support, and Telegram Stars payments, while the Mini App provides the main user-facing catalog experience.

The production application is actively deployed on a custom domain with HTTPS.

---

## Overview

The project originally worked entirely through a Telegram bot: users opened the bot, selected a title using inline buttons, and received content directly in private chat.

As the project evolved, the main user experience was moved to a **Telegram Mini App**.

The current flow is:

**Telegram Channel → Bot → Mini App → Web Interface**

Users now open the daily catalog through a Telegram link and browse the current selection inside the Mini App instead of interacting with multiple bot messages.

The bot remains responsible for backend automation, support, and Telegram Stars donations.

---

## How It Works

### 1. Content Ingestion

Content is uploaded to a private Telegram storage channel.

The bot automatically:

- creates new catalog entries;
- detects covers and content pages;
- stores Telegram file and message identifiers;
- preserves content ordering in SQLite.

Large media files remain stored in Telegram rather than being duplicated on the server.

### 2. Daily Publishing

A scheduled job generates the daily catalog selection and publishes it to the Telegram catalog channel.

Each publication contains a link that opens the Telegram Mini App.

### 3. Telegram Mini App

When the user follows the catalog link, Telegram opens the Mini App with the current daily selection.

The frontend retrieves catalog data from the bot/backend API and renders it as a web interface.

This replaces the previous workflow based on inline keyboards and content delivery through private bot messages.

### 4. Bot Interaction

The private bot chat is intentionally kept lightweight.

It is currently used for:

- user support;
- Telegram Stars donations;
- backend Telegram integration.

---

## Architecture

```text
Private Telegram Storage
        │
        ▼
Telegram Bot
Node.js + TypeScript + grammY
        │
        ├── Content ingestion
        ├── Scheduled publishing
        ├── SQLite storage
        ├── Reader API
        ├── Support
        └── Telegram Stars
        │
        ▼
Telegram Mini App
React + TypeScript
        │
        ▼
Custom Domain
Vercel + HTTPS
```

---

## Tech Stack

### Bot / Backend

- Node.js
- TypeScript
- grammY
- Telegram Bot API
- SQLite
- better-sqlite3
- node-cron

### Mini App

- React
- TypeScript
- Telegram Mini Apps API
- CSS

### Infrastructure

- Contabo VPS
- Ubuntu
- PM2
- Vercel
- Custom domain
- HTTPS with managed SSL/TLS certificates

---

## Project Structure

### Bot

```text
src/
├── db.ts
├── handlers.ts
├── index.ts
├── manga.ts
├── readerApi.ts
├── support.ts
└── utils.ts
```

### Mini App

```text
src/
├── App.css
├── App.tsx
├── index.css
├── main.tsx
└── telegram.d.ts
```

---

## Deployment

The Telegram bot runs continuously on a **Contabo VPS** using PM2.

The Mini App is deployed independently through **Vercel** and connected to its own custom domain.

Vercel provides HTTPS for the production domain with automatically managed SSL/TLS certificates.

This separates the Telegram automation layer from the web interface and allows both parts of the project to be deployed and updated independently.

---

## Technical Highlights

- Telegram Bot + Mini App architecture
- React-based Telegram web interface
- Custom production domain
- HTTPS / managed TLS
- Telegram-based media storage
- Persistent SQLite database
- Automated daily catalog publishing
- Backend API for Mini App data
- Telegram Stars integration
- Production VPS deployment
- Independent frontend deployment through Vercel

---

## Privacy

This repository is a technical showcase of the project architecture.

Production content, private Telegram channels, bot tokens, user data, payment information, and other sensitive configuration are not included.
