# Introduction to Linux
**Relevant areas:** Linux, Foundations

> [!Note]
> Originally Written by [Ruhan Shafi](https://github.com/RuhanShafi): Last Updated Semester 2 2026

### Table of Content
* [What is Linux?](#what-is-linux)
* [Why should you use Linux?](#why-should-you-use-linux)
* [How to try out Linux without getting rid of your current OS](#trying-out-linux-without-getting-rid-of-your-current-os)
* [Foundations Terminal Commands](#fundamental-terminal-commands)

Linux powers everything from servers to smartphones, yet it's often overlooked by everyday users. This workshop breaks down what Linux actually is and why it's worth exploring — whether you're a programmer looking for a more powerful development environment, a casual user curious about alternatives to Windows, or a creative professional wanting more control over your tools. We'll cover low-risk ways to try Linux without giving up Windows (like live USBs, virtual machines, and dual booting), explain what distros are and how to choose one, and finish with hands-on basic terminal usage so you can start navigating a Linux system with confidence. No prior experience needed - just curiosity.

### What is Linux?

Linux is a free, open-source operating system — the software that manages your computer's hardware and lets everything else run on top of it, similar to Windows or macOS. Unlike those two, Linux isn't owned by a single company; it was originally created by Linus Torvalds in 1991 and has since been built and maintained by a massive global community of developers who contribute to it openly. Because the underlying code is freely available, anyone can inspect it, modify it, and redistribute it — which is why Linux comes in many different "flavors" called distributions (or distros), each tailored for different needs, from beginner-friendly desktops to lightweight servers to specialized tools for programmers. You've almost certainly used Linux without realizing it: it runs the majority of the world's web servers, powers Android phones, and even runs on devices like your router or smart TV. For programmers, it offers powerful command-line tools and a development environment close to what real-world servers use; for everyday users, it offers a fast, customizable, and privacy-respecting alternative to mainstream operating systems.

### Why should you use Linux?

**For Technical Users & Programmers**
Linux is practically the native language of modern development. Most servers, cloud infrastructure, and the tools you'll use throughout your career — Docker, Git, SSH, package managers — were built with Linux in mind, so working in that environment daily closes the gap between what you learn and what you'll actually use on the job. The command line becomes second nature, automation and scripting feel effortless, and you get direct access to system internals without fighting a locked-down OS. For anyone studying software engineering, cybersecurity, or robotics, it's less a lifestyle choice and more a professional advantage.

**For Gamers**
Gaming on Linux has come a long way, largely thanks to tools like Valve's Proton, which lets a huge portion of the Windows game library run smoothly without needing to dual boot or switch systems. Beyond compatibility, many gamers find Linux distros run lighter than Windows, freeing up system resources for better performance on the same hardware. It also appeals to anyone tired of forced updates, background bloat, or invasive telemetry — Linux gives you more control over what's actually running on your machine while you play.

**For Creatives**
Linux offers a genuinely capable, cost-free alternative to expensive creative software suites, with tools like GIMP, Krita, Blender, DaVinci Resolve, and Inkscape covering everything from digital art to 3D modelling to professional video editing. Because the system is so customizable, creatives can strip away distractions and tailor their workspace entirely around their workflow, rather than working around software defaults. It also removes the subscription treadmill many creative tools rely on — once it's installed, it's yours (even though we all know that you pirate Adobe, because after all, it's the morally correct thing to do).

**For Casual/Everyday Users**
For everyday use — browsing, writing, emailing, streaming — Linux offers a fast, clean, and privacy-respecting experience without the ads, forced updates, or data collection that often come bundled with mainstream operating systems. It also breathes new life into older hardware, running noticeably lighter than Windows so a laptop that feels sluggish can feel snappy again. And with beginner-friendly distros like Linux Mint or Ubuntu, the learning curve is far gentler than people expect.

## Trying Out Linux Without Getting Rid of Your Current OS

You don't need to fully commit to Linux to see what it's like — here are a few low-risk ways to try it out:

**1. Live USB**
You can create a bootable USB drive with a Linux distro on it and run the entire OS directly from the USB — without touching your hard drive or installing anything. Just plug it in, boot from it, and you get a fully working Linux environment to explore. Once you're done, just unplug it and reboot back into your normal OS like nothing happened. It's slower than a full install (since it's running off a USB stick) but it's the fastest way to get hands-on.

**2. Virtual Machine (VM)**
Using software like VirtualBox or VMware, you can install Linux "inside" your current operating system as a virtual computer. It runs in a window on your desktop, has its own virtual hard drive, and doesn't affect your host OS at all. This is great for testing things out, practicing terminal commands, or breaking things without any real consequences — you can always just delete the VM and start fresh.

**3. Windows Subsystem for Linux (WSL)**
If you're on Windows, WSL lets you run a real Linux environment (and terminal) directly alongside Windows without a VM or dual boot. It's built into Windows, lightweight, and great for programmers who want Linux command-line tools while still using Windows for everything else.

**4. Dual Boot**
This involves installing Linux alongside your current OS on the same machine, with a boot menu letting you choose which one to load each time you turn on your computer. Unlike a Live USB or VM, this gives you full native performance since Linux runs directly on your hardware — but it also means partitioning your drive, so it's a good idea to back up your data first and follow a guide carefully.

**5. Online/Browser-Based Linux**
For a zero-installation option, there are websites that let you try a Linux terminal or desktop environment directly in your browser (e.g. distrotest.net or similar tools). It's not as fully-featured as running Linux locally, but it's the easiest way to get a quick feel for the interface and commands with literally no setup.

**6. Linux on a Removable SSD**
Another great option is installing Linux fully onto an external/removable SSD rather than your internal drive. You get a real, full-performance Linux installation — not just a live/temporary session like a USB — but your internal drive and current OS remain completely untouched. Simply plug in the SSD, boot from it (usually via your BIOS/boot menu), and you're running Linux natively; unplug it and your computer goes right back to normal. It's a great middle ground between a Live USB (limited and slower) and dual booting (which touches your internal drive) — especially handy if you want to actually use Linux for daily tasks or gaming without any risk to your existing setup, and it's portable enough to take with you and plug into other machines too.

## Fundamental Terminal Commands

**Navigation**
| Command | What it does |
|---|---|
| `pwd` | Prints the current directory you're in (Print Working Directory) |
| `ls` | Lists files and folders in the current directory |
| `ls -la` | Lists all files (including hidden ones) with detailed info |
| `cd <folder>` | Changes directory into the specified folder |
| `cd ..` | Moves up one directory (to the parent folder) |
| `cd ~` | Jumps straight to your home directory |

**Files & Folders**
| Command | What it does |
|---|---|
| `mkdir <name>` | Creates a new folder |
| `touch <file>` | Creates a new empty file |
| `rm <file>` | Deletes a file |
| `rm -r <folder>` | Deletes a folder and everything inside it |
| `cp <source> <destination>` | Copies a file or folder |
| `mv <source> <destination>` | Moves or renames a file/folder |
| `cat <file>` | Prints the contents of a file to the terminal |
| `nano <file>` / `vim <file>` | Opens a file in a terminal text editor |

**Viewing & Searching**
| Command | What it does |
|---|---|
| `less <file>` | Views a file's contents one page at a time (scrollable) |
| `head <file>` | Shows the first 10 lines of a file |
| `tail <file>` | Shows the last 10 lines of a file |
| `grep "text" <file>` | Searches for a specific word/phrase inside a file |
| `find <path> -name "file"` | Searches for files by name within a directory |

**System Info & Permissions**
| Command | What it does |
|---|---|
| `whoami` | Shows the currently logged-in user |
| `sudo <command>` | Runs a command with administrator (root) privileges |
| `chmod <permissions> <file>` | Changes a file's read/write/execute permissions |
| `chown <user> <file>` | Changes who owns a file |
| `ps` | Lists currently running processes |
| `top` / `htop` | Shows live system resource usage (CPU, memory, processes) |
| `df -h` | Shows disk space usage in human-readable form |
| `du -sh <folder>` | Shows the total size of a folder |

**Networking**
| Command | What it does |
|---|---|
| `ping <address>` | Checks if a server/website is reachable |
| `curl <url>` | Fetches data from a URL directly in the terminal |
| `ifconfig` / `ip a` | Shows your network interfaces and IP address |

**Package Management (varies by distro)**
| Command | What it does |
|---|---|
| `sudo apt install <package>` | Installs a package (Debian/Ubuntu) |
| `sudo pacman -S <package>` | Installs a package (Arch) |
| `sudo dnf install <package>` | Installs a package (Fedora) |

**Misc/Utility**
| Command | What it does |
|---|---|
| `clear` | Clears the terminal screen |
| `history` | Shows a list of previously run commands |
| `man <command>` | Opens the manual/help page for a command |
| `exit` | Closes the terminal session |


## Choosing & Getting Started

### Distro Recommendations by Audience

With hundreds of Linux distributions out there, picking one can feel overwhelming — but it really comes down to matching a distro to what you want out of it:

- **New to Linux? → Linux Mint or Ubuntu**
  These are the most beginner-friendly distros around, with straightforward installers, huge community support, and sane defaults out of the box. Almost every "how do I fix X on Linux" guide online assumes Ubuntu, so troubleshooting is easy. Great for casual users and anyone dipping their toes in for the first time.

- **Want something modern and polished? → Fedora**
  Fedora tends to ship newer software and kernel versions than Mint/Ubuntu, giving you a more up-to-date, cutting-edge experience while still being stable and well-supported. It's a great middle ground for people who want modern features without diving into more advanced/DIY territory.

- **Want to really learn how Linux works? → Arch Linux**
  Arch doesn't hold your hand — you install it piece by piece, choosing your own desktop environment, drivers, and tools along the way. It's more hands-on and has a steeper learning curve, but that's exactly the appeal: you come out the other side genuinely understanding your system instead of just using it. Best suited for people who enjoy tinkering or want to deepen their technical skills (this is what I personally run, and it's taught me a lot).

- **Other honorable mentions:**
  - **Pop!_OS** — Ubuntu-based, great out-of-the-box support for gaming and Nvidia GPUs
  - **Debian** — the rock-solid foundation many other distros (including Ubuntu) are built on
  - **Kali Linux** — purpose-built for cybersecurity and penetration testing (relevant for the UC Cybersecurity crowd!)

There's no permanently "wrong" choice here — most people start with something beginner-friendly and naturally migrate toward something more advanced as they get comfortable.

### Desktop Environments

One thing that surprises a lot of newcomers: Linux doesn't have one fixed "look." Unlike Windows or macOS, the desktop environment (DE) that you choose which is the whole visual interface, taskbar, icons, and window behavior, is separate from the OS itself, and you can customize it however you want and even run mutliple swapping to which one you prefer the most. [Here's some of the different ways that you can customize your Linux Desktop](https://www.reddit.com/r/unixporn/)

- **GNOME** — Clean, modern, and minimalist, with a workflow built around full-screen "activities" and virtual desktops rather than a traditional taskbar. Used by default on Ubuntu and Fedora.
- **KDE Plasma** — Highly customizable and visually flexible, closer to a traditional desktop feel (taskbar, start menu-like launcher) but with far more configuration options than Windows offers out of the box.
- **XFCE** — Lightweight and fast, ideal for older hardware or anyone who prefers a snappier, no-frills experience over flashy visuals.
- **Cinnamon** — Mint's default DE, designed to feel immediately familiar to Windows users transitioning over.
- **Hyprland** — A tiling window manager (rather than a traditional DE) that arranges windows automatically instead of letting them float freely — popular with people who want a fast, keyboard-driven, highly customized setup (this is what Dylan and Me personally use).

The takeaway for the audience: installing "Linux" isn't installing one fixed interface — you're choosing a combination of distro *and* desktop environment, and most distros let you install multiple DEs and switch between them at login if you want to swap.

