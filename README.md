# KlarText

KlarText turns dense German or English text into easier-to-understand language and can read it aloud. It is built to make written information more accessible for people who struggle with complex text.

> **Important:** KlarText produces plain-language / easy-language simplifications. It is **not** certified *Leichte Sprache* and does not guarantee legal, medical, or official accuracy.

## Introduction

KlarText is an accessibility-focused product designed for people who face barriers when reading complex text. This includes people with:

- reading or cognitive difficulties
- dyslexia
- lower literacy
- non-native language backgrounds
- seniors
- anyone who needs clearer, simpler wording

The system takes dense bureaucratic, legal, medical, or technical text and transforms it into easier language while aiming to preserve the original meaning.

## Product Overview

KlarText is currently being developed as a small product ecosystem:

### KlarText Web App
A web-based interface for simplifying text and listening to it through text-to-speech.

### KlarText Extension
A browser extension that brings simplification directly into the reading experience by helping users simplify selected text or website content in place.

### KlarText Feedback Loop
An internal evaluation and learning workflow used to review output quality, compare runs, and improve prompts, rules, and system behavior over time.

## Architecture

KlarText is built as a multi-interface product around a shared API layer.

```text
┌──────────────────────────────────────────────────────────────────┐
│                         Interfaces                               │
│  ┌──────────────┐    ┌──────────────┐    ┌──────────────┐        │
│  │   Web App    │    │   Demo UI    │    │  Extension   │        │
│  │  (Frontend)  │    │ (Prototype)  │    │  (Browser)   │        │
│  └──────┬───────┘    └──────┬───────┘    └──────┬───────┘        │
└─────────┼───────────────────┼───────────────────┼────────────────┘
          │                   │                   │
          └───────────────────┼───────────────────┘
                              │
                              ▼
┌──────────────────────────────────────────────────────────────────┐
│                      Backend API Layer                           │
│                         (FastAPI)                                │
│                                                                  │
│   Simplification  │  PDF ingestion  │  TTS  │  Logging / eval    │
└──────────────────────────────────────────────────────────────────┘
                              │
          ┌───────────────────┼───────────────────┐
          ▼                   ▼                   ▼
    ┌───────────┐       ┌───────────┐       ┌───────────┐
    │   LLM     │       │ PDF/text  │       │    TTS    │
    │ provider  │       │ processing│       │  service  │
    └───────────┘       └───────────┘       └───────────┘
                              │
                              ▼
                   ┌─────────────────────┐
                   │ Evaluation / review │
                   │ and feedback loop   │
                   └─────────────────────┘
```

## How It Was Built

KlarText was built as an accessibility-first application with a modular architecture so different interfaces can use the same simplification services.

At a high level, the system includes:

- a frontend web application for direct user interaction
- a backend API for simplification, ingestion, and text-to-speech
- a browser extension for in-context website simplification
- an internal feedback loop for quality review and iterative improvement

The architecture is designed to support experimentation, evaluation, and future product expansion without tightly coupling every interface to separate logic.

## Tech Stack

| Layer | Technology |
|------|------------|
| Frontend | React, TypeScript, Vite, Tailwind CSS |
| Backend API | Python, FastAPI, Uvicorn |
| Simplification Pipeline | LLM-based prompting and rule-guided transformations |
| PDF Processing | PyMuPDF and text-cleanup pipeline |
| Text-to-Speech | gTTS and optional alternate TTS providers |
| Evaluation | JSONL logging, quality review workflows, internal metrics |
| Deployment | Vercel (frontend), Fly.io (backend) |

## API Overview

The KlarText architecture is centered around a backend API that supports:

- text simplification
- PDF ingestion
- URL-based content ingestion
- text-to-speech
- internal logging and review workflows

Core endpoints include:

- `POST /v1/simplify`
- `POST /v1/simplify/batch`
- `POST /v1/ingest/pdf`
- `POST /v1/ingest/url`
- `POST /v1/tts`
- `POST /v1/log-run`
- `GET /healthz`

Public demo users interact with KlarText through the product interfaces rather than through direct source access in this repository.

## Current Focus

KlarText is currently focused on:

- improving plain-language simplification quality
- preserving meaning while reducing complexity
- improving browser-extension usability
- strengthening internal evaluation workflows
- making accessibility-focused reading support easier to access

## In Development

Planned and in-progress capabilities include:

- translation rating and quality review
- highlighted-word clarification for translated or simplified text
- continued browser extension improvements
- stronger internal feedback and evaluation workflows
- additional quality and readability analysis features

## Demo and Documentation

This repository exists as the public-facing project overview for KlarText.

Here you will find:

- product information
- architecture summaries
- public documentation
- demo access information
- high-level development updates

## Live Demo

You can acess the Webapp [here](https://klartext-rho.vercel.app/)

Access to the extension through the google store tbd

## Additional Documentation

Add public links here, such as:

- Product overview
- Architecture notes
- Extension overview
- Feedback loop overview
- Roadmap or development updates

Example:

- [Product Overview](./docs/product-overview.md)
- [Architecture Notes](./docs/architecture.md)
- [Extension Overview](./docs/extension.md)
- [Feedback Loop Overview](./docs/feedback-loop.md)

## Why KlarText Exists

A lot of important information is still written in ways that are too difficult for many people to use. Bureaucratic, legal, medical, and technical language often create unnecessary barriers.

KlarText is being built to reduce that gap by making information clearer, easier to access, and easier to understand.

## Repository Purpose

This is the public showcase repository for KlarText.

It is intended to provide:

- product context
- architecture and design overview
- demo access
- public-facing documentation

The full implementation repository is kept separate.
