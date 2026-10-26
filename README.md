# TrendScope India — starter project

A first working Streamlit prototype for daily trend discovery in India.

## What works in v0.1
- Google trending searches via the community `pytrends` client (unofficial; may break).
- YouTube popular videos in India via the official YouTube Data API.
- Daily in-app caching (24 hours) and manual refresh.
- CSV export.
- Facebook and Instagram integration status/help panels without fabricated data.

## What it does not claim
- It does not return exact Google search volume.
- YouTube popular videos are not the same as YouTube search queries.
- It does not scrape private content or claim access to all Facebook/Instagram searches.
- Facebook/Instagram connectors need eligible accounts, app setup, permissions, and review where applicable.

## Windows setup
1. Install Python 3.10 or newer from https://www.python.org/downloads/
2. Extract this ZIP to a folder, for example `D:\TrendScope`.
3. Open Command Prompt in that folder.
4. Create a virtual environment:
   `python -m venv .venv`
5. Activate it:
   `.venv\Scripts\activate`
6. Install dependencies:
   `python -m pip install -r requirements.txt`
7. Start the dashboard:
   `python -m streamlit run app.py`
8. Streamlit will show a local URL, usually `http://localhost:8501`.

## YouTube API key (recommended)
1. Open https://console.cloud.google.com/
2. Create/select a Google Cloud project.
3. Enable **YouTube Data API v3**.
4. Create an API key under APIs & Services > Credentials.
5. Restrict the key to YouTube Data API v3 where possible.
6. Paste it into the dashboard sidebar when running locally.

Optional environment variable:
- Copy `.env.example` to `.env` for your own reference, but this starter does not automatically load `.env`.
- Or set it in Command Prompt before running:
  `set YOUTUBE_API_KEY=YOUR_KEY_HERE`

Do not publish the API key or commit it to GitHub.

## Daily automation
The dashboard caches provider data for 24 hours while the app is running. To save a daily snapshot even when nobody opens the dashboard, the next version should add a scheduled job (Windows Task Scheduler) that runs a separate collector and appends results to SQLite/CSV. This starter does not yet run a background scheduler.

## Architecture
Browser -> Streamlit dashboard -> provider collectors -> normalized pandas tables -> CSV export.
Next phase: scheduled collector -> SQLite history -> 7-day growth score -> cross-platform topic matching.
