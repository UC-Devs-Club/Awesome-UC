# Introduction to Github
**Relevant areas:** Git, CLI, Foundations

> [!Note]
> Originally Written by [Ruhan Shafi](https://github.com/RuhanShafi): Last Updated Semester 2 2026

### Table of Contents
* [What is Git and why do you need to know it?](#what-is-git-and-why-do-you-need-to-know-it)
* [Installing Git](#installing-git)
* [Setting Up the Git CLI](#setting-up-the-git-cli)
* [Initializing a Local Repository](#initializing-a-local-repository)
* [Committing to Local](#committing-to-local)
* [Version Control Concepts](#version-control-concepts)
* [Pushing to a Remote](#pushing-to-a-remote)
* [Using the GitHub CLI](#using-the-github-cli)
* [Multiple People Working on the Same Repo](#multiple-people-working-on-the-same-repo)
* [Branches](#branches)
* [Merging](#merging)
* [Merge Conflicts](#merge-conflicts)
* [Common Beginner Mistakes](#common-beginner-mistakes)
* [Where to go next](#where-to-go-next)

### What is Git and why do you need to know it?
Git is a version control system developed by Linus Torvalds (yes, ***that*** Linus Torvald, the one who made Linux). It is designed to tracks changes to your files over time within a "repository", letting you save checkpoints ("commits"), see exactly what changed and when, undo mistakes, and collaborate with others without overwriting each other's work.

Before Git-style tools existed, and by extension (let's be honest here, I can personally attest to this) before *you* found out about Git, "version control" often meant folders named `project_final`, `project_final_v2`, `project_final_ACTUALLY_FINAL`, we've all been there. Git replaces that chaos with a structured history you can navigate, compare, and roll back at will.

Why it matters for you specifically:

* It's an industry-standard expectation for virtually any programming job, or anything remotely related to IT
* It enables real collaboration, multiple people can work on the same project without stepping on each other. Sort of how online productive suites such as Google Drive Suite or Office 365 allows multiple people to work on the same document/project, the same applies for any coding project using Git.
* It gives you a safety net when working with projects where you can experiment freely, knowing you can always roll back should anything break or you simply wish to.
* Most of your future projects will live on GitHub (or GitLab/Bitbucket), which are built entirely around Git

### Installing Git

**Windows**: Download and run the installer from [git-scm.com](https://git-scm.com/downloads). During setup, the default options are fine for beginners but just remember to make sure "Git Bash" and "Add Git to PATH" are selected.

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

### Committing to Local

Git tracks changes in three stages:

```
Working Directory  →  Staging Area  →  Repository (committed)
      (edited)          (git add)         (git commit)
```

**Basic workflow:**

```bash
# See what's changed
git status

# Stage a specific file
git add filename.txt

# Or stage everything that's changed
git add .

# Commit your staged changes with a message
git commit -m "Add initial project structure"

# View your commit history
git log
git log --oneline    # condensed, one line per commit
```

**Why staging exists:** it lets you build a commit deliberately, you might have five files changed, but only want two of them in this particular commit. `git add` lets you choose exactly what goes in.

**Undoing things:**

| Situation | Command |
|---|---|
| Unstage a file (keep changes) | `git restore --staged filename.txt` |
| Discard uncommitted changes to a file | `git restore filename.txt` |
| Change your last commit's message | `git commit --amend -m "New message"` |
| See what changed in a file | `git diff filename.txt` |

### Version Control Concepts

- **Commit**: A snapshot of your project at a point in time, with a message describing what changed and why. Think of it as a save point you can always return to.
- **`.gitignore`**: A file listing things Git should never track (build artifacts, secrets, `node_modules/`, `.env` files, IDE settings). Create one early accidentally committing a password or API key is a very common and very avoidable mistake that happens to also be very costly (or can get you fired).

```bash
  # Example .gitignore
  node_modules/
  .env
  *.log
  __pycache__/
  ```
- **Commit history is immutable (mostly)**: Once pushed and shared, rewriting history (e.g. with `git commit --amend` or `rebase`) can cause real problems for collaborators. Amend/rebase freely on local, unpushed work; be careful once it's shared.
- **Good commit messages matter**: "fixed stuff" tells future-you nothing. A clear, specific message (bonus points for a convention like Conventional/Angular commits) makes your history genuinely useful months later.

### Pushing to a Remote

A **remote** repo is a version of your repository hosted elsewhere typically GitHub, but it can be stored on alternative services or even on an ftp server. So far everything above has been entirely local; nothing leaves your machine until you push.

**Starting a new project and connecting it to GitHub:**

```bash
# Create a repo on GitHub first (via the website), then:
git remote add origin https://github.com/username/repo-name.git
git branch -M main
git push -u origin main
```

**Getting an existing project from GitHub:**

```bash
git clone https://github.com/username/repo-name.git
```
This downloads the full project *and* its entire history in one step, no `git init` needed, it's already a Git repo, can confirm by check `.git` folder.

**Everyday push/pull cycle:**

```bash
git add .
git commit -m "Add feature X"
git push          # send your commits to the remote
git pull          # fetch + merge the latest changes from the remote
```

> [!TIP]
> The `-u` flag in `git push -u origin main` (used only the first time) tells Git to remember this remote/branch pairing, so afterward you can just type `git push` without specifying `origin main` every time.


### Using the GitHub CLI

Everything so far uses plain `git`, which works with any remote host. If you're specifically using **GitHub**, the [GitHub CLI](https://cli.github.com/) (`gh`) lets you do GitHub-specific things such as creating repos, opening Pull Requests, managing Issues, all directly from the terminal, without switching to the browser.

**Install it:**

```bash
# macOS
brew install gh

# Windows (via winget)
winget install --id GitHub.cli

# Linux (Debian/Ubuntu)
sudo apt install gh

# Linux (Fedora)
sudo dnf install gh

# Linux (Arch)
sudo pacman -S github-cli
```

**Authenticate once:**

```bash
gh auth login
```
This walks you through logging in via your browser (recommended) or a personal access token, and handles Git authentication for you going forward, a good alternative to setting up SSH keys manually if you'd rather not.

**Common everyday commands:**

```bash
# Create a new repo on GitHub straight from your terminal
gh repo create my-project --public --source=. --push

# Clone a repo
gh repo clone username/repo-name

# Create an issue
gh issue create --title "Bug: broken link in intro-to-linux.md" --body "Details here"

# List open issues
gh issue list

# Create a Pull Request from your current branch
gh pr create --title "Add GitHub CLI section" --body "Adds a new section covering gh usage"

# List open Pull Requests
gh pr list

# Check out someone else's PR locally to review it
gh pr checkout 42

# View a PR's status/checks
gh pr status
```

**Why it's worth knowing:** for a workflow like this repo, such as forking, branching, committing, opening PRs, `gh pr create` in particular saves a lot of back-and-forth tab-switching, and it's genuinely faster once it becomes muscle memory. It's optional (everything is still possible through the GitHub website), but it fits naturally alongside the Git CLI habits from the rest of this workshop.


### Multiple People Working on the Same Repo

Once a repo has more than one contributor, a few extra habits matter:

- **Pull before you push.** If someone else has pushed changes since you last pulled, Git will reject your push until you `git pull` and reconcile the differences first.
- **`git fetch` vs `git pull`**: `fetch` downloads the latest remote history *without* merging it into your work (lets you look before you leap); `pull` is effectively `fetch` + `merge` in one step.

  ```bash
  git fetch origin
  git log origin/main   # see what's new without merging yet
  git pull              # now actually merge it in
  ```

- **Commit and push often, in small chunks.**: Large, infrequent commits from multiple people dramatically increase the odds of painful merge conflicts.
- **Communicate what you're working on**: A quick message wherever project discussion is happening ("I'm working on the Linux workshop file") avoids two people editing the same section simultaneously.
- **Forking vs. direct collaboration:**: If you have write access to a repo, you typically clone it directly and push branches. If you don't (e.g. contributing to someone else's open-source project), you **fork** it to your own account first, make changes there, and open a Pull Request back to the original.


### Branches

A branch is an independent line of development, a way to work on something (a feature, a fix, an experiment) without touching the stable `main` branch until it's ready.

```bash
# Create and switch to a new branch
git checkout -b feature/new-navbar

# (Newer Git versions, equivalent)
git switch -c feature/new-navbar

# See all branches
git branch

# Switch between existing branches
git checkout main
git switch main

# Push a new branch to the remote for the first time
git push -u origin feature/new-navbar
```

**Why branch instead of just committing straight to `main`?**
- Keeps `main` always in a working, deployable state
- Lets multiple people work on completely different things simultaneously without conflicting
- Lets you experiment freely: if an idea doesn't work out, just delete the branch, `main` is untouched

**Typical workflow:**
1. Create a branch for your specific piece of work
2. Commit your changes there
3. Push the branch and open a **Pull Request** (on GitHub) to propose merging it into `main`
4. Someone reviews it, discussion happens, changes get requested if needed
5. Once approved, it gets merged into `main`


### Merging

Once a branch's work is ready, you bring it back into `main` (or another branch) by merging.

```bash
# Switch to the branch you want to merge INTO (usually main)
git checkout main

# Merge the other branch into your current branch
git merge feature/new-navbar
```

In practice, most teams do this via a **Pull Request on GitHub** rather than merging locally: it adds a review step, a visible diff, and a discussion thread before the code lands in `main`. The underlying Git operation is the same either way.

**Two common merge styles worth knowing about:**
- **Merge commit** (default): Creates a new commit joining the two histories together, preserving the fact a branch existed
- **Squash merge**: Condenses all of a branch's commits into a single commit on `main`, producing a cleaner, more linear history (common for small feature branches with messy in-progress commits)


### Merge Conflicts

A merge conflict happens when Git can't automatically reconcile changes, this usually because two branches modified the **same lines** of the **same file** differently, and Git doesn't know which version is "correct."

**This is normal.** It doesn't mean something went wrong, it just means Git needs a human to make the call.

**What it looks like:**

```
<<<<<<< HEAD
This is the version from your current branch.
=======
This is the version from the branch being merged in.
>>>>>>> feature/new-navbar
```

**How to resolve it:**

1. Run `git status` to see which files have conflicts
2. Open the conflicted file(s), you'll see the `<<<<<<<`, `=======`, `>>>>>>>` markers shown above
3. Manually edit the file to keep the correct content (could be one side, the other, a combination, or something new entirely) and **delete the conflict markers themselves**
4. Stage the resolved file:
   ```bash
   git add filename.txt
   ```
5. Complete the merge with a commit:
   ```bash
   git commit
   ```
   (Git will pre-fill a merge commit message for you, this usually fine to keep as-is)

**Tips for avoiding/minimizing conflicts:**
- Pull frequently so your branch doesn't drift too far from `main`
- Keep branches short-lived and focused on one thing
- Communicate with teammates about who's touching which files
- Most editors (including VS Code) show conflict markers with inline "Accept Current / Accept Incoming / Accept Both" buttons. This is far easier than resolving by hand in a text editor

### Common Beginner Mistakes

- **Committing secrets** (API keys, passwords, `.env` files): Always set up `.gitignore` *before* your first commit, not after
- **Vague commit messages**: "update", "fix", "asdf" tell nobody (including future you) what actually happened
- **Not pulling before pushing**: Leads to unnecessary rejected pushes and confusion
- **Working directly on `main`** for everything: Makes it much harder to keep a stable, deployable version of the project
- **Panicking during a merge conflict**: It's a normal, expected part of collaborative work, not a sign something's broken
- **Force-pushing without understanding the consequences** (`git push --force`): This can overwrite/erase other people's work on a shared branch; avoid it unless you know exactly why you need it


### Where to Go Next

- **Practice platforms**: [Learn Git Branching](https://learngitbranching.js.org/) is an excellent interactive visualizer for branching/merging concepts
- **Documentation**: the [official Git docs](https://git-scm.com/doc) and `git help <command>` (e.g. `git help merge`) for anything beyond the basics
- **Going deeper on GitHub**: code review workflows, GitHub Issues templates, and GitHub Actions (CI/CD) are natural next steps once the core Git and `gh` workflow feels comfortable
- **This very repo**: this repository itself is a great low-stakes place to practice everything from this workshop: fork it, branch, commit, and open a real Pull Request


