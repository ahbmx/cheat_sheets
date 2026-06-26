# Python Rich Module - Complete Cheat Sheet

## Installation
```bash
pip install rich
```

## Import Convention
```python
from rich import print
from rich.console import Console
from rich.table import Table
from rich.panel import Panel
from rich.progress import Progress, track
from rich.prompt import Prompt, Confirm, IntPrompt, FloatPrompt
from rich.syntax import Syntax
from rich.markdown import Markdown
from rich.json import JSON
from rich.tree import Tree
from rich.layout import Layout
from rich.columns import Columns
from rich.text import Text
from rich.rule import Rule
from rich.align import Align
from rich.emoji import Emoji
from rich.theme import Theme
from rich import box
```

## 1. Console Object (Core)

```python
console = Console()

# Basic printing
console.print("Hello, World!")
console.print("Hello", "World", "!", sep="-", end="\n\n")
console.print("Bold text", style="bold")
console.print("Colored text", style="red")
console.print("Background color", style="on blue")

# Logging
console.log("This is a log message")
console.log("Log with data", data={"key": "value"})
console.log("Rich log", style="yellow", markup=True)

# Rules/Lines
console.rule("Section Title")
console.rule(style="red")
console.rule(characters="=")

# Clearing
console.clear()
console.soft_clear()
```

## 2. Style Syntax

```python
# Colors
"red", "green", "blue", "yellow", "cyan", "magenta", "white", "black"
"bright_red", "bright_green", "bright_blue", "bright_yellow"
"bright_cyan", "bright_magenta", "bright_white"

# Background colors
"on red", "on green", "on blue", "on yellow", "on cyan"
"on magenta", "on white", "on black"

# Styles
"bold", "italic", "underline", "blink", "reverse", "dim", "strike"

# Combined styles
"bold red on yellow"
"italic bright_blue"
"underline green on white"

# 16 Million Colors (RGB)
"color(255,100,50)"
"color(255,100,50) on color(0,0,128)"

# Hex colors
"#ff0000"
"#ff0000 on #0000ff"
```

## 3. Table Formatting

```python
# Basic table
table = Table(title="User Data")
table.add_column("Name", style="cyan", no_wrap=True)
table.add_column("Age", style="green")
table.add_column("Role", style="magenta")

table.add_row("Alice", "28", "Developer")
table.add_row("Bob", "34", "Designer")
table.add_row("Charlie", "42", "Manager")

console.print(table)

# Advanced table
table = Table(
    title="Advanced Table",
    caption="This is a caption",
    box=box.ROUNDED,
    border_style="bright_blue",
    header_style="bold white on blue",
    padding=(0, 1),
    show_lines=True,
    width=80
)

# Column options
table.add_column("ID", justify="right", style="cyan", width=8)
table.add_column("Product", justify="left", style="green", width=20)
table.add_column("Price", justify="right", style="yellow", width=12)
table.add_column("Status", justify="center", style="bold", width=15)

# Table with footers
table.add_column("Total", footer="Sum", style="bold")

# Box styles
box.ASCII, box.HEAVY, box.DOUBLE, box.SIMPLE
box.ROUNDED, box.SQUARE, box.MINIMAL, box.MINIMAL_HEAVY_HEAD
```

## 4. Progress Bars

```python
# Basic progress
with Progress() as progress:
    task = progress.add_task("[cyan]Processing...", total=100)
    for i in range(100):
        progress.update(task, advance=1)
        # Do work

# Multiple progress bars
with Progress() as progress:
    task1 = progress.add_task("Task 1", total=100)
    task2 = progress.add_task("Task 2", total=50)
    while not progress.finished:
        progress.update(task1, advance=0.5)
        progress.update(task2, advance=0.2)

# Progress with track
for i in track(range(100), description="Processing..."):
    # Do work

# Progress with custom columns
from rich.progress import BarColumn, TextColumn, TimeElapsedColumn, TimeRemainingColumn

progress = Progress(
    TextColumn("[progress.description]{task.description}"),
    BarColumn(),
    TextColumn("[progress.percentage]{task.percentage:>3.0f}%"),
    TimeElapsedColumn(),
    TimeRemainingColumn(),
)

# Progress with spinner
from rich.progress import SpinnerColumn

progress = Progress(
    SpinnerColumn(),
    TextColumn("[progress.description]{task.description}"),
)
```

## 5. Prompts

