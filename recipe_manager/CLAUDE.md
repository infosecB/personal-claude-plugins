# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a Claude Code plugin for managing food recipes stored as markdown files with YAML frontmatter.

## Plugin Structure

- `skills/recipe-crud/` — create, read, update, delete recipes
- `skills/recipe-search/` — find recipes by ingredients, cuisine, tags, dietary restrictions
- `skills/recipe-import/` — parse unstructured text into structured recipe format
- `skills/meal-planning/` — generate meal plans, shopping lists, nutritional summaries
- `agents/recipe-parser.md` — autonomous batch import agent

## Storage Directories

- `./recipes/` — individual recipe markdown files
- `./meal-plans/` — weekly meal plan files
- `./shopping-lists/` — generated shopping lists

Create directories on first use with `mkdir -p`.

## Recipe File Naming

Kebab-case from title: `chicken-tikka-masala.md`, `french-onion-soup.md`. No numbering or date prefixes.

## Recipe Format

Every recipe file must follow this structure:

```markdown
---
title: Recipe Name
cuisine: Italian
servings: 4
prep_time: 20 min
cook_time: 40 min
tags: [pasta, easy, weeknight]
dietary: [vegetarian]
difficulty: easy
date_added: YYYY-MM-DD
---

## Ingredients
- quantity unit ingredient, prep notes

## Instructions
1. Step one...

## Notes
Optional notes.
```

### Required Frontmatter Fields

| Field | Type | Values / Format |
|-------|------|-----------------|
| title | string | Recipe name |
| cuisine | string | e.g., Italian, Indian, Mexican, American, Thai, Japanese, French, Mediterranean, Korean, Chinese |
| servings | integer | Number of servings |
| prep_time | string | "X min" or "X hr Y min" |
| cook_time | string | "X min" or "X hr Y min" |
| tags | string[] | Lowercase. Include key ingredients, cooking method, meal type, character |
| dietary | string[] | Empty `[]` if none. Allowed: vegetarian, vegan, gluten-free, dairy-free, nut-free, low-carb, keto, paleo |
| difficulty | string | easy, medium, hard |
| date_added | string | YYYY-MM-DD |

### Ingredients Format

Pattern: `- QUANTITY UNIT INGREDIENT, PREP_NOTES`

Examples: `- 1 lb chicken breast, cubed` / `- 2 cloves garlic, minced` / `- salt and pepper to taste`

### Dietary Inference Rules

- No meat/fish/poultry → vegetarian
- No animal products → vegan (also add vegetarian)
- No wheat/barley/rye/flour → gluten-free
- No milk/cheese/cream/butter/yogurt → dairy-free
- No tree nuts or peanuts → nut-free
