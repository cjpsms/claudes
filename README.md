# claudes

Terminal command that prints how much of your Claude **5-hour session limit**
and **weekly limit** you've used.

## How it works

It reuses the OAuth session Claude Code already has logged in
(`~/.claude/.credentials.json`) — no separate API key needed. It makes the
cheapest possible request (a 1-output-token Haiku call) and reads the
`anthropic-ratelimit-unified-5h-*` / `-7d-*` headers Anthropic returns on every
Messages API response. If that's rejected, it falls back to the OAuth usage
endpoint that backs Claude Code's own `/usage` command.

## Usage

```
claudes
```

Prints something like:

```
5-hour session:  42% used   resets 2026-06-07 14:00
Weekly limit:    18% used   resets 2026-06-12 00:00
```

If your Claude Code session has expired, it'll tell you to run `claude` to
log back in.

## Files

- `claudes` — the script (symlinked into `~/.local/bin/claudes`, which is on PATH)
