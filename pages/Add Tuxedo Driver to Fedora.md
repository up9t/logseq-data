- Tuxedo Control Center is a tool and a driver to manage hardware like adjusting fan speed manually and automatically, or changing the color of your keyboard RGB in a Tuxedo Laptop. Well I just found out that I'm using a tuxedo laptop, and when I bought it, it uses Windows and have the driver installed by default, but I already change my mind and decided to use Linux, after I boot linux, I need to install the driver manually. Here's how you can do it.
-
- **Add tuxedo repository.**
-
- The repository lives in this website https://rpm.tuxedocomputers.com/fedora/
- After you visit the link, you can navigate it like a file directory, there you can see different fedora versions, and they even have `rawhide` version on Fedora.
- Here's the final url https://rpm.tuxedocomputers.com/fedora/44/x86_64/base/
- You're going to add that url to your `dnf` repo list. But I want the version to be dynamic instead of me hardcoding the number `44` in the url, I'll make it so it follows the version of my system automatically. I can do it by using a variable named `$releasever`, and another variable named `$basearch` to determine our machine architecture such as `x86_64` or `aarch64`.
-
- You can add them manually to the `/etc/yum.repos.d/tuxedo.repo` or you can use an easier way that is stated on their official documentation. Here's you can you do it.
- ```bash
  sudo dnf config-manager addrepo --from-repofile="https://rpm.tuxedocomputers.com/fedora/tuxedo.repo"
  ```
-
- From here you have 2 ways installation:
- Using DKMS (Official Installation)
  logseq.order-list-type:: number
- Using Akmod (Community)
  logseq.order-list-type:: number
-
- More info about DKMS vs Akmod: [[Akmod vs DKMS. Installing Linux Kernel Modules that are out-of-tree.]]
-
- ## 1. Official Install (DKMS)
-
- Let's use the official installation first by using DKMS. **Just install them normally.**
-
- ```bash
  sudo dnf install tuxedo-drivers tuxedo-control-center
  ```
-
- > Note it'll install bunch of dependencies because it uses DKMS.
-
-
- ## 2. Community Install (Akmod)
-
- The reason why I like using Akmod is because it's designed specifically for Fedora and RPM-based distro. And the proprietary Nvidia driver also uses Akmod when you install it [[Add Nvidia Driver in Fedora Linux.]] That way, we're using the existing `akmod` instead of installing `dkms`.
-
- First, you need to add this line `excludepkgs=tuxedo-drivers` in the `/etc/yum.repos.d/tuxedo.repo`. This will make `dnf install` to not install the `tuxedo-drivers` through the official repository, instead we're using the community's `tuxedo-drivers`  that uses `akmod`.
-
- ```bash
  [tuxedo]
  # ...
  # ... other configs
  # ...
  excludepkgs=tuxedo-drivers
  ```
-
- After that, add the Fedora Copr repo. [[Difference between Fedora Copr vs RPM Fusion.]]
-
- ```bash
  # Add copr repository
  dnf copr enable darrencocco/tuxedo-drivers-kmod
  
  # Install
  dnf install tuxedo-drivers tuxedo-control-center
  
  # Reboot after install
  ```
-
-
-
- ## Sources
-
- https://www.linuxtechmore.com/how-to-install-tuxedo-software-on-fedora
- https://www.tuxedocomputers.com/en/Add-TUXEDO-software-package-sources.tuxedo
-
- #driver #linux #fedora