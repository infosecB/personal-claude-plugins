---
name: dashboard
description: Display a dashboard overview of the recipe collection with stats, breakdowns by cuisine/difficulty/dietary, tag summary, meal plan status, shopping list status, and a full recipe table. Triggers on "dashboard", "recipe stats", "show my collection", "recipe overview", "how many recipes".
argument-hint: "[optional: focus area like 'cuisines' or 'tags']"
allowed-tools: Read, Glob, Grep, Bash
---

# Recipe Dashboard

Generate a rich summary dashboard of the user's recipe collection.

## Interactive Dashboard

An interactive HTML dashboard is available at `${CLAUDE_PLUGIN_ROOT}/skills/dashboard/dashboard.html`. If the user asks to open or view the dashboard visually, open this file in their browser:

```bash
open "${CLAUDE_PLUGIN_ROOT}/skills/dashboard/dashboard.html"
```

The user can drag & drop their `recipe_manager` folder into the browser to load all recipes, meal plans, and shopping lists with visual charts and search.

## Terminal Dashboard

For a quick text-based overview, generate the dashboard directly in the terminal:

1. Read CLAUDE.md for the canonical recipe format.
2. Glob `./recipes/*.md` to find all recipe files.
3. Read frontmatter from each recipe file.
4. Glob `./meal-plans/*.md` and `./shopping-lists/*.md` for meal plans and shopping lists (these directories may not exist yet — that's fine, just report 0).

## Dashboard Sections

Render the dashboard using well-formatted markdown. Include all of the following sections:

### 1. Overview Stats

Show a summary line:
```
📊 X recipes | Y cuisines | Z tags | W meal plans | V shopping lists
```

### 2. Cuisine Breakdown

A table showing each cuisine and its recipe count, sorted by count descending:

| Cuisine | Recipes |
|---------|---------|

### 3. Difficulty Breakdown

A table with counts for easy, medium, and hard:

| Difficulty | Recipes |
|------------|---------|

### 4. Dietary Tags

List each dietary tag found across recipes and how many recipes have it:

| Dietary | Recipes |
|---------|---------|

### 5. Tag Cloud

Show all tags with counts, sorted by frequency descending. Format as a compact inline list:
`tag1 (N) · tag2 (N) · tag3 (N) · ...`

### 6. Meal Plans

If any meal plan files exist, list them with their titles and dates. Otherwise note that none exist yet.

### 7. Shopping Lists

If any shopping list files exist, list them with their titles. Otherwise note that none exist yet.

### 8. All Recipes

A full table of every recipe, sorted by title:

| Title | Cuisine | Difficulty | Servings | Prep | Cook | Added |
|-------|---------|------------|----------|------|------|-------|

## Focus Mode

If the user asks about a specific area (e.g., "show me cuisine stats" or "what tags do I have"), show only the relevant section in more detail rather than the full dashboard.
