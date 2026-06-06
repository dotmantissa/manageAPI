# manageAPI

A small shell script that manages multiple Claude API keys. When you hit a rate limit, instead of waiting it out, you run the script and it finds a working key and swaps it into your Claude config automatically.

## How it works

The script keeps a list of your API keys in `~/.claude/api_keys.txt`. When you run it with no arguments, it tests each key against the API one by one until it finds one that is not rate limited, then writes that key into `~/.claude/settings.json`. Both places the key appears in that file get updated at the same time.

If `settings.json` does not exist yet, the script creates it with the right structure before writing the key in.

## Setup

Copy the script somewhere on your PATH, for example `~/.local/bin/manageAPI`, and make it executable:

```bash
chmod +x manageAPI
cp manageAPI ~/.local/bin/manageAPI
```

Then add your first key:

```bash
manageAPI --add your_api_key_here
```

That is all the setup required. The key file and settings file are created for you if they do not already exist.

## Usage

**Find and activate a working key:**
```bash
manageAPI
```

Scans through your stored keys, tests each one, and switches to the first that is not rate limited. If all keys are rate limited it exits with an error.

**Add a new key:**
```bash
manageAPI --add your_api_key_here
# or
manageAPI -ad your_api_key_here
```

Appends the key to `~/.claude/api_keys.txt`. Duplicate keys are silently ignored.

**See all configured keys:**
```bash
manageAPI --list
# or
manageAPI -l
```

Prints every key in your list and marks which one is currently active in your settings.

**Help:**
```bash
manageAPI --help
```

## Files

| Path | Purpose |
|------|---------|
| `~/.claude/api_keys.txt` | Your stored API keys, one per line |
| `~/.claude/settings.json` | Claude Code settings where the active key lives |
