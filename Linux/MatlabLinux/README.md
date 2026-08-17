# How to Install Matlab on Linux
Relevant Areas: Linux

> [!Note]
> Originally Written by [Ruhan Shafi](https://github.com/RuhanShafi): Last Updated Semester 2 2026

### Table of Content

- [Debian Flavoured Distributions - Ubuntu (and Ubuntu Variations such as Kubuntu), Linux Mint](#debian-flavoured-distributions---ubuntu-and-ubuntu-variations-such-as-kubuntu-linux-mint)
- [Fedora and Red Hat Linux](#fedora-and-red-hat-linux)
- [Arch Flavoured Distributions (Arch, EndeavourOS, Manjaro)](#arch-flavoured-distributions-arch-endavouros-manjaro)
  - [Via AUR](#via-aur)
  - [Manual Installer](#manual-installer)
- [NixOS](#nixos)
- [Other](#other)

### Debian Flavoured Distributions - Ubuntu (and Ubuntu Variations such as Kubuntu), Linux Mint

There's no official `.deb` package or apt repository for MATLAB — MathWorks only distributes it as a standalone installer that you download directly from your MathWorks account. The good news is the process is largely distro-agnostic once you have the installer.

> [!NOTE]
> You'll need a valid MathWorks account and license to download and activate MATLAB which is tied under your university credentials .

1. **Install required dependencies first.** MATLAB's GUI installer relies on a handful of system libraries that aren't always installed by default:
   ```bash
   sudo apt update
   sudo apt install libxt6 libxtst6 libxrender1 libxrandr2 libxi6 libxcomposite1 libxcursor1 libnss3 libasound2 unzip
   ```

2. **Download the Linux installer** from your [MathWorks account](https://www.mathworks.com/downloads/) — choose the `.zip` installer for Linux, not the Windows/macOS ones.

3. **Extract and run the installer:**
   ```bash
   unzip matlab_R20XXx_glnxa64.zip -d matlab_installer
   cd matlab_installer
   sudo ./install
   ```
   This launches the graphical installer — sign in with your MathWorks account, select the toolboxes you need, and choose an install location (defaults to `/usr/local/MATLAB/R20XXx`).

4. **Add MATLAB to your PATH** so you can launch it from any terminal:
   ```bash
   echo 'export PATH=$PATH:/usr/local/MATLAB/R20XXx/bin' >> ~/.bashrc
   source ~/.bashrc
   ```

5. **Launch it:**
   ```bash
   matlab
   ```

> [!TIP]
> If the installer window appears blank or fails to render, it's usually a missing GTK/rendering dependency — double check step 1, and try running with `sudo ./install -v` for verbose output to spot what's missing.

### Fedora and Red Hat Linux

Same story as Debian-based distros — no official RPM package, so you're using the same MathWorks-provided installer. The main difference is dependency names and occasionally needing to enable extra repositories for older/32-bit compatibility libraries.

1. **Install required dependencies:**
   ```bash
   sudo dnf install libXt libXtst libXrender libXrandr libXi libXcomposite libXcursor nss alsa-lib unzip
   ```

2. **(Older MATLAB releases only)** some versions expect `libnsl`, which was dropped from newer Fedora/RHEL releases by default:
   ```bash
   sudo dnf install libnsl
   ```

3. **Download, extract, and install** exactly as with Ubuntu:
   ```bash
   unzip matlab_R20XXx_glnxa64.zip -d matlab_installer
   cd matlab_installer
   sudo ./install
   ```

4. **Add MATLAB to your PATH:**
   ```bash
   echo 'export PATH=$PATH:/usr/local/MATLAB/R20XXx/bin' >> ~/.bashrc
   source ~/.bashrc
   ```

> [!NOTE]
> If you're on a fresh minimal Fedora/RHEL install (e.g. a server image or minimal Workstation install), you may also be missing basic X11/desktop libraries the installer assumes are present — installing the `"X Software Development"` group (`sudo dnf groupinstall "X Software Development"`) tends to resolve most missing-library errors in one go.

### Arch Flavoured Distributions (Arch, EndavourOS, Manjaro)

> [!NOTE]
> Like all things Arch, the best place to look first is the Arch Wiki, the partiular page for getting Matlab working on arch can be found [here](https://wiki.archlinux.org/title/MATLAB)

#### Via AUR

Arch Linux isn't an officially supported distribution for MATLAB, so you'll still need a valid MathWorks license — but the community maintained **MATLAB Package Manager (MPM)** is the recommended and most robust way to get it installed, since it automates fetching both MATLAB itself and any toolboxes you select.

> [!NOTE]
> The standard graphical MATLAB installer does not officially support Wayland. If you're on a Wayland session, MPM is effectively the only supported install path, additionally MATLAB itself will additionally need `xorg-xwayland` to actually run.

1. **Install `matlab-mpm` from the AUR** (replace `yay` with your preferred AUR helper):
   ```bash
   yay -S matlab-mpm
   ```

   > [!NOTE]
   > As of `matlab-mpm` version `1:2026.4+r147.g87963d3-1` and later, the package no longer provides a `/usr/bin/mpm` symlink (to avoid conflicting with `meta-package-manager`). Use `matlab-mpm` as the command instead of `mpm` below.

2. **(Optional) Install `matlab-mpm-input`**, which provides the template input files listing the correctly formatted product/toolbox names MPM expects:
   ```bash
   yay -S matlab-mpm-input
   ```

3. **Run MPM to install MATLAB and any toolboxes you need**, specifying the release and a destination folder. For example, to install MATLAB R2021b along with a few toolboxes:
   ```bash
   matlab-mpm install --release=R2021b --destination=~/matlab MATLAB Simulink Deep_Learning_Toolbox Parallel_Computing_Toolbox
   ```
   This step does **not** require signing in, a File Installation Key, or a pre-acquired license file — MPM defers all activation and licensing to after installation.

4. **Activate your license.** If you're using an Academic Online License, run:
   ```bash
   ~/matlab/bin/glnxa64/MathWorksProductAuthorizer.sh
   ```
   and sign in with your MathWorks/university-linked account when prompted.

> [!TIP]
> There's also a [`matlab`AUR](https://aur.archlinux.org/packages/matlab) package that integrates MATLAB more tightly into Arch's package management (handling dependencies and some installation nuances for you). However, due to MATLAB's EULA prohibiting redistribution of the installation files, that package **cannot** bundle the installer itself. Rather you're expected to manually place your own MathWorks-obtained installation files into the cloned AUR package's folder and compile the package yourself, rather than installing it directly through an AUR helper, this also has the side effect of taking forever. For most people, MPM above is the simpler route.

#### Manual Installer

If you'd rather not go through the AUR (or `matlab-mpm` doesn't cover the toolbox/version you need), you can run the official MathWorks installer directly, same as on Debian/Fedora. Arch Linux just doesn't ship the dependency libraries by default, so you'll need to grab them yourself.

1. **Install required dependencies:**
   ```bash
   sudo pacman -S libxt libxtst libxrender libxrandr libxi libxcomposite libxcursor nss alsa-lib unzip
   ```

2. **Download, extract, and run the installer** as usual:
   ```bash
   unzip matlab_R20XXx_glnxa64.zip -d matlab_installer
   cd matlab_installer
   sudo ./install
   ```

3. **Add MATLAB to PATH:**
   ```bash
   echo 'export PATH=$PATH:/usr/local/MATLAB/R20XXx/bin' >> ~/.bashrc
   source ~/.bashrc
   ```

> [!TIP]
> The AUR/MPM route above is generally less painful on Arch since it handles a lot of this dependency wrangling for you — only reach for the manual installer if MPM doesn't support what you need.

### NixOS

NixOS is a special case because of its non-standard filesystem layout. There's no `/usr/lib`, `/lib`, etc. in the locations MATLAB's installer expects, so running the installer directly will fail with missing library errors even if the packages are technically installed via Nix.

The standard workaround is to run the installer (and MATLAB itself) inside an **FHS-compatible environment** using `buildFHSUserEnv`, which creates a sandboxed environment that looks like a traditional Linux filesystem to the installer.

1. **Create a `shell.nix`** with an FHS environment containing the libraries MATLAB needs:
   ```nix
   { pkgs ? import <nixpkgs> {} }:

   (pkgs.buildFHSUserEnv {
     name = "matlab-fhs";
     targetPkgs = pkgs: (with pkgs; [
       xorg.libXt
       xorg.libXtst
       xorg.libXrender
       xorg.libXrandr
       xorg.libXi
       xorg.libXcomposite
       xorg.libXcursor
       nss
       alsa-lib
       unzip
       glibc
     ]);
     runScript = "bash";
   }).env
   ```

2. **Enter the environment and run the installer as normal:**
   ```bash
   nix-shell shell.nix
   unzip matlab_R20XXx_glnxa64.zip -d matlab_installer
   cd matlab_installer
   sudo ./install
   ```

3. **To launch MATLAB later**, you'll need to re-enter the FHS shell each time (or wrap it in a script/desktop entry that does so automatically):
   ```bash
   nix-shell shell.nix --run matlab
   ```

> [!NOTE]
> This is more setup than other distros, but it's the same underlying trick used for other FHS-assuming proprietary software (Steam, VS Code extensions with native binaries, etc.). If you've dealt with `buildFHSUserEnv` before for something else, this will feel familiar.

### Other
I'm going to be frank; You're on your own, if you do find a way, be sure to edit page and open pull request.
