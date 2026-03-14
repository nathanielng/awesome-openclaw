# Obsidian CLI Help

> Source: [https://help.obsidian.md/cli](https://help.obsidian.md/cli)

The Obsidian CLI is a command-line interface built into the Obsidian app that lets you control Obsidian from your terminal. It is useful for scripting, automation, and integration with external tools.

## Requirements

- Obsidian 1.12 or above (currently Early Access, requires a Catalyst license)
- Obsidian must be running (the first command you execute will launch it automatically if it is not)
- Desktop only — no iOS or Android support

## Setup

1. Open Obsidian and go to **Settings → General**
2. Enable **Command Line Interface**
3. Follow the on-screen prompt to register the CLI and add it to your system PATH
4. Restart your terminal for changes to take effect

## Usage

```
obsidian [command] [parameters]
```

Run without arguments to enter the interactive **Terminal User Interface (TUI)**, which provides autocomplete, command history, and reverse search (`Ctrl+R`).

## Parameter Syntax

| Pattern | Description |
|---|---|
| `key=value` | Key-value parameter |
| `flag` | Boolean switch (no value needed) |
| `format=json\|csv\|tsv\|md\|paths` | Output format (default: `json`) |

---

## Commands

### Notes

| Command | Description |
|---|---|
| `obsidian read` | Read the current file |
| `obsidian create name="<name>" template=<template>` | Create a new note, optionally from a template |
| `obsidian move file="<path>" to="<destination>"` | Move a note and automatically update all wikilinks |
| `obsidian delete file="<name>"` | Move a note to trash |
| `obsidian delete file="<name>" permanent` | Permanently delete a note (bypasses trash) |

### Search

| Command | Description |
|---|---|
| `obsidian search query="<terms>"` | Search the vault |
| `obsidian unresolved` | List links whose targets do not exist |
| `obsidian orphans` | List notes that nothing links to |

### Links

| Command | Description |
|---|---|
| `obsidian links file="<name>"` | Show outgoing links from a note |
| `obsidian backlinks file="<name>"` | Show notes that link to a note |

### Properties (Frontmatter)

| Command | Description |
|---|---|
| `obsidian properties file="<name>"` | View all frontmatter properties of a note |
| `obsidian property:set file="<name>" name="<key>" value="<val>"` | Set a frontmatter property |
| `obsidian property:remove file="<name>" name="<key>"` | Remove a frontmatter property |

### Tags

| Command | Description |
|---|---|
| `obsidian tags counts` | List all tags with their frequency |

### Tasks

| Command | Description |
|---|---|
| `obsidian tasks daily` | List all tasks from today's daily note |

### Daily Notes

| Command | Description |
|---|---|
| `obsidian daily` | Open today's daily note |
| `obsidian daily:append content="<text>"` | Append content to today's daily note |
| `obsidian daily:read` | Display the contents of today's daily note |
| `obsidian daily:path` | Print the file path of today's daily note |

### Bookmarks

| Parameter | Description |
|---|---|
| `file=<path>` | Bookmark a file |
| `folder=<path>` | Bookmark a folder |
| `search=<query>` | Bookmark a search query |
| `url=<url>` | Bookmark a URL |
| `title=<title>` | Set a bookmark title |
| `subpath=<subpath>` | Bookmark a specific section within a file |
| `total` | Return bookmark count |
| `verbose` | Include bookmark types in output |
| `format=json\|tsv\|csv` | Output format |

### Commands & Hotkeys

| Parameter | Description |
|---|---|
| `id=<command-id>` | Execute a specific Obsidian command by its ID (required) |

### Diff

```
obsidian diff file=<name> from=<version> to=<version>
```

Compare two versions of a file.

### Developer Commands

| Command | Description |
|---|---|
| `obsidian devtools` | Open the developer tools panel |
| `obsidian plugin:reload <plugin-id>` | Reload a plugin (useful during development) |
| `obsidian dev:screenshot file=<path>` | Capture a screenshot of the app |
| `obsidian eval "<js>"` | Execute JavaScript in the Obsidian context |
| `obsidian dev:errors` | Review JavaScript errors |
| `obsidian dev:css selector="<selector>"` | Inspect CSS properties for a selector |
| `obsidian dev:dom selector="<selector>"` | Query DOM elements by selector |

---

## Examples

```bash
# Open today's daily note
obsidian daily

# Append a task to today's daily note
obsidian daily:append content="- [ ] Review meeting notes"

# Search the vault
obsidian search query="project ideas"

# Create a new note from a template
obsidian create name="Trip to Paris" template=Travel

# Move a note and update all links
obsidian move file="Inbox/note" to="Archive/"

# Set a frontmatter property
obsidian property:set file="note" name="status" value="draft"

# View all tags and their frequency
obsidian tags counts

# Find orphan notes
obsidian orphans

# Execute JavaScript to count files
obsidian eval "app.vault.getFiles().length"

# Reload a plugin during development
obsidian plugin:reload my-plugin
```

---

## Multi-Vault Usage

When working with multiple vaults, specify the target vault with:

```bash
obsidian <command> vault="<VaultName>"
```

---

## Limitations

- **Not headless**: the CLI controls the running Obsidian GUI — it launches Obsidian automatically on first use, but requires startup time.
- **Desktop only**: no support for iOS or Android.
- **Early Access**: commands and syntax may change before general availability.

---

## Output Formats

Most listing commands support the `format` parameter:

| Value | Description |
|---|---|
| `json` | JSON (default) |
| `csv` | Comma-separated values |
| `tsv` | Tab-separated values |
| `md` | Markdown |
| `paths` | File paths only |
