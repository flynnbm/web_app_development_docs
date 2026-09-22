# Writing Guides

Keep each guide focused on a task you might want to repeat. Explain unfamiliar
syntax alongside the example, and identify where each piece of code belongs.
Start with a small working example; add complexity only when the task needs it.

## Suggested page outline

Copy this outline into a new Markdown file and replace the prompts:

```markdown
# Task title, such as Add a button to a page

Describe what the reader will be able to do and what the result looks like.

## Before you start

List the existing files or concepts this example depends on.

## Files involved

Identify the HTML, CSS, JavaScript, or Python files used and each file's role.

## Steps

Show the smallest useful changes, where to put them, and why they are needed.
Explain new syntax as it appears.

## How it works

Trace the interaction from the user's action through the relevant functions
and state changes to the visible result.

## Check the result

Describe how to try the feature and the behavior to expect.
Include relevant keyboard and small-screen checks for interface changes.

## Adapt it

Explain which labels, selectors, values, or styles to change for another use.

## Related guides

Link to existing pages that explain supporting concepts or a complete feature.
```

## Register a new page

For example, after creating `docs/html/add-a-button.md`, add it to the existing
`nav` list in `mkdocs.yml`:

```yaml
  - HTML and Page Structure:
      - Add a Button: html/add-a-button.md
```

Only add navigation entries and links once their target pages exist. Run
`python -m mkdocs build --strict` before considering a guide ready.
