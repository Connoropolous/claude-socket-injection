# Claude Code Notifications for Agents

A patch for `@anthropic-ai/claude-agent-sdk`'s `cli.js` that lets Claude Code sessions subscribe to external events and receive them as prompts.

## [View the diff](https://github.com/Connoropolous/claude-notifications-for-agents/compare/03d21f1..b8e03d0)

## What it does

Adds a socket server at `~/.claude/sockets/{sessionId}.sock` that accepts newline-delimited messages (JSON or plain text) and feeds them into the internal message queue. Messages are processed one at a time, sequentially.

## Usage

```bash
# Find the socket for a running session
SOCK=$(ls ~/.claude/sockets/*.sock 2>/dev/null | head -1)

# Send a prompt
echo '"Hello, list the files in the current directory"' | nc -U "$SOCK"

# Send structured JSON
echo '{"value":"What files are in /tmp?","mode":"prompt"}' | nc -U "$SOCK"
```
