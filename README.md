# Credit Risk Scorecard

A Google Apps Script web application that enables risk teams to submit structured risk cases via a guided intake form and score each case automatically using a configurable weighted model — with no API keys, no external services, and no redeployment needed when tuning weights.

---

## Overview

This tool was built to standardize how risk cases are captured and evaluated. Instead of ad-hoc spreadsheet reviews, analysts fill out a simple web form, and the system instantly calculates a deterministic risk score based on configurable weighted factors. An AI-generated explanation (via Google Sheets' built-in Gemini integration) summarizes the top contributing factors in plain language.

---
## Important Links
- [Live Application](https://script.google.com/macros/s/AKfycbxysrw_zPZ6DDyLuyZG1qS8kJaCniSUtwB897hbMzSqXnPAlJfXKroigxasChiVXP7mIw/exec)
- [Database](https://docs.google.com/spreadsheets/d/11s1Maz8KyQUP8Id_axBDzl1YGPy3oZYhpQ_tWdIGM8U/edit?gid=0#gid=0)
---
## Features

- **Structured intake form** — guided web form for submitting risk cases consistently
- **Weighted scoring model** — six configurable factors produce a deterministic score
- **AI-generated explanations** — uses Google Sheets' native `AI()` function (Gemini-powered); falls back to a deterministic explanation if unavailable
- **Live dashboard** — trend charts and geographic breakdowns update automatically
- **Zero API keys required** — all processing runs within Google Workspace
- **Hot-reloadable weights** — update the scoring model in the sheet; changes take effect immediately without redeployment
- **Public URL access** — deployed app works in any browser, no login required for end users

---

## Scoring Model

| Factor | Weight |
|---|---|
| Alert Type | 25% |
| Geography | 25% |
| Transaction Size | 20% |
| Customer Segment | 10% |
| Urgency | 10% |
| Prior Incidents | 10% |

Weights are stored in the `ScoringWeights` sheet and can be updated at any time without touching code.

---

## Architecture

| Component | Role |
|---|---|
| Google Apps Script | Backend logic, form handling, scoring engine |
| Google Sheets | Data storage and weight configuration |
| Sheets `AI()` function | Gemini-powered explanation generation |
| Web App deployment | Frontend served directly from Apps Script |

**Core sheets:**
- `Cases` — all submitted risk cases and scores
- `ScoringWeights` — factor weights (editable)
- `Lookup_Countries` — geographic reference data

---

## Setup

### 1. Copy the source sheet

Make a copy of the Google Sheet that contains the Apps Script project.

### 2. Initialize sheets

Open **Extensions → Apps Script**, then run the `initializeSheets()` function once. This creates the required sheet structure if it doesn't already exist.

### 3. Deploy as a web app

1. In Apps Script, click **Deploy → New deployment**
2. Select type: **Web app**
3. Set **Execute as**: Me
4. Set **Who has access**: Anyone
5. Click **Deploy** and copy the web app URL

### 4. Share the URL

Paste the deployed URL into your browser or share it with your team. No additional authentication or configuration is needed.

---

## Customizing Weights

Open the `ScoringWeights` sheet and update any factor's weight value. Changes are reflected immediately the next time a case is scored — no redeployment required.

> Weights should sum to 100%. The scoring engine reads them at runtime.

---

## Built With

- [Google Apps Script](https://developers.google.com/apps-script)
- [Google Sheets](https://workspace.google.com/products/sheets/) (including the native `AI()` / Gemini function)

---

## Author

Built by **Fernando Pereira** using Claude and Google Apps Script + Sheets AI().
