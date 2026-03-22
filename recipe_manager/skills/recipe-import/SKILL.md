---
name: recipe-import
description: Parse and import recipes from unstructured text, copied content, or informal descriptions into the standard markdown format. Use when the user pastes recipe text, shares a recipe, asks to "import a recipe", "save this recipe", "convert this recipe", or provides unstructured cooking instructions.
argument-hint: "[recipe text or description]"
allowed-tools: Read, Write, Glob, Bash
---

# Recipe Import

Convert unstructured recipe text into the standard recipe markdown format.

## Import Process

1. **Receive input**: The user provides recipe content as pasted text, a dictated recipe, website content, or an informal family recipe.

2. **Extract structured data**:
   - **Title**: Look for a prominent name or heading
   - **Ingredients**: Lines with quantities, units, food items
   - **Instructions**: Numbered or sequential steps
   - **Metadata**: Servings, prep/cook time, cuisine hints

3. **Infer missing metadata** using context clues:
   - Cuisine: from ingredient combinations and techniques
   - Difficulty: from technique complexity
   - Tags: from ingredients and method
   - Dietary: from ingredient list (see CLAUDE.md dietary rules)
   - Times: estimate if not stated

4. **Normalize ingredients** to: `- QUANTITY UNIT INGREDIENT, PREP_NOTES`
   - Convert informal measurements ("a handful of") to approximate standard units
   - Separate prep notes from ingredient names

5. **Present the formatted recipe** to the user for review before saving.

6. **Save** to `./recipes/` using kebab-case filename from title.

Reference: @${CLAUDE_PLUGIN_ROOT}/skills/recipe-import/references/import-examples.md

## Handling Ambiguity

- If title is unclear, ask the user.
- If servings aren't mentioned, default to 4 and note the assumption.
- If ingredients are vague ("some oil"), use reasonable defaults ("2 tbsp oil").
- Always show parsed result for confirmation before writing.

## Batch Import

For multiple recipes at once, process each separately and confirm each before saving. For large batches, the recipe-parser agent can handle autonomous processing.
