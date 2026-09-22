# Web App Development Docs

A growing collection of practical guides for building web applications with
HTML, CSS, JavaScript, and Python. Built with MkDocs and the Read the Docs theme.

## Local setup

From this repository's directory, create an isolated Python environment and
install the documentation dependencies:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements-docs.txt
```

Start the local preview:

```bash
python -m mkdocs serve
```

Open http://127.0.0.1:8000. MkDocs refreshes the preview as you edit the source.
Stop the server with Ctrl+C.

## Build and validate

With the virtual environment active:

```bash
python -m mkdocs build --strict
```

The generated site is written to `site/`, which Git ignores. Edit the Markdown
source in `docs/`, not the generated files.

## Add a guide

1. Create a Markdown file in `docs/`, using subdirectories when helpful.
2. Follow the template in `docs/writing-guides.md`.
3. Add the page to `nav` in `mkdocs.yml`. Paths are relative to `docs/`.
4. Preview the page and run the strict build.

The initial setup is local only. Add a GitHub remote and a documentation
publishing workflow when you are ready to publish.

## Planned documentation: URL parameters and the search request flow

Requested learning topic (September 8, 2026): explain how JavaScript search
parameters, URLs, Flask routes, and database queries connect, using a small,
concrete example from the sibling `response_robot_database_web_app` project.
This is a note for future documentation work, not a request to write the guide yet.

Context for a future chat: Brian found that typing a full API URL into the browser
and seeing the returned results helped the pieces connect. He has studied this
before but wants a simple walkthrough to rebuild his understanding. Start with
an observable URL and response, introduce terminology as needed, and then trace
the actual code rather than assuming familiarity with routes or querying.

Suggested example:

```text
/api/search-systems?browseBy=system&q=Spot&showAllConfigurations=false
```

Use the running web app's origin before this path. Compare the response with
`showAllConfigurations=true`, explaining that differences depend on the available
matching configurations. Cover:

- The route path (`/api/search-systems`) versus the query string after `?`, with
  named parameters separated by `&`. Explain that `q` is this app's name for
  search text, not a special browser keyword.
- How `static/js/search.js` creates a local `URLSearchParams` object named
  `params` from `filterState`, adds values with `.set()`, and converts it to URL
  text with `.toString()`. It lives in browser memory for that refresh; distinguish
  it from saved settings in `sessionStorage` and from DOM element references.
- How `fetch()` sends the URL without navigating the page, while opening the same
  URL directly in the address bar displays the API response.
- How Flask's `/api/search-systems` route in `app.py` reads `request.args`.
  Distinguish URL parameters from the separate bound SQL parameters used by the
  database query. Explain that only parameters the route handles affect results;
  the frontend also sends `browseBy`, but this route already targets systems.
- How `q=Spot` filters manufacturer/model matches, how the configuration toggle
  controls grouping after filtering, and how JSON `rows` and `count` return to
  `renderSearchResults()` to become visible cards.

Keep the first example small and show the value at each step:
user choice → application state → URL parameters → Flask route → database
query/result grouping → JSON response → rendered page. An annotated flow visual
could support the walkthrough. Recheck the source when writing the guide so the
explanation matches the current implementation.
