# Interested in Contributing to Awesome UC, We want you to contribute to the Joint Workshop Repository

Welcome! This repository is a joint effort between **UC DEVS**, **UC ROBO**, and **UC Cybersecurity** — a shared home for workshops, resources, and awesome things curated by the community of IT students across the different IT clubs at the University of Canberra.

Whether you're fixing a typo, adding a new workshop, or contributing resources for your club, this guide will help you get started.

## Ways to Contribute

- **Add or improve a workshop** — slides, agendas, exercises, demo code, or write-ups
- **Curate resources** — tutorials, tools, cheat sheets, or reading material relevant to programming, robotics, or cybersecurity
- **Fix issues** — typos, broken links, outdated instructions, or unclear explanations
- **Suggest ideas** — new workshop topics, structure improvements, or tooling
- **Review contributions** — feedback on open pull requests is just as valuable as code

## Getting Started

1. **Fork** this repository to your own GitHub account
2. **Clone** your fork locally:
   ```bash
   git clone https://github.com/<your-username>/<repo-name>.git
   ```
3. Create a new branch for your contribution:
   ```bash
   git checkout -b your-branch-name
   ```
4. Make your changes
5. Commit with a clear message:
   ```bash
   git commit -m "Add: short description of your change"
   ```
6. Push to your fork and open a **Pull Request** against the `main` branch

## Repository Structure

Please keep contributions organized under the relevant topic, for example:

```
/awesome-uc
  /Foundations
    /LinuxIntro
      README.md
    /ProgrammingIntro
      README.md
  /Networking
    /Proxmox/
      README.md
```

If you're unsure where something belongs, open an issue to ask or mention it in your PR description — a maintainer will help you sort it out.

## Formatting

In every document, ensure you have the following

* A clear title indicating what this page is about
* Relevant subject area
* Original Author and their contact, i.e Github Link
* Any editors
* Table of Content with markdown links

A sample entry should be formatted like this

```markdown
# Title
Relevant areas: Area1, Area2...

>[!Note]
> Originally Written by [Orginal Author](contact link i.e Github): Last Updated - Rough Date is fine
> Authors: Author1, Author2...

### Table of Content
* [Heading Name](#heading-name-in-markdown) #Use LSP
* [Heading 2 Name](#heading2-name-in-markdown)

L
```

## Guidelines

- **Keep it beginner-friendly.** Many contributors and readers are early in their IT journey — explain acronyms and avoid assuming prior knowledge where possible.
- **Credit your sources.** If you're referencing external material, link to it rather than copying it wholesale.
- **Use clear file and folder names.** Prefer `intro-to-linux/` over `workshop2/`.
- **One topic per pull request.** This makes reviews faster and easier to merge.
- **Be respectful.** This is a community space across three clubs — keep discussions constructive and welcoming to all skill levels.

## Pull Request Checklist

Before submitting, please check that:

- [ ] Your branch is up to date with `main`
- [ ] File names and folder structure follow existing conventions
- [ ] Any code included has been tested and runs as expected
- [ ] Markdown files are free of broken links or formatting errors
- [ ] You've added your name/club to the contributor list (if one exists) or workshop credits, if applicable

## Reporting Issues

Found a bug, typo, or outdated instruction? Open an [Issue](../../issues) describing:

- What's wrong
- Where to find it (file/section)
- (Optional) A suggested fix

## Questions?

If anything is unclear, reach out through your club's Discord/Slack, or open a discussion/issue in this repo — someone from UC DEVS, UC ROBO, or UC Cybersecurity will be happy to help.

Thanks for helping build something useful for the UC IT student community! 🎉
