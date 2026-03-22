---
name: recipe-search
description: Search, filter, and find recipes by ingredients, cuisine, tags, dietary restrictions, difficulty, or any combination. Use when the user wants to find recipes, asks "what can I make with...", searches by ingredient, filters by cuisine or dietary need. Triggers on "find recipe", "search recipes", "show me all", "what recipes have", "recipes with".
argument-hint: "[search criteria]"
allowed-tools: Read, Glob, Grep, Bash
---

# Recipe Search

Find and filter recipes in `./recipes/` based on user criteria.

## Search Strategy

Recipes are markdown files with YAML frontmatter. Use grep to search frontmatter fields and ingredient lists.

### By Ingredient

```bash
grep -rl "ingredient_name" ./recipes/
```

For multiple ingredients (ALL must match), chain greps or read each candidate and verify.

### By Cuisine

```bash
grep -rl "^cuisine: Indian" ./recipes/
```

### By Tag

```bash
grep -rl "tags:.*tagname" ./recipes/
```

### By Dietary Restriction

```bash
grep -rl "dietary:.*vegetarian" ./recipes/
```

### By Difficulty

```bash
grep -rl "^difficulty: easy" ./recipes/
```

## Combining Filters

When user specifies multiple criteria (e.g., "easy vegetarian Indian recipes"):

1. Start with the most restrictive filter.
2. Read frontmatter of matching files.
3. Apply remaining filters programmatically.
4. Present results as a summary table.

## "What Can I Make With..." Queries

When the user lists ingredients they have on hand:

1. Search for recipes containing those ingredients.
2. Rank by how many of the user's ingredients each recipe uses.
3. Note which additional ingredients are needed.
4. Present top matches with a "missing ingredients" list.

## Output Format

Present results as a table:

| Recipe | Cuisine | Difficulty | Key Match |
|--------|---------|------------|-----------|

If only one result, display the full recipe.