```python
# Text input
name = Prompt.ask("Enter your name")
password = Prompt.ask("Enter password", password=True)

# Confirm
if Confirm.ask("Continue?"):
    print("Confirmed!")

# Choices
choice = Prompt.ask("Select option", choices=["A", "B", "C"], default="A")

# Numbers
age = IntPrompt.ask("How old are you?", default=25)
price = FloatPrompt.ask("Enter price", default=9.99)

# Auto-complete
result = Prompt.ask("Command", choices=["start", "stop", "restart"])
```

## 6. Panels

```python
# Basic panel
panel = Panel("Content inside panel", title="Title", border_style="green")
console.print(panel)

# Panel with subtitle
panel = Panel("Content", title="Top", subtitle="Bottom", 
              title_align="left", subtitle_align="right")

# Panel with width/height
panel = Panel("Content", width=40, height=5)

# Panel with different styles
Panel.fit("Content", style="white on blue", border_style="yellow")

# Sub-panels
panel = Panel(Panel("Nested"), title="Outer")

# Panel with padding
panel = Panel("Content", padding=(1, 2, 3, 4))

# Safe box panel
from rich.panel import Panel
Panel("Text", safe_box=True)

# Align panel
Align.center(Panel("Centered Panel"))
Align.left(Panel("Left Panel"))
Align.right(Panel("Right Panel"))
```

## 7. Syntax Highlighting

```python
# Code with syntax highlighting
code = """
def hello():
    print("Hello World!")
    return True
"""

syntax = Syntax(code, "python", theme="monokai", line_numbers=True)
console.print(syntax)

# Line numbers with specific start
syntax = Syntax(code, "python", line_numbers=True, start_line=10)

# Different themes
"monokai", "solarized-dark", "solarized-light", "dracula"
"material", "one-dark", "github-dark", "vs"

# Word wrap
syntax = Syntax(long_code, "python", word_wrap=True)

# Code from file
with open("file.py") as f:
    code = f.read()
syntax = Syntax(code, "python")
```

## 8. Markdown

```python
# Render markdown
md = Markdown("""
# Heading 1
## Heading 2
**Bold text**
*Italic text*
- List item 1
- List item 2
[Link](https://example.com)
`code`
```python
print("Hello")
```
""")
console.print(md)

# With hyperlinks
from rich.markdown import Markdown
md = Markdown("[Click me](https://example.com)", hyperlinks=True)

# Code theme
Markdown("# Code", code_theme="monokai")
```

## 9. JSON

```python
data = {"name": "John", "age": 30, "hobbies": ["reading", "coding"]}
json_data = JSON.from_data(data)
console.print(json_data)

# Pretty print with specific indentation
json_data = JSON.from_data(data, indent=2)

# Sort keys
json_data = JSON.from_data(data, sort_keys=True)
```

## 10. Tree Structure

```python
tree = Tree("Root")
branch = tree.add("Branch 1")
branch.add("Leaf 1")
branch.add("Leaf 2")
tree.add("Branch 2").add("Leaf 3")
console.print(tree)

# Styled tree
tree = Tree("📁 Project", style="bold blue")
src = tree.add("📁 src", style="green")
src.add("📄 main.py", style="yellow")
src.add("📄 utils.py", style="yellow")
src.add("📁 tests", style="magenta")
src.add("📄 test_main.py", style="red")
console.print(tree)

# Guide lines
from rich.tree import Tree
tree = Tree("Root", guide_style="dim")
```

## 11. Layout System

```python
# Split layout
layout = Layout()
layout.split(
    Layout(name="header", size=3),
    Layout(name="body"),
    Layout(name="footer", size=3)
)
layout["body"].split_row(
    Layout(name="sidebar", size=30),
    Layout(name="main"),
    Layout(name="right", size=20)
)

# Update with content
layout["header"].update(Panel("Header", style="white on blue"))
layout["body"]["main"].update(Panel("Main content"))
layout["footer"].update(Panel("Footer", style="white on red"))

console.print(layout)

# Ratio based
layout.split_column(
    Layout(name="top", ratio=2),
    Layout(name="bottom", ratio=1)
)
```

## 12. Columns

```python
# Render items in columns
items = ["Item 1", "Item 2", "Item 3", "Item 4", "Item 5"]
columns = Columns(items, equal=True, expand=True)
console.print(columns)

# With styling
columns = Columns(
    [Panel(item) for item in items],
    column_first=True,
    width=20,
    align="center"
)

# Equal width
Columns([Text("A"), Text("Longer text"), Text("C")], equal=True)
```

