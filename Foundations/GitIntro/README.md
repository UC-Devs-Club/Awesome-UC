# Introduction to Github
**Relevant areas:** Git, CLI, Foundations

> [!Note]
> Originally Written by [Ruhan Shafi](https://github.com/RuhanShafi): Last Updated Semester 2 2026

### Table of Contents
* [What is Git and why do you need to know it?]

### What is Git and why do you need to know it?
Git is a version control system developed by Linus Torvalds (yes, *that* Linus Torvald, the one who made Linux). It is designed to tracks changes to your files over time within a "repository", letting you save checkpoints ("commits"), see exactly what changed and when, undo mistakes, and collaborate with others without overwriting each other's work.

Before Git-style tools existed, and by extension before *you* found out about Git, "version control" often meant folders named `project_final`, `project_final_v2`, `project_final_ACTUALLY_FINAL`, we've all been there. Git replaces that chaos with a structured history you can navigate, compare, and roll back at will.

Why it matters for you specifically:

* It's an industry-standard expectation for virtually any programming job, or anything remotely related to IT
* It enables real collaboration, multiple people can work on the same project without stepping on each other. Sort of how online productive suites such as Google Drive Suite or Office 365 allows multiple people to work on the same document/project, the same applies for any coding project using Git.
* It gives you a safety net when working with projects where you can experiment freely, knowing you can always roll back should anything break or you simply wish to.
* Most of your future projects will live on GitHub (or GitLab/Bitbucket), which are built entirely around Git

### Installing Git

**Windows**: Download and run the installer from git-scm.com. During setup, the default options are fine for beginners — just make sure "Git Bash" and "Add Git to PATH" are selected.

**macOS**:

```bash
# Via Homebrew
brew install git


# Or Git comes bundled with Xcode Command Line Tools
xcode-select --install
```

**Linux (Debian/Ubuntu)**:
```
bash
sudo apt update
sudo apt install git
```

**Linux (Fedora)**:

```
bash
sudo dnf install git
```

**Linux (Arch)**:


```bash
sudo pacman -S git
```

Verify it installed correctly:

```bash
git --version
```

### Setting Up the Git CLI

Before your first commit, Git needs to know who you are and this information gets attached to every commit you make.

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

Other useful one-time setup:

```bash
# Set your default branch name (modern convention is "main")
git config --global init.defaultBranch main

# Set your default editor for commit messages (optional)
git config --global core.editor "code --wait"

# Check all your current config settings
git config --list
```

> [!TIP] 
> Use the same email here as your GitHub account, GitHub matches commits to your profile by email, so a mismatch means your contributions won't show up correctly on your GitHub profile graph.

### Initializing a Local Repository

To start tracking a project with Git, run this inside your project folder:

``` bash
cd my-project
git init
``` 

This creates a hidden .git folder in the folder where you ran the `git init` command. This is is where Git stores the entire history of your project. Deleting this folder removes all Git tracking (but not your actual files).

Check the current state of your repo at any time:

```bash
git status
```

This is the command you'll run constantly, it tells you what's changed, what's staged, and what's untracked.
