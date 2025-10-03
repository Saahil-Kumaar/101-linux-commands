# Contributing

## Pull Requests

### Creating a Pull Request

This book has been designed so that people can easily contribute to it.  
To request us to review changes that you create, you will need to open a pull request.  
Creating a pull request is described in  
[this tutorial](https://www.digitalocean.com/community/tutorials/how-to-create-a-pull-request-on-github).

### File Location/Types

### [`ebook`](./ebook)

This directory contains all of the translations of the eBook.

### [`ebook/{LANG}`](./ebook/{LANG})

The `ebook` directory contains translations of the eBook in different languages.

If you are adding a new translation, copy the `./ebook/en` directory and use the language code as the new directory name.

### [`ebook/{LANG}/content`](./ebook/{LANG}/content)

All the Markdown files for the '101 Linux commands' eBook are located within the [`content`](./content) directory for the specific language.

For example, if you are adding a Bulgarian translation, copy the `./ebook/en` folder to `./ebook/bg`, translate the `.md` files in the `content` directory, and submit a PR.

### eBook Generation

The project uses [Ibis Next](https://github.com/Hi-Folks/ibis-next) developed by [Roberto Butti](https://github.com/roberto-butti), forked from the original [Ibis](https://github.com/themsaid/ibis/) by [Mohamed Said](https://github.com/themsaid).

Ibis Next supports generating PDF, EPUB, and HTML formats from Markdown content.

## Setup and Usage

1. Install dependencies:

```bash
composer install
```

2. Generate PDF (light theme):

```bash
composer run pdf
```

3. Generate PDF (dark theme):

```bash
composer run pdf-dark
```

4. Generate EPUB:

```bash
composer run epub
```

5. Generate HTML:

```bash
composer run html
```

For more information about Ibis Next, visit: [Getting started with Ibis Next](https://github.com/Hi-Folks/ibis-next)

## Contribution Examples

### Typical Git workflow

1. Fork the repository on GitHub and clone your fork locally.

```bash
git clone https://github.com/<your-user>/101-linux-commands.git
cd 101-linux-commands
```

2. Create a dedicated branch for your changes.

```bash
git checkout -b feature/add-cli-example
```

3. While you work, check your status and stage files deliberately.

```bash
git status
git add CONTRIBUTING.md
```

4. Commit with a descriptive message and push your branch.

```bash
git commit -m "docs: add CLI contribution examples"
git push origin feature/add-cli-example
```

### Running the CLI locally

1. Move into the CLI workspace.

```bash
cd cli
```

2. (Recommended) Create and activate a virtual environment. Use the command that matches your shell:

```bash
python -m venv .venv
# Windows PowerShell
.\.venv\Scripts\Activate.ps1
# macOS/Linux
source .venv/bin/activate
```

3. Install the dependencies and the CLI in editable mode.

```bash
pip install -r requirements.txt
pip install -e .
```

4. Confirm the CLI works.

```bash
linux-cli --help
# or run directly without installation
python -m cli.cli hello greet --name "Linux Contributor"
# greet someone specific using the installed entry point
linux-cli hello greet --name "Linux Contributor"
```

### Adding a new command

1. Create a new command module inside `cli/commands/`. Example (`cli/commands/ping.py`):

```python
import typer

app = typer.Typer(help="Ping command group")

@app.command()
def once():
    """Print a ping message."""
    typer.echo("pong")
```

2. Register the command with the main Typer app in `cli/cli.py`:

```python
from commands import hello, ping

app = typer.Typer(help="101 Linux Commands CLI 🚀")
app.add_typer(hello.app, name="hello")
app.add_typer(ping.app, name="ping")
```

3. Add or update tests in `cli/test_cli.py` to cover your new command. Mirror the existing `hello` command tests and update expectations.

4. Run the CLI manually to verify your command behaves as expected.

```bash
python -m cli.cli ping once
```

### Running tests

1. Ensure you're in the `cli` directory with your virtual environment activated.

2. Install the testing dependency if you haven't already.

```bash
pip install pytest
```

3. Execute the test suite:

```bash
pytest
```

4. (Optional but encouraged) Run the additional quality checks that the workflow executes:

```bash
black cli/
isort cli/
flake8 cli/
mypy cli/
```

## Issue Creation

If you have an issue using the guide or want to suggest a change but cannot contribute changes,  
we are more than happy to help.  
Make sure that when you create your issue, it follows the format for the type of issue you select  
(it has individual templates for each issue type).

Issue template types include the following:

- Bug Reporting  
- Feature Requests  
- Help Requests  
