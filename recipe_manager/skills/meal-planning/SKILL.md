---
name: meal-planning
description: Generate weekly meal plans, shopping lists, and nutritional summaries from the recipe collection. Use when the user wants a meal plan, asks to plan meals, needs a shopping list or grocery list, or asks "what should I eat this week". Triggers on "meal plan", "plan my meals", "shopping list", "grocery list", "what to buy", "nutritional summary".
argument-hint: "[preferences or constraints]"
allowed-tools: Read, Write, Glob, Grep, Bash
---

# Meal Planning

Generate meal plans, shopping lists, and nutritional summaries from recipes in `./recipes/`.

## Generating a Weekly Meal Plan

1. **Understand preferences** (ask if not provided):
   - Meals per day (default: 3 — breakfast, lunch, dinner)
   - Dietary restrictions
   - Cuisine preferences
   - Difficulty preference (weeknight = easy/medium)
   - Servings per meal

2. **Select recipes** from available collection:
   - Vary cuisines across the week
   - Mix difficulty levels (simpler on weekdays)
   - Respect dietary restrictions
   - Reuse ingredients across meals to reduce shopping
   - If not enough recipes for a full week, note which slots need new recipes

3. **Format the meal plan**:

```markdown
# Meal Plan: March 22 - March 28, 2026

| Day | Breakfast | Lunch | Dinner |
|-----|-----------|-------|--------|
| Mon | ... | ... | ... |
| Tue | ... | ... | ... |
```

4. **Save** to `./meal-plans/YYYY-MM-DD-to-YYYY-MM-DD.md` if user wants it persisted.

## Shopping List Generation

From a meal plan or user-specified set of recipes:

1. Read the Ingredients section of each recipe.
2. Parse quantities and units.
3. Combine duplicates, summing quantities where units match.
4. Group by category:
   - Produce
   - Meat & Seafood
   - Dairy & Eggs
   - Pantry / Dry Goods
   - Spices & Seasonings
   - Other
5. Present the list and optionally save to `./shopping-lists/`.

Reference: @${CLAUDE_PLUGIN_ROOT}/skills/meal-planning/references/nutrition-guidelines.md

## Nutritional Summary

Provide rough nutritional overview per meal and per day (estimates based on common knowledge):
- Approximate calories per serving
- Protein / carbs / fat balance
- Notable nutritional highlights (high protein, high fiber, etc.)

Always note these are estimates, not precise values.
