# Recipe Schema Reference

## Complete YAML Frontmatter Fields

| Field | Type | Required | Values / Format |
|-------|------|----------|-----------------|
| title | string | yes | Recipe name |
| cuisine | string | yes | e.g., Italian, Indian, Mexican, Thai, Japanese, French, American, Mediterranean, Korean, Chinese |
| servings | integer | yes | Number of servings |
| prep_time | string | yes | "X min" or "X hr Y min" |
| cook_time | string | yes | "X min" or "X hr Y min" |
| tags | string[] | yes | Lowercase descriptive. Include key ingredients, cooking method, meal type, character |
| dietary | string[] | yes | Empty `[]` if none. Allowed: vegetarian, vegan, gluten-free, dairy-free, nut-free, low-carb, keto, paleo |
| difficulty | string | yes | easy, medium, hard |
| date_added | string | yes | YYYY-MM-DD |

## Dietary Inference Rules

- No meat/fish/poultry → vegetarian
- No animal products at all → vegan (also add vegetarian)
- No wheat/barley/rye/flour products → gluten-free
- No milk/cheese/cream/butter/yogurt → dairy-free
- No tree nuts or peanuts → nut-free

## Example

```yaml
---
title: Chicken Tikka Masala
cuisine: Indian
servings: 4
prep_time: 20 min
cook_time: 40 min
tags: [chicken, curry, spicy, weeknight]
dietary: []
difficulty: medium
date_added: 2026-03-22
---
```
