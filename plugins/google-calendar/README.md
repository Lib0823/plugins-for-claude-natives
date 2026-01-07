# Google Calendar Plugin

Multi-account Google Calendar integration with parallel querying and conflict detection.

## Features

- Query multiple Google accounts (work, personal) in parallel
- Detect scheduling conflicts between calendars
- Create, update, and delete events
- OAuth2 authentication with stored refresh tokens

## Installation

```bash
/plugin install google-calendar
```

## Prerequisites

### 1. Google Cloud Project Setup

1. Create a project at [Google Cloud Console](https://console.cloud.google.com)
2. Enable Calendar API
3. Create OAuth 2.0 Client ID (Desktop type)
4. Download `credentials.json`

### 2. Account Authentication (one-time)

```bash
# Work account
uv run python scripts/setup_auth.py --account work

# Personal account
uv run python scripts/setup_auth.py --account personal
```

## Usage

Ask Claude about your calendar:

- "오늘 일정 알려줘"
- "이번 주 일정 충돌 확인해줘"
- "내일 3시에 팀 미팅 추가해줘"
- "What's on my calendar today?"
- "Schedule a meeting for tomorrow at 2pm"

## License

MIT
