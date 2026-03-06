# CLI Tool & Standalone Scripts

figranium can be run entirely from the command line, either interactively or for automated scripting.

## Global Installation

```bash
npm install -g @figraniumdev/figranium
```

## Commands

### Start Server

Run the standard figranium server (API + UI).

```bash
figranium
# or
npx @figraniumdev/figranium
```

### Modes

#### Scraper Mode (`--scrape`)

Runs a high-performance scraping task without the full agent logic. Ideal for simple data extraction.

```bash
figranium --scrape --url "https://example.com" --selector ".content"
```

- `--url`: Target URL.
- `--selector`: CSS selector to extract text from.
- `--output`: (Optional) File to save the result.

#### Headful Execution (`--headful`)

Launches a visible browser session for debugging.

```bash
figranium --headful --url "https://example.com"
```

#### Agent Mode (`--agent`)

Executes a saved task by ID or a JSON definition file.

```bash
figranium --agent --task "task_id_or_file.json"
```

## Environment Variables

CLI commands respect the same environment variables as the server:

- `PORT`: Server port.
- `SESSION_SECRET`: Session encryption key.
- `HEADLESS`: Set to `false` to see the browser window (if running locally without Docker).

## Scripting

You can pipe JSON into figranium for complex workflows:

```bash
echo '{"url": "https://example.com", "actions": [{"type": "screenshot"}]}' | figranium --agent
```
