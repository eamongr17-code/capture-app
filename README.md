# Capture

**Your second brain.**

## What is this?

A single-file web app for capturing todos, notes, wins, and decisions. Everything saves to GitHub. Dexter reads it during conversations.

## Features

- **Instant load**: PWA with service worker (works offline)
- **Mobile-first**: Designed for quick capture on the go
- **GitHub-backed**: All data saved to repo automatically
- **Zero cost**: No servers, no build process
- **Offline support**: Queue writes when offline, sync when back

## Usage

**Live app**: [https://eamongr17-code.github.io/Dexter-personal-/capture/](https://eamongr17-code.github.io/Dexter-personal-/capture/)

1. Open the app
2. Type your thought
3. Pick a category (todo, note, win, decision)
4. Hit "Capture"
5. Done. Saved to GitHub.

## Data Structure

All captures save to `capture/YYYY-MM-DD.json`:

```json
{
  "date": "2026-02-23",
  "todos": [
    {
      "id": 1771565892439,
      "text": "Follow up with Shab",
      "urgency": 3,
      "completed": false,
      "timestamp": "2026-02-23T09:30:00Z"
    }
  ],
  "notes": [...],
  "wins": [...],
  "decisions": [...]
}
```

## Views

- **Today**: Quick capture + today's todos/notes/wins
- **Projects**: Active projects from `app/data/projects.json`
- **Week**: Weekly summary (coming soon)

## How Dexter Uses It

Every session, Dexter reads:
1. Today's capture (`capture/YYYY-MM-DD.json`)
2. Recent 3-7 days for context
3. Project files when relevant

Daily sync (11pm) processes captures into project overviews and compresses old data.

See `SYSTEM/HOMEBASE-OPERATIONS.md` for full details.

## Offline Support

- **Online**: Writes go directly to GitHub
- **Offline**: Queued in localStorage, synced when back online
- **Cache**: Service worker caches the app for instant load

## Development

This is a single HTML file. No build process.

To update:
1. Edit `index.html`
2. Commit to GitHub
3. Deploy via GitHub Pages

**GitHub Token**: Hardcoded in `index.html` (line ~420). Replace if needed.

## Daily Sync

Cron job runs at 11pm daily:

```bash
0 23 * * * cd /Users/dexterprimary/.openclaw/workspace && node scripts/daily-sync.js
```

**What it does**:
- Process captures into project files
- Update MEMORY.md
- Compress old captures (7+ days)
- Commit to GitHub

## Migration from Old System

Old todos from `app/data/todos.json` were migrated to `capture/2026-02-23.json` on Feb 23, 2026.

Projects still live in `app/data/projects.json` (read by both old and new system).

## Why "Capture"?

Because that's what it does. No fluff, just capture and move on.

---

**Built**: Feb 23, 2026  
**Version**: 1.0  
**Status**: Production
