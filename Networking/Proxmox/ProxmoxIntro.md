# Introduction to Homelabbing, Virtualization and Proxmox

### Table of Contents
* [What is Homelabbing](<ProxmoxIntro#What is Homelabbing?>)
  * [Why should you create your own Home Lab](<ProxmoxIntro#Why should you create your own Home Lab?>)
* [What is Virtualization](<ProxmoxIntro#What is Virtualization?>)
* [What is a Hypervisor](<ProxmoxIntro#What is a Hypervisor?>)
* [What is Proxmox VE](<ProxmoxIntro#What is Proxmox VE?>)

### What is Homelabbing?

"Homelabbing" is the hobby (and, for many, an ongoing skill-building practice) of running and hosting your own servers, services, and infrastructure at home (hence the name and the direct definition, however in a more general sense, it's most things that aren't commercial and/or enterprise) by using spare or dedicated hardware to host things yourself instead of relying entirely on commercial cloud services. It ranges from something as simple as a single Raspberry Pi running one small service, all the way up to full server racks running dozens of VMs and containers running different services such as reverse proxies, Network Attached Storage solutions, media servers, dedicated game server, render farms and more. This workshop will be focused on setting up Proxmox as it's scablable as your hardware and demands grow alongside your knowledge.

#### Why should you create your own Home Lab?

* **Skill Growth**
This is the most direct benefit for anyone studying IT, especially Cybersecurity and Networking: A home lab gives you a safe, low-stakes environment to actually practice the things you're learning in lectures such as networking, systems administration, Linux, virtualization and security. It's the difference between reading about DNS and actually standing up your own DNS server and watching it break, then fixing it yourself. For cybersecurity-focused students specifically, a home lab is also where you'll build isolated environments for practicing attacks, defenses, and network segmentation without touching production systems or breaking any rules.
* **A Genuine Portfolio/Resume Talking Point**
Beyond the direct skills, a home lab is something concrete you can point to and talk about in an interview and often technical recruiters will be deliated to hear about. Saying that you "...run a Proxmox cluster with X VMs handling Y and Z" is a real, demonstrable signal that you've gone beyond coursework and actually built and maintained infrastructure on your own initiative. It tends to stand out to recruiters since you using software that you'll be using in the field.
* **Digital Sovereignty & Privacy**
Every commercial cloud service you use such as file storage, photo backups, password managers, media streaming, and even commercial DNS providers are services where a company holds your data, sets the terms, and can change pricing, features, or availability at any time. Homelabbing lets you take some of that back: hosting your own file storage, your own password manager, your own media server, or your own DNS-level ad blocker means your data stays on hardware you physically control, under rules you set. Remember that there is no such thing as the "Cloud", it just someone else's computer!
* **Convenience**
Beyond the principle of it, self-hosting is often offer better services compared to many commercial options. Running your own media server means your content is organized exactly how you want, with no algorithm or subscription gate involved. Running your own network-wide ad blocker (like Pi-hole) benefits every device on your network automatically, with no per-device app needed. A home lab becomes infrastructure that quietly makes your actual daily computer use better, not just a learning exercise that sits idle.

### What is Virtualization?

Virtualization is the ability to run multiple independent, isolated "computers" on a single physical machine. Each of these virtual computers referred to as a virtual machine (VM), behaves exactly like a real one: it has its own operating system, its own allocated CPU, RAM, and storage, and thinks it's running on its own dedicated hardware, even though it's actually sharing the same physical box with several others.

This might sound abstract, but you've almost certainly used virtualization already without necessarily calling it that. A lot of university computer labs run virtualized environments, cloud platforms like AWS/Azure/GCP are built entirely on it, and even your own laptop might run a VM if you've ever used something like VirtualBox for a uni subject.

Now you may be asking why it matters here specifically for home labbing and self hosting services, well the answer is that instead of needing five physical computers to experiment with five different setups (a web server, a firewall, a test environment, a Linux distro you're curious about, a vulnerable machine to practice on), virtualization lets you run all five on one piece of spare hardware, safely isolated from each other and from your everyday devices.

For anyone leaning cybersecurity/networking: this is also exactly how you'll safely run intentionally vulnerable machines, test exploits, or simulate a network topology without ever putting your actual devices at risk — virtualization is the backbone of basically every home lab, CTF practice setup, and pentesting range you'll come across.

### What is a Hypervisor?

A hypervisor is the software layer that actually creates and manages virtual machines and it's what sits between your physical hardware and the VMs running on top of it, handing out slices of CPU, memory, and storage to each one.

There are two fundamentally different types, and the distinction matters a lot for what we're doing today:

* **Type 2 (Hosted) Hypervisors**
Software that runs on top of a regular operating system, like an app. Examples: VirtualBox, VMware Workstation. You install Windows or Linux like normal, then install VirtualBox on top, and run VMs from within that. This is what most people have used in a university lab setting.
* **Type 1 (Bare-Metal) Hypervisors**
Software that is the operating system. There's no separate host OS underneath and the hypervisor installs directly onto the physical hardware and IS what boots up. Examples: Proxmox VE, VMware ESXi, Microsoft Hyper-V (server edition). This is what real data centers, cloud providers, and enterprise IT environments run on.

Why this distinction matters in the context of this workshop and Homelabbing in general: Type 2 hypervisors are fine for quick testing, but they're inherently limited since you're competing with a full host OS for resources, and it's not how production infrastructure actually works. Proxmox being Type 1 means what you learn today directly mirrors real enterprise and cloud infrastructure, not just a desktop convenience tool. This is the difference between "I fiddled with VMs once for an assignment" and "I understand how actual infrastructure is provisioned", a distinction that matters a lot if you're talking to a recruiter or a technical interviewer later.

### What is Proxmox VE?

Proxmox Virtual Environment (Proxmox VE) is a free, enterprise-grade, open-source, Debian-based Type 1 hypervisor platform. What makes Proxmox enterprise-grade and also a very commonly used for self-hosting is that it's not just a hypervisor, but a full management layer on top, with a web-based dashboard for controlling everything: creating VMs, managing storage, configuring networks, setting up backups, and monitoring resource usage, all without needing to memorize command-line syntax for every action (though the CLI is always there if you want it).

It's genuinely used in production by real organizations from small businesses, ISPs, and increasingly larger enterprises use Proxmox as a free alternative to expensive licensed platforms like VMware vSphere. This isn't "toy software for hobbyists that happens to look professional" but rather it's the real thing, which is exactly why it's such a strong skill to have hands-on experience with before you graduate.

For IT students broadly, Proxmox is a genuinely gentle on-ramp into systems administration and infrastructure concepts since you get a browser-based interface to learn on, while still building real, transferable skills underneath. For cybersecurity/networking students specifically, it's also the natural foundation for building an isolated lab network: multiple VMs, virtual networks between them, and the ability to safely simulate real-world topologies (attacker machine, target machine, firewall, segmented VLANs) entirely on one physical box.

#### VMs vs. Containers

Proxmox supports two different kinds of virtualization, and knowing when to reach for each is a core practical skill:

**Virtual Machines (VMs)**: full virtualization, using a technology stack called QEMU/KVM. Each VM runs its own complete, independent operating system (its own kernel, its own everything), fully isolated from the host and from other VMs. This is the most "real" form of isolation, a VM genuinely doesn't know it's not on physical hardware. Less useful for self-hosting but is excellent for malware analysis

**Use when**: you need a different OS than the host (e.g. running Windows on a Linux Proxmox host), you need strong security isolation, or you're simulating a real standalone machine (a common need in cybersecurity labs).

**Containers (LXC)**: lightweight, OS-level virtualization. Rather than virtualizing entire hardware and running a full separate kernel, containers share the host's kernel and isolate everything else (processes, filesystem, networking). This makes them dramatically faster to start, and far lighter on resources.
**Use when**: you're running a Linux-based service or app and don't need a different OS or kernel, e.g. hosting a website, a database, or a self-hosted app. This is closer to (though not identical to) the same underlying idea behind Docker, if you've encountered that term before.

The practical trade-off: VMs give you maximum isolation and flexibility at the cost of resource overhead; containers give you speed and efficiency at the cost of being tied to the host's kernel/OS family. On "spare hardware" with limited RAM/CPU, this distinction directly affects how much you can actually run at once, a big part of getting real value out of a home lab is knowing which one to reach for, for a given task.