## 13. Text Manipulation

```python
# Rich Text
text = Text("Hello")
text.append(" World", style="bold red")
text.append("!", style="blue on white")
console.print(text)

# Text with spans
text = Text.assemble(
    ("Hello", "bold cyan"),
    (" World", "magenta"),
    ("!", "white on blue")
)

# Align text
from rich.align import Align
Align.center(Text("Centered"), vertical="middle")

# Justify
Text("Text").justify("center", width=50)

# Highlighting
text = Text("Hello World!")
text.highlight_words(["World"], "bold yellow")
```

## 14. Emoji Support

```python
console.print(":smile: Hello!")
console.print(":heart: Love")
console.print(":rocket: Launch")
console.print(":fire: Hot")
console.print(":warning: Warning")
console.print(":check_mark: Success")
console.print(":cross_mark: Failed")

# Emoji reference
# https://www.webfx.com/tools/emoji-cheat-sheet/
```

## 15. Status Spinners

```python
from rich.status import Status

with Status("Working..."):
    # Do work
    import time
    time.sleep(2)

with Status("Loading", spinner="dots"):
    time.sleep(2)

# Spinner styles
"dots", "line", "dots12", "dots8", "dots10", "dots12"
"dots14", "dots16", "dots18", "dots20", "dots24"
"dots32", "dots48", "dotty", "earth", "balloon"
"bouncingBall", "bouncingBar", "moon"
```

## 16. Live Display

```python
from rich.live import Live

with Live(console=console, refresh_per_second=4) as live:
    for i in range(10):
        live.update(f"Update {i}")
        time.sleep(0.5)

# Update complex content
live = Live(Panel("Initial"), refresh_per_second=4)
live.start()
live.update(Panel("Updated"))
live.stop()
```

## 17. Themes

```python
# Custom theme
theme = Theme({
    "info": "bold cyan",
    "warning": "bold yellow",
    "error": "bold red",
    "success": "bold green"
})
console = Console(theme=theme)

console.print("Info message", style="info")
console.print("Warning message", style="warning")
console.print("Error message", style="error")
console.print("Success message", style="success")

# Built-in themes
# "default", "ansi_light", "ansi_dark", "dracula", "monokai"
```

## 18. Measurement & Formatting

```python
from rich.measure import Measurement
from rich.format import Format

# Get console size
width, height = console.size

# Measure text width
measure = Measurement.get(console, "Hello World")
width = measure.maximum

# Format helpers
console.print("[bold]Hello[/bold]")  # inline markup
console.print("[#ff0000]Red[/#ff0000]")  # hex color
console.print("[rgb(255,0,0)]Red[/rgb(255,0,0)]")  # RGB color
```

---

# Complete Helper Script

