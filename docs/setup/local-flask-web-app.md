# Set up a local Flask web app

Create a small Python web app that opens a page in your browser and leaves
room for templates, styles, routes, and database code later.

## Before you start

You need Python 3 installed on Linux. Run the commands below from the
directory where you keep your projects.

## Create the project

Make a project directory and enter it:

```bash
mkdir my-web-app
cd my-web-app
```

Create an isolated virtual environment, activate it, and install Flask:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install Flask
```

Save the dependency so the project can be recreated later:

```bash
python -m pip freeze > requirements.txt
```

Create the application folders:

```text
my-web-app/
├── .venv/
├── app.py
├── requirements.txt
├── templates/
│   └── index.html
└── static/
```

The `static/` folder can remain empty for now. It is ready for CSS,
JavaScript, and images when the page needs them.

## Add the application

Create `app.py`:

```python
from flask import Flask, render_template

app = Flask(__name__)


@app.get("/")
def home():
    return render_template("index.html")
```

`Flask(__name__)` creates the application. The `@app.get("/")` decorator
connects the browser path `/` to the `home` function. The function returns the
HTML template instead of putting HTML directly in the Python file.

Create `templates/index.html`:

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>My Web App</title>
  </head>
  <body>
    <main>
      <h1>My Web App</h1>
      <p>The local app is running.</p>
    </main>
  </body>
</html>
```

Flask looks for templates in a directory named `templates` next to `app.py`.
Keeping the HTML there makes it straightforward to add more pages and shared
layouts later.

## Run it in the browser

With the virtual environment active, start Flask's development server:

```bash
flask --app app run --debug
```

Open <http://127.0.0.1:5000/>. You should see “My Web App”. The development
server reloads when you save a source file. Stop it with Ctrl+C.

The `--debug` option is useful for local development because it reloads code
changes and shows helpful errors. Do not use Flask's development server to host
an internet-facing production site.

## Add the project to Git

Create `.gitignore` so the virtual environment and Python caches are not
committed:

```gitignore
.venv/
__pycache__/
*.pyc
```

Then create the first commit:

```bash
git init
git add app.py templates/ static/ requirements.txt .gitignore
git commit -m "Create minimal Flask web app"
```

## Where to grow next

- Add CSS or browser JavaScript under `static/` and link it from the template.
- Add another route and template for a second page.
- Extract shared page structure into a Jinja template layout.
- Add configuration and database access after the page flow is clear.

Keep the first version small: each new folder or dependency should support a
feature you are ready to build.
