# Setup Guide

## Exporting ChatGPT History

1. Go to https://chat.openai.com
2. Click your profile icon → Settings
3. Click "Data Controls" → "Export Data"
4. Wait for email with download link
5. Extract the ZIP and place conversations in `/chatgpt-history/`

### Organizing ChatGPT Exports

The export comes as JSON. You can organize by:
- Date: `2024-12/`, `2025-01/`
- Topic: `coding/`, `business/`, `learning/`
- Project: `channel-advisor/`, `pim-cloud/`

## Exporting Claude History

Claude Code conversations can be exported using:
```bash
# Export current session summary
claude --print-conversation > claude-history/YYYY-MM-DD-topic.md
```

## Work Project Summaries

For each major project, create a file in `/projects/`:
- `channel-advisor-catalog.md`
- `pim-cloud.md`
- etc.

Use the template in `/projects/_template.md`
