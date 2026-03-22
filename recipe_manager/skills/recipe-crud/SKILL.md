---
name: recipe-crud
description: Create, read, update, and delete food recipes stored as markdown files. Use when the user wants to add a new recipe, view an existing recipe, edit recipe details, remove a recipe, or list all recipes. Triggers on "new recipe", "save recipe", "edit recipe", "delete recipe", "show recipe", "list recipes".
argument-hint: "[recipe name or details]"
allowed-tools: Read, Write, Edit, Glob, Grep, Bash
---

# Recipe CRUD Operations

Manage recipe files in `./recipes/`. Each recipe is a markdown file with YAML frontmatter.

## Before Any Operation

1. Read CLAUDE.md for the canonical recipe format and field rules.
2. Ensure `./recipes/` exists: `mkdir -p ./recipes/`

## Create a Recipe

1. Gather recipe details from the user. At minimum: title, ingredients, and instructions.
2. Infer reasonable defaults for missing fields:
   - `cuisine`: infer from ingredients and techniques
   - `difficulty`: estimate from technique complexity and ingredient count
   - `prep_time` / `cook_time`: estimate if user provides rough sense
   - `tags`: extract from ingredients and cooking method
   - `dietary`: infer from ingredients using CLAUDE.md dietary rules
   - `date_added`: use today's date
   - `servings`: default to 4 if not specified
3. Generate filename from title (kebab-case, `.md`).
4. Check if file already exists. If so, ask before overwriting.
5. Write using the exact format from CLAUDE.md.
6. Confirm creation and show file path.

Reference: @${CLAUDE_PLUGIN_ROOT}/skills/recipe-crud/references/recipe-schema.md

## Read / View a Recipe

1. If user specifies a name, glob for `./recipes/*name*`.
2. If multiple matches, list them and ask which one.
3. Read and display the recipe in a readable format.
4. To list all: glob `./recipes/*.md` and present a summary table with titles and cuisines from frontmatter.

## Update a Recipe

1. Find the recipe file (same as Read).
2. Read current contents.
3. Apply requested changes using Edit.
4. If title changes, rename file to match new kebab-case title.
5. Confirm update and show what changed.

## Delete a Recipe

1. Find the recipe file.
2. Show title and ask for confirmation.
3. Delete with `rm`.
4. Confirm deletion.

## Listing Recipes

Present a summary table from frontmatter:

| Title | Cuisine | Difficulty | Tags |
|-------|---------|------------|------|
