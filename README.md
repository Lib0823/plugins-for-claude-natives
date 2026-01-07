# Plugins for Claude Natives

A collection of Claude Code plugins for power users who want to extend Claude Code's capabilities beyond the defaults.

## Table of Contents

- [Quick Start](#quick-start)
- [Available Plugins](#available-plugins)
- [Plugin Details](#plugin-details)
  - [agent-council](#agent-council) - Get consensus from multiple AI models
  - [clarify](#clarify) - Transform vague requirements into specs
  - [dev](#dev) - Scan developer communities for opinions
  - [interactive-review](#interactive-review) - Review plans with a web UI
  - [say-summary](#say-summary) - Hear responses via text-to-speech
  - [youtube-digest](#youtube-digest) - Summarize and quiz on YouTube videos
  - [google-calendar](#google-calendar) - Multi-account calendar integration
- [Contributing](#contributing)
- [License](#license)

---

## Quick Start

```bash
# Add this marketplace to Claude Code
/plugin marketplace add team-attention/plugins-for-claude-natives

# Install any plugin
/plugin install <plugin-name>
```

---

## Available Plugins

| Plugin | Description | Social |
|--------|-------------|--------|
| [agent-council](./plugins/agent-council/) | Collect and synthesize opinions from multiple AI agents (Gemini, GPT, Codex) | [LinkedIn](https://www.linkedin.com/posts/gb-jeong_claude-code%EA%B0%80-codex-gemini-cli-%EA%B3%BC-%ED%9A%8C%EC%9D%98%ED%95%B4%EC%84%9C-%EA%B2%B0%EB%A1%A0%EC%9D%84-activity-7406083077258665984-L_fD) |
| [clarify](./plugins/clarify/) | Transform vague requirements into precise specifications through iterative questioning | [LinkedIn](https://www.linkedin.com/posts/gb-jeong_%ED%81%B4%EB%A1%9C%EB%93%9C%EC%BD%94%EB%93%9C%EA%B0%80-%EA%B0%9D%EA%B4%80%EC%8B%9D%EC%9C%BC%EB%A1%9C-%EC%A7%88%EB%AC%B8%ED%95%98%EA%B2%8C-%ED%95%98%EB%8A%94-skills%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%B4%EB%B3%B4%EC%84%B8%EC%9A%94-clarify-activity-7413349697022570496-qLts) |
| [dev](./plugins/dev/) | Fetch developer opinions from Reddit, Hacker News, Dev.to, and Lobsters | |
| [interactive-review](./plugins/interactive-review/) | Interactive markdown review with web UI for visual plan/document approval | [LinkedIn](https://www.linkedin.com/posts/hoyeonleekr_claude-code%EA%B0%80-%EC%9E%91%EC%84%B1%ED%95%9C-%EA%B3%84%ED%9A%8D%EC%9D%B4%EB%82%98-%EA%B8%B4-%EB%AC%B8%EC%84%9C%EC%97%90-%EB%8C%80%ED%95%9C-%EC%96%B4%EB%96%BB%EA%B2%8C-%ED%94%BC%EB%93%9C%EB%B0%B1-%EC%A3%BC%EC%84%B8%EC%9A%94-activity-7412613598516051968-ujHp) |
| [say-summary](./plugins/say-summary/) | Speaks a short summary of Claude's response using macOS TTS (Korean/English) | [LinkedIn](https://www.linkedin.com/posts/gb-jeong_claude-code%EC%9D%98-%EC%9D%91%EB%8B%B5%EC%9D%84-%EC%9A%94%EC%95%BD%ED%95%B4%EC%84%9C-%EC%9D%8C%EC%84%B1%EC%9C%BC%EB%A1%9C-%EB%93%A4%EC%9D%84-%EC%88%98-%EC%9E%88%EB%8A%94-hooks-activity-7412609821390249984-ekCd) |
| [youtube-digest](./plugins/youtube-digest/) | Summarize YouTube videos with transcript, insights, Korean translation, and quizzes | [LinkedIn](https://www.linkedin.com/posts/gb-jeong_84%EB%B6%84%EC%A7%9C%EB%A6%AC-%EC%98%81%EC%96%B4-%ED%8C%9F%EC%BA%90%EC%8A%A4%ED%8A%B8%EB%A5%BC-5%EB%B6%84-%EB%A7%8C%EC%97%90-%ED%95%B5%EC%8B%AC-%ED%8C%8C%EC%95%85%ED%95%98%EA%B3%A0-%ED%80%B4%EC%A6%88%EA%B9%8C%EC%A7%80-%ED%92%80%EA%B3%A0-%EC%A7%81%EC%A0%91-activity-7414055598754848768-c0oy) |
| [google-calendar](./plugins/google-calendar/) | Multi-account Google Calendar integration with parallel querying and conflict detection | |

---

## Plugin Details

### agent-council

![Demo](./assets/agent-council.gif)

**Summon multiple AI models to debate your question and reach a consensus.**

When you're facing a tough decision or want diverse perspectives, this plugin queries multiple AI agents (Gemini CLI, GPT, Codex) in parallel and synthesizes their opinions into a single, balanced answer.

**Trigger phrases:**
- "summon the council"
- "ask other AIs"
- "what do other models think?"

**How it works:**
1. Your question is sent to multiple AI agents simultaneously
2. Each agent provides its perspective
3. Claude synthesizes the responses into a consensus view with noted disagreements

```bash
# Example
User: "summon the council - should I use TypeScript or JavaScript for my new project?"
```

---

### clarify

![Demo](./assets/clarify.gif)

**Turn vague requirements into precise, actionable specifications.**

Before writing code based on ambiguous instructions, this plugin conducts a structured interview to extract exactly what you need. No more assumptions, no more rework.

**Trigger phrases:**
- "/clarify"
- "clarify requirements"
- "what do I mean by..."

**The process:**
1. **Capture** - Record the original requirement verbatim
2. **Question** - Ask targeted multiple-choice questions to resolve ambiguities
3. **Compare** - Present before/after showing the transformation
4. **Save** - Optionally save the clarified spec to a file

**Example transformation:**

| Before | After |
|--------|-------|
| "Add a login feature" | Goal: Add username/password login with self-registration. Scope: Login, logout, registration, password reset. Constraints: 24h session, bcrypt, rate limit 5 attempts. |

---

### dev

**Scan developer communities for real opinions on any tech topic.**

Want to know what developers actually think about a framework, tool, or practice? This plugin searches Reddit, Hacker News, Dev.to, and Lobsters in parallel to gather diverse perspectives.

**Trigger phrases:**
- "developer reactions to..."
- "what do devs think about..."
- "community opinions on..."

**Output includes:**
- **Consensus** - Points mentioned across multiple sources
- **Controversy** - Where opinions diverge
- **Notable perspectives** - Unique insights from experienced devs
- **Platform temperature** - Overall sentiment by community

```bash
# Example
User: "What do developers think about React 19?"
```

---

### interactive-review

**Review Claude's plans and documents through a visual web interface.**

Instead of reading long markdown in the terminal, this plugin opens a browser-based UI where you can check/uncheck items, add comments, and submit structured feedback.

**Trigger phrases:**
- "/review"
- "review this plan"
- "let me check this"

**The flow:**
1. Claude generates a plan or document
2. A web UI opens automatically in your browser
3. Review each item with checkboxes and optional comments
4. Click Submit to send structured feedback back to Claude
5. Claude adjusts based on your approved/rejected items

---

### say-summary

![Demo](./assets/say-summary.gif)

**Hear Claude's responses spoken aloud (macOS only).**

This plugin uses a Stop hook to summarize Claude's response to a short headline and speaks it using macOS text-to-speech. Perfect for when you're coding and want audio feedback.

**Features:**
- Summarizes responses to 3-10 words using Claude Haiku
- Auto-detects Korean vs English
- Uses appropriate voice (Yuna for Korean, Samantha for English)
- Runs in background, doesn't block Claude Code

**Requirements:**
- macOS (uses the `say` command)
- Python 3.10+

---

### youtube-digest

![Demo](./assets/youtube-digest.jpeg)

**Summarize YouTube videos with transcripts, translations, and comprehension quizzes.**

Drop a YouTube URL and get a complete breakdown: summary, key insights, full Korean translation of the transcript, and a 3-stage quiz (9 questions total) to test your understanding.

**Trigger phrases:**
- "summarize this YouTube"
- "digest this video"
- YouTube URL

**What you get:**
1. **Summary** - 3-5 sentence overview with key points
2. **Insights** - Actionable takeaways and ideas
3. **Full transcript** - With Korean translation and timestamps
4. **3-stage quiz** - Basic, intermediate, and advanced questions
5. **Deep Research** (optional) - Web search to expand on the topic

**Output location:** `research/readings/youtube/YYYY-MM-DD-title.md`

---

### google-calendar

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/a5/Google_Calendar_icon_%282020%29.svg/960px-Google_Calendar_icon_%282020%29.svg.png" width="120" alt="Google Calendar">

**Manage multiple Google Calendar accounts from Claude Code.**

Query, create, update, and delete events across multiple Google accounts (work, personal, etc.) with automatic conflict detection.

**Trigger phrases:**
- "show my schedule"
- "what's on my calendar"
- "create a meeting"
- "check for conflicts"

**Features:**
- Parallel querying across multiple accounts
- Conflict detection between accounts
- Full CRUD operations (create, read, update, delete)
- Pre-authenticated with refresh tokens (no repeated logins)

**Setup required:**
1. Create Google Cloud project with Calendar API
2. Run setup script for each account

```bash
# One-time setup per account
uv run python scripts/setup_auth.py --account work
uv run python scripts/setup_auth.py --account personal
```

---

## Contributing

Contributions welcome! Please open an issue or PR.

## License

MIT