```python
#!/usr/bin/env python3
"""
Rich Module Helper Functions
A collection of simple helper functions for common Rich operations
"""

from rich import print as rprint
from rich.console import Console
from rich.table import Table
from rich.panel import Panel
from rich.progress import Progress, track, SpinnerColumn, TextColumn, BarColumn
from rich.prompt import Prompt, Confirm, IntPrompt
from rich.syntax import Syntax
from rich.markdown import Markdown
from rich.json import JSON
from rich.tree import Tree
from rich.layout import Layout
from rich.columns import Columns
from rich.text import Text
from rich.rule import Rule
from rich.align import Align
from rich import box
import time

# Initialize console
console = Console()

# ==================== Basic Helpers ====================

def print_colored(text, color="white", style="", bg_color=""):
    """Print text with color and style"""
    style_str = color
    if bg_color:
        style_str += f" on {bg_color}"
    if style:
        style_str = f"{style} {style_str}"
    console.print(text, style=style_str)

def print_success(text):
    """Print success message in green"""
    console.print(f"✓ {text}", style="bold green")

def print_error(text):
    """Print error message in red"""
    console.print(f"✗ {text}", style="bold red")

def print_warning(text):
    """Print warning message in yellow"""
    console.print(f"⚠ {text}", style="bold yellow")

def print_info(text):
    """Print info message in blue"""
    console.print(f"ℹ {text}", style="bold blue")

def print_heading(text, level=1, style="bold white on blue"):
    """Print a heading with a rule"""
    console.rule(f"[{style}]{text}[/{style}]")

# ==================== Table Helpers ====================

def create_table(data, title="Table", headers=None, caption=None, box_style="rounded"):
    """Create a table from 2D data list"""
    table = Table(title=title, caption=caption, box=getattr(box, box_style.upper()))
    
    if headers:
        for header in headers:
            table.add_column(str(header), style="bold cyan")
    
    for row in data:
        table.add_row(*[str(cell) for cell in row])
    
    return table

def print_table(data, title="Table", headers=None, caption=None):
    """Print a table from 2D data list"""
    table = create_table(data, title, headers, caption)
    console.print(table)

# ==================== Progress Helpers ====================

def show_progress(items, description="Processing"):
    """Show progress bar while processing items"""
    results = []
    for item in track(items, description=description):
        # Simulate processing
        time.sleep(0.1)
        results.append(item)
    return results

def show_spinner(text="Loading...", duration=2, spinner="dots"):
    """Show a spinner while doing work"""
    with Progress(
        SpinnerColumn(spinner),
        TextColumn("[progress.description]{task.description}"),
    ) as progress:
        task = progress.add_task(text, total=None)
        start = time.time()
        while time.time() - start < duration:
            time.sleep(0.1)
        progress.update(task, completed=100)

def multi_progress(tasks):
    """Show multiple progress bars for different tasks"""
    with Progress() as progress:
        task_objs = {}
        for name, total in tasks.items():
            task_objs[name] = progress.add_task(f"[cyan]{name}", total=total)
        
        # Simulate processing
        for _ in range(100):
            for name, task in task_objs.items():
                progress.update(task, advance=0.5)
            time.sleep(0.01)

# ==================== Panel Helpers ====================

def print_panel(content, title=None, border_style="green", padding=1, width=None):
    """Print content inside a panel"""
    panel = Panel(
        content,
        title=title,
        border_style=border_style,
        padding=padding,
        width=width
    )
    console.print(panel)

def print_box(content, title=None, style="bold white on blue"):
    """Print content in a styled box"""
    panel = Panel(
        content,
        title=title,
        border_style="white",
        style=style
    )
    console.print(panel)

# ==================== Code Helpers ====================

def print_code(code, language="python", theme="monokai", line_numbers=True):
    """Print code with syntax highlighting"""
    syntax = Syntax(code, language, theme=theme, line_numbers=line_numbers)
    console.print(syntax)

def print_code_from_file(filename, language=None, theme="monokai"):
    """Print code from file with syntax highlighting"""
    try:
        with open(filename, 'r') as f:
            code = f.read()
        if language is None:
            language = filename.split('.')[-1]
        print_code(code, language, theme)
    except FileNotFoundError:
        print_error(f"File not found: {filename}")

# ==================== Markdown Helpers ====================

def print_markdown(text, code_theme="monokai", hyperlinks=True):
    """Print markdown formatted text"""
    md = Markdown(text, code_theme=code_theme, hyperlinks=hyperlinks)
    console.print(md)

def print_markdown_from_file(filename, code_theme="monokai"):
    """Print markdown from file"""
    try:
        with open(filename, 'r') as f:
            text = f.read()
        print_markdown(text, code_theme)
    except FileNotFoundError:
        print_error(f"File not found: {filename}")

# ==================== JSON Helpers ====================

def print_json(data, indent=2, sort_keys=True):
    """Print JSON data with formatting"""
    json_data = JSON.from_data(data, indent=indent, sort_keys=sort_keys)
    console.print(json_data)

# ==================== Tree Helpers ====================

def create_tree_structure(root_name, structure, style="bold"):
    """Create a tree from nested dictionary structure"""
    tree = Tree(f"[{style}]{root_name}[/{style}]")
    
    def add_branches(node, dict_data):
        for key, value in dict_data.items():
            if isinstance(value, dict):
                branch = node.add(f"[cyan]{key}[/cyan]")
                add_branches(branch, value)
            elif isinstance(value, list):
                branch = node.add(f"[magenta]{key}[/magenta]")
                for item in value:
                    branch.add(f"[yellow]{item}[/yellow]")
            else:
                node.add(f"[green]{key}[/green]: [white]{value}[/white]")
    
    add_branches(tree, structure)
    return tree

# ==================== Interactive Helpers ====================

def ask_yes_no(question, default=True):
    """Ask a yes/no question"""
    return Confirm.ask(question, default=default)

def ask_input(prompt, default=None, choices=None):
    """Ask for text input with optional choices"""
    return Prompt.ask(prompt, default=default, choices=choices)

def ask_number(prompt, default=None):
    """Ask for a number input"""
    return IntPrompt.ask(prompt, default=default)

# ==================== Layout Helpers ====================

def create_dashboard(header_text, sidebar_content, main_content, footer_text):
    """Create a simple dashboard layout"""
    layout = Layout()
    layout.split(
        Layout(name="header", size=3),
        Layout(name="body"),
        Layout(name="footer", size=3)
    )
    layout["body"].split_row(
        Layout(name="sidebar", size=30),
        Layout(name="main")
    )
    
    layout["header"].update(Panel(header_text, style="white on blue"))
    layout["sidebar"].update(Panel(sidebar_content, title="Sidebar", border_style="cyan"))
    layout["main"].update(Panel(main_content, title="Main Content", border_style="green"))
    layout["footer"].update(Panel(footer_text, style="white on red"))
    
    return layout

# ==================== Formatting Helpers ====================

def print_rule(text=None, style="white", characters="-"):
    """Print a rule line"""
    console.rule(text, style=style, characters=characters)

def print_columns(items, width=20, equal=True):
    """Print items in columns"""
    columns = Columns(
        [str(item) for item in items],
        equal=equal,
        width=width
    )
    console.print(columns)

# ==================== Status Helpers ====================

def with_status(text, spinner="dots"):
    """Decorator or context manager for showing status"""
    def decorator(func):
        def wrapper(*args, **kwargs):
            with Progress(
                SpinnerColumn(spinner),
                TextColumn(f"[progress.description]{{task.description}}"),
            ) as progress:
                task = progress.add_task(text, total=None)
                result = func(*args, **kwargs)
                progress.update(task, completed=100)
                return result
        return wrapper
    return decorator

# ==================== Utility Functions ====================

def get_console_size():
    """Get current console width and height"""
    return console.size

def clear_screen():
    """Clear the console"""
    console.clear()

def print_separator(length=80, char="="):
    """Print a separator line"""
    console.print(char * length, style="dim")

# ==================== Example Usage ====================

def example_usage():
    """Demonstrate all helper functions"""
    
    print_heading("Rich Helper Functions Demo", style="bold white on blue")
    
    # Basic printing
    print_success("Everything is working!")
    print_error("Something went wrong!")
    print_warning("This is a warning!")
    print_info("This is information")
    
    print_separator()
    
    # Table example
    data = [
        ["Alice", 28, "Developer"],
        ["Bob", 34, "Designer"],
        ["Charlie", 42, "Manager"]
    ]
    print_table(data, "Users", ["Name", "Age", "Role"])
    
    print_separator()
    
    # Panel example
    print_panel("This is a panel with content", title="Panel Demo", border_style="cyan")
    
    print_separator()
    
    # Progress example
    show_progress(range(10), "Processing items...")
    
    print_separator()
    
    # Tree example
    structure = {
        "src": {
            "main.py": "source code",
            "utils.py": "utilities",
            "tests": ["test_main.py", "test_utils.py"]
        },
        "docs": ["README.md", "LICENSE"]
    }
    tree = create_tree_structure("Project", structure)
    console.print(tree)
    
    print_separator()
    
    # Code example
    code = "def hello(): print('Hello World!')"
    print_code(code, "python")
    
    print_separator()
    
    # JSON example
    json_data = {"name": "John", "age": 30, "hobbies": ["reading", "coding"]}
    print_json(json_data)
    
    print_separator()
    
    # Interactive example
    if ask_yes_no("Would you like to continue?"):
        name = ask_input("What's your name?")
        print_success(f"Hello, {name}!")

if __name__ == "__main__":
    example_usage()
```

## Quick Reference Card

```python
# Most commonly used functions in one place
from rich import print
from rich.console import Console
from rich.table import Table
from rich.panel import Panel
from rich.progress import track, Progress
from rich.prompt import Prompt, Confirm
from rich.syntax import Syntax

console = Console()

# Print with style
console.print("Text", style="bold red on yellow")

# Create tables
table = Table(title="Title")
table.add_column("Col1", style="cyan")
table.add_row("Data1", "Data2")
console.print(table)

# Progress bars
for i in track(range(100), description="Processing"):
    # work
    pass

# Panels
console.print(Panel("Content", title="Title", border_style="green"))

# User input
name = Prompt.ask("Name?")
if Confirm.ask("Continue?"):
    # do something
    pass

# Code highlighting
console.print(Syntax("print('Hello')", "python", theme="monokai"))
```

This comprehensive cheat sheet covers all major features of the Rich library with practical examples and helper functions for quick implementation in your projects.
