# Introduction to Programming

>[!Note]
> Originally Written by [Ruhan Shafi](https://github.com/RuhanShafi): Last Updated Semester 2 2026

### Table of Contents
* [What Actually Happens When You Run Code](#what-actually-happens-when-you-run-code)
* [Installing a Language Properly](#installing-a-language-properly)
* [What PATH Actually Is](#what-path-actually-is)
* [Setting Up VS Code Properly](#setting-up-vs-code-properly)
* [Virtual Environments](#virtual-environments)
* [Package Managers](#package-managers)
* [How to Debug](#how-to-debug)
  * [Reading Error Messages (Tracebacks)](#reading-error-messages-tracebacks)
* [How to Read Documentation](#how-to-read-documentation)
* [Basic Python Introduction](#basic-python-introduction)
* [Common Beginner Mistakes](#common-beginner-mistakes)


### What Actually Happens When You Run Code

Programming languages generally fall into two categories:

- **Compiled languages** (C, C++, Java, Rust) translate your entire program into machine code *before* it runs, producing a standalone executable. This is why you "build" or "compile" a project before running it — and why you can get errors at the *compile stage* before your program has even started.
- **Interpreted languages** (Python, JavaScript, Ruby) are read and executed line-by-line by an interpreter at runtime, with no separate build step. This is why Python feels more immediate — you just hit run — but it also means some errors only show up once the program reaches that specific line, not before.

Neither approach is objectively "better" — they trade off raw execution speed against speed of iteration and simplicity. Knowing which category a language falls into helps you understand *why* and *when* errors appear, and why some languages need a "build" step while others don't.

Additionally, some languages (like Java, and to an extent Python) are actually a hybrid — compiled to an intermediate bytecode, then interpreted or JIT-compiled at runtime. You don't need to go deep here, just enough that people aren't surprised when they encounter it later.


### Installing a Language Properly
- **System-wide installs** put one version of a language on your machine, available everywhere. Simple, but it becomes a problem the moment two projects need different versions.
- **Version managers** — tools like `pyenv` (Python), `nvm` (Node.js), or `rbenv` (Ruby) — let you install multiple versions side by side and switch between them per-project. This avoids a very common real-world headache: "this project needs Python 3.9, but I only have 3.12 installed."

For a beginner workshop, a system-wide install is completely fine to start with — but flagging that version managers exist means people aren't blindsided later when a tutorial or job suddenly requires a specific version.

**Also worth a mention:** always install from the *official* source (python.org, nodejs.org, etc.) or your OS's package manager if you're using Linux which will be covered in the following workshop. Never install from a random third-party download link, which is a common source of malware for beginners who don't know better.


### What PATH Actually Is

One of the most common and most confusing beginner errors is typing a command and getting back `command not found` or `'python' is not recognized as an internal or external command`.

This almost always comes down to **PATH**: a list of folders your operating system checks, in order, whenever you type a command in the terminal. If the program you're trying to run isn't installed in one of those folders (or wasn't added to the list), your computer has no idea what you're talking about — even though the program is sitting right there on your hard drive.

The fix is always the same shape: find the folder where the tool was installed, and add that folder to PATH. Once people understand this one concept, a huge chunk of "why doesn't this work" mysteries disappear saving hours in debugging and headaches.


### Setting Up VS Code Properly

VS Code works out of the box, but a few configuration steps turn it from "a text editor" into a real development environment:

- **Language extensions** — install the official extension for your language (e.g. the Python extension) for syntax highlighting, autocomplete (IntelliSense), and inline error checking as you type, before you even run the code.
- **Linters & formatters** — tools like `Pylint`, `Flake8`, or `Prettier` catch style issues and likely bugs automatically, and can auto-format your code on save so you're not manually fighting indentation and spacing.
- **Integrated terminal** — VS Code has a built-in terminal (`` Ctrl+` ``), so you never have to alt-tab to a separate terminal app to run your code.
- **Debugger integration** — VS Code lets you set breakpoints and step through your code line-by-line, inspecting variables as you go. This is a huge upgrade over debugging with scattered `print()` statements.
- **Useful keybindings** — `Ctrl+P` (quickly open any file by name), `Ctrl+Shift+F` (search across the entire project), `Ctrl+/` (comment/uncomment a line).
- **Settings sync** — if people have multiple machines, mention that VS Code can sync extensions and settings via a GitHub/Microsoft account, so they don't have to reconfigure everything each time.


### Virtual Environments

A virtual environment is an isolated, self-contained space for a specific project's dependencies — separate from your system-wide language install and separate from other projects.

**Why they matter:** without one, every package you install goes into one global pool. Project A might need `requests==2.10` while Project B needs `requests==2.31` — without isolation, installing one breaks the other. Virtual environments solve this by giving each project its own private set of installed packages.

**Basic Python example:**

```bash
# Create a virtual environment named "venv"
python -m venv venv

# Activate it (macOS/Linux)
source venv/bin/activate

# Activate it (Windows)
venv\Scripts\activate

# Install packages — these only affect this environment
pip install requests

# Deactivate when done
deactivate
```

A good habit to instill early: **one virtual environment per project**, and never install packages globally unless there's a specific reason to. It's a small extra step that saves a lot of pain later.


### Package Managers

Almost no real project is built entirely from scratch — you'll rely on libraries other people have written, and package managers are how you install and manage them.

- **Python** → `pip` (e.g. `pip install requests`)
- **JavaScript/Node.js** → `npm` (e.g. `npm install express`)
- **Rust** → `cargo`
- **Java** → Maven or Gradle

This ties directly into virtual environments: a package manager installs libraries *into* your current environment, so keeping projects isolated prevents dependency conflicts between them. A useful mental model to use: your language is the toolbox, and packages are specialized tools other people built and shared so you don't have to reinvent them yourself.


### How to Debug

Debugging is arguably the single most important skill in programming, arguably more important than writing the code in the first place, since you'll spend far more time fixing things than writing them from scratch.

**Core debugging approaches:**

- **Read the error message first.** This sounds obvious, but it's the single most skipped step. See the section below.
- **Print debugging** — scatter `print()` statements to check the value of variables at different points. Simple, effective, and universally available.
- **Using a real debugger** — setting breakpoints (in VS Code, click to the left of a line number) lets you pause execution and inspect every variable at that exact moment, rather than guessing where to add print statements.
- **Rubber duck debugging** — explain your code line-by-line, out loud, to another person (or literally a rubber duck). The act of explaining often surfaces the bug yourself, before the other person even says anything.
- **Isolate the problem** — comment out or remove code until the bug disappears, narrowing down exactly which section is responsible, rather than staring at the whole file at once.
- **Check your assumptions** — a huge number of bugs come from assuming a variable holds what you *think* it holds. Print it out and check.

#### Reading Error Messages (Tracebacks)

This might be the single highest-value skill for a beginner, and it's often skipped entirely in favor of panic-Googling the whole error message.

Teach people to read Python tracebacks **from the bottom up**:
- The **last line** tells you the actual error type and message (e.g. `NameError: name 'x' is not defined`) — this is the headline.
- The lines **above it** show the chain of function calls that led there, each with a file name and line number pointing to exactly where to look.

The mindset shift worth emphasizing: an error message isn't the program "breaking" at you. Rather think that it's the program telling you precisely what went wrong and where, if you take a moment to actually read it instead of scrolling straight past it.


### How to Read Documentation

Documentation is the single most reliable source of truth for any language or library — more reliable than random blog posts, and definitely more reliable than half-remembered advice from a forum thread.

- **Start with the official docs** (e.g. docs.python.org, a library's official ReadTheDocs page) rather than defaulting straight to search results.
- **Learn to read a function signature** — e.g. `open(file, mode='r', encoding=None)` tells you the required argument, default values, and what you're allowed to customize, without needing an example at all.
- **Use Ctrl+F liberally** — documentation pages are long; searching for the specific method or keyword you need is faster than reading top to bottom.
- **Look for a "Quickstart" or "Getting Started" section** — most good documentation has one, designed specifically to get you oriented fast.
- **Don't be afraid of official examples** — most docs include runnable code snippets; running them yourself (and tweaking them) cements understanding far better than just reading.

> [!NOTE]
> AI tools like Claude or ChatGPT are excellent for explaining a confusing doc page in plainer language, or for debugging *alongside* you. But relying on them to write code you don't understand yourself will hurt you long-term, especially early on. Treat them as a tutor, not a replacement for actually learning to read the source material.


### Basic Python Introduction

A quick, practical on-ramp for anyone who's never written code before:

```python
# Variables
name = "Alice"
age = 20

# Conditionals
if age >= 18:
    print(f"{name} is an adult")
else:
    print(f"{name} is a minor")

# Loops
for i in range(5):
    print(i)

# Functions
def greet(person):
    return f"Hello, {person}!"

print(greet("Bob"))

# Lists
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)
```

Key beginner concepts worth knowing:
- **Indentation matters** in Python — it defines code blocks instead of curly braces `{}`
- **Data types** — strings, integers, floats, booleans, lists, dictionaries
- **f-strings** for clean string formatting (`f"{name} is {age}"`)
- Running a script: `python filename.py`


### Common Beginner Mistakes

- **Not reading the error message** — skimming past it and guessing, instead of reading exactly what it says
- **Copy-pasting code without understanding it** — it might work, but you won't be able to fix or extend it later
- **Ignoring indentation** — since Python uses indentation to define code blocks, one misaligned line causes confusing errors
- **Not testing incrementally** — writing 100 lines before running anything once, instead of testing small pieces as you go
- **Confusing `=` and `==`** — assignment vs. comparison is one of the most common early bugs across almost every language
- **Installing packages globally instead of in a virtual environment** — works at first, causes conflicts later
- **Not saving/backing up work** — losing hours of progress with no way to roll back


### Where to Go Next

- **Practice platforms** — freeCodeCamp (structured, beginner-friendly), LeetCode (interview-style problems), Advent of Code (fun, seasonal challenge problems)
- **Documentation** — make official docs the first stop, not the last resort
- **Communities** — Stack Overflow for specific questions, r/learnprogramming for general guidance, and your own club (UC DEVS) for ongoing support and future workshops
- **Build something small** — a to-do list app, a simple calculator, a script that automates something tedious in your own life. Small real projects teach far more than tutorials alone.
- **Using AI tools responsibly** — genuinely useful for explaining concepts and debugging *with* you, but not a substitute for understanding what your own code does
