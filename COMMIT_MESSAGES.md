# Meaningful Git Commit Messages

The MCP server now supports automatic generation of meaningful Git commit messages based on user context.

## How It Works

When you perform operations that modify Home Assistant configuration, you can provide a `description` parameter that explains **what** you're changing and **why**. This description will be used in the Git commit message, making it easy to understand changes later.

## Examples

### Writing Files

Instead of generic "Update file: automations.yaml", you can provide context:

```json
{
  "path": "automations.yaml",
  "content": "...",
  "description": "Add motion sensor automation to control living room lights"
}
```

**Result:** `Automations: Add motion sensor automation to control living room lights`

### Creating Helpers

```json
{
  "type": "input_boolean",
  "config": { "name": "Climate System Enabled" },
  "description": "Enable/disable climate system control for all TRVs"
}
```

**Result:** `Add helper: Enable/disable climate system control for all TRVs`

### Creating Automations

```json
{
  "config": {
    "alias": "Motion Sensor Light Control",
    "trigger": [...],
    "action": [...]
  },
  "description": "Control living room lights when motion detected after sunset"
}
```

**Result:** `Add automation: Control living room lights when motion detected after sunset`

### Creating Scripts

```json
{
  "config": {
    "morning_routine": {
      "alias": "Morning Routine",
      "sequence": [...]
    }
  },
  "description": "Start morning routine: turn on lights and adjust temperature"
}
```

**Result:** `Add script: Start morning routine: turn on lights and adjust temperature`

### Updating Themes

```json
{
  "theme_name": "nice_dark",
  "theme_config": {...},
  "description": "Change primary color to blue for better visibility"
}
```

**Result:** `Update theme: Change primary color to blue for better visibility`

### Applying Dashboards

```json
{
  "dashboard_config": {...},
  "filename": "main-dashboard.yaml",
  "description": "Main dashboard with climate controls and all sensors"
}
```

**Result:** `Update dashboard: Main dashboard with climate controls and all sensors`

## Benefits

1. **Clear History**: Git history shows exactly what was changed and why
2. **Easy Rollback**: When rolling back, you can see what each commit did
3. **Better Understanding**: Future you (or others) can understand the purpose of changes
4. **Automatic**: If you don't provide `description`, a reasonable message is still generated

## Best Practices

- **Be specific**: "Add motion sensor automation" is better than "Update automation"
- **Explain why**: "Fix temperature threshold to prevent overheating" is better than "Change temperature"
- **Use action verbs**: "Add", "Fix", "Update", "Remove", "Configure"
- **Keep it concise**: One sentence is usually enough

## Fallback Behavior

If you don't provide a `description`, the MCP server will still generate a meaningful commit message based on:
- File type (automations, scripts, configuration, etc.)
- Operation type (create, update, delete)
- Entity/automation/script names

Example fallback: `Add automation: Motion Sensor Light Control`

