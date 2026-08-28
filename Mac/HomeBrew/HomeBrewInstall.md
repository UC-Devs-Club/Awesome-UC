# How to Install Homebrew on Mac (Intel Based and Apple Silicon Chips)
Relevant Areas: CLI, Mac,

> [!Note]
> Originally Written by [Ruhan Shafi](https://github.com/RuhanShafi): Last Updated Semester 2 2026

### Table of Contents
* [What is a Package Manager?](<HomeBrewInstall#What is a Package Manager?>)
* [What is Homebrew?](<HomeBrewInstall#What is Homebrew?>)
* [Installing Homebrew](#installing-homebrew)
* [Verifying the Install](#verifying-the-install)


### What is a Package Manager?

A package manager is a tool that installs, updates, and removes software for you from the command line instead of manually hunting down installers on random websites, downloading .dmg files, and dragging icons into folders.

Think of it like an alternative to the Apple app store, run entirely through text commands. Instead of:

1. Googling "install Python mac"
2. Finding a download link
3. Downloading an installer
4. Running through a setup wizard

...you just run:

```bash
brew install python
```
and it handles downloading, installing, and setting everything up correctly including any other tools that package depends on to work.

Package managers also make it trivial to update or remove software later, and to keep track of exactly what's installed on your system, all from one consistent interface.

### What is Homebrew?

Homebrew (often just called "brew") is the most popular package manager for macOS, and also runs on Linux (although this is mainly for testing purposes and not to be used instead of your Distro's primary package manager). MacOS doesn't ship with a built-in package manager the way most Linux distros do, so Homebrew fills that exact gap, it's often one of the very first things developers install on a new Mac.

With Homebrew, installing most developer tools, command-line utilities, and even some full applications becomes a single command:

```bash
brew install git
brew install node
brew install --cask visual-studio-code
```

(--cask is used for full GUI applications, rather than command-line tools.)

It's community-maintained, free, and open-source, anyone can contribute new packages ("formulae") to it, which is part of why it has such broad coverage of modern developer tools.

#### Installing Homebrew

Homebrew's installer is a single command, and it works identically regardless of which Mac chip you have — it automatically detects your CPU architecture and installs to the correct location for you.

1. Run the Installer Script
Ensure that your system is up to date before running
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
Follow any on-screen prompts, you may be asked for your password for administer privileges, and possibly to install Apple's Command Line Tools first if you don't already have them (the installer will offer to do this automatically).

#### 2. Add Homebrew to your PATH
 
This is the one step that differs depending on your Mac's chip, since Homebrew installs to a different location on each:
 
| Chip | Install location |
|---|---|
| Intel | `/usr/local/Homebrew` |
| Apple Silicon (M1 and onward) | `/opt/homebrew` |


> [!TIP]
> The installer usually prints the exact command you need at the very end of its output — copy and run that if you see it. Otherwise, use the matching command below.
 
**Apple Silicon (M1/M2/M3/M4):**
```bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```
 
**Intel:**
```bash
echo 'eval "$(/usr/local/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/usr/local/bin/brew shellenv)"
```
 
> [!NOTE]
> If you're using bash instead of the default zsh shell, replace `~/.zprofile` with `~/.bash_profile` in the commands above. You can check which shell you're currently using via the following command `echo $SHELL`
 
## Verifying the Install
 
Confirm everything's working correctly:
 
```bash
brew --version
which brew
```
 
`which brew` should print:
- `/opt/homebrew/bin/brew` on Apple Silicon
- `/usr/local/bin/brew` on Intel

