# CLAUDE.md

This file provides guidance to Claude Code when working with this marketplace repository.

## Marketplace Structure

This repository serves as a Claude Code plugin marketplace that aggregates multiple plugins.

```
claude-marketplace/
├── .claude-plugin/
│   └── marketplace.json         # Marketplace manifest
├── CLAUDE.md                    # This file
└── README.md
```

## Adding a Plugin

To add a new plugin to the marketplace:

1. Add plugin entry to `.claude-plugin/marketplace.json`:

```json
{
  "name": "plugin-name",
  "source": {
    "source": "url",
    "url": "https://github.com/username/plugin-repo.git",
    "ref": "1.0.0"
  },
  "description": "Plugin description",
  "version": "1.0.0",
  "author": { "name": "username" },
  "license": "MIT",
  "keywords": ["keyword1", "keyword2"]
}
```

2. Add plugin to `README.md` table
3. Commit and push changes

## Updating Plugin Versions

When a plugin releases a new version:

1. Update the `ref` field in `marketplace.json` (e.g., `"ref": "1.2.0"`)
2. Update the `version` field to match
3. Commit and push

**IMPORTANT:** Plugin tags should use semantic versioning **WITHOUT** the 'v' prefix:
- ✅ Use: `"ref": "1.2.0"`
- ❌ Don't use: `"ref": "v1.2.0"`

## Version Format

All plugin versions in this marketplace follow semantic versioning without the 'v' prefix:

- ✅ Correct: `1.0.0`, `1.2.3`, `2.0.0`
- ❌ Incorrect: `v1.0.0`, `v1.2.3`, `v2.0.0`

## Testing Changes

After updating the marketplace:

```bash
# Reinstall the plugin to test
claude plugin remove plugin-name@briannadoubt
claude plugin install plugin-name@briannadoubt

# Verify the version
claude plugin list | grep -A 3 plugin-name
```

## Troubleshooting

If a plugin doesn't update to the new version:
1. Remove the plugin: `claude plugin remove plugin-name@briannadoubt`
2. Clear plugin cache if needed
3. Reinstall: `claude plugin install plugin-name@briannadoubt`
4. Verify the `ref` field in marketplace.json points to the correct tag
