## Introduction
-
- Have you ever tried to download a specific software on Fedora through `dnf install` command, but there is no package like that available?
- We first need to now know `dnf install` searches for a package and installs it. It works by using repository. Repository is like an library where you can find all of the packages. So Repository A might not contains a package you asked for, but Repository B has it. So, `dnf` will search in all of the repositories that are available on your computer one by one just to find that specific package you want to download. The list of repositories where `dnf` will search, usually inside the `/etc/yum.repos.d/` directory.
- If you want to download a software that is not available on all of the current repository lists. You might want to add another repository manually, so that your `dnf install` command can find the package in that new repository.
- To add your own repository, you need to create a new file called `yourreponame.repo` inside the `/etc/yum.repos.d`. For example, if you want to install Visual Studio Code (VSCode), you need to add a file named `vscode.repo` with this content:
-
- ```bash
  # cat vscode.repo 
  [code]
  name=Visual Studio Code
  baseurl=https://packages.microsoft.com/yumrepos/vscode
  enabled=1
  autorefresh=1
  type=rpm-md
  gpgcheck=1
  gpgkey=https://packages.microsoft.com/keys/microsoft.asc
  
  ```
-
- If you take a closer look at the `baseUrl` section, it's a link to `https://packages.microsoft.com/yumrepos/vscode`, that is Microsoft own's repository.
-
- Same goes with Fedora Copr and RPM Fusion, both are also repositories to install third party software. They're official from Fedora. Fedora Copr is used for individual developers who want to publish their own software, while RPM Fusion is usually for Proprietary driver published by companies such as the Nvidia driver through it's non-free repositories, though it has free repository for publishing open source software too.
-
- For example using RPM Fusion, if you want to download an proprietary official Nvidia driver [[Add Nvidia Driver in Fedora Linux.]] , you install a package named `akmod-nvidia` using `dnf install` command, but `dnf` can't find a package named `akmod-nvidia` through all of the repositories you have in your `/etc/yum.repos.d`. The official documentation says you need to add both free and non-free RPM fusion repositories.
-
- ```bash
  sudo dnf install akmod-nvidia
  # failed because you don't have repositories that have akmod-nvidia
  
  # after adding the RPM Fusion repository
  sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
  
  sudo dnf install akmod-nvidia
  # success, then reboot your computer
  ```
-
- The choice between RPM Fusion and Fedora Copr depends on the publishers in which they want to publish their software.
- For Fedora Copr, you use `dnf copr` command. For example, you want to add a repository from a specific developer, you use this syntax:
-
- ```bash
  sudo dnf copr enable <copr-owner>/<project-name>
  ```
-
- An example here, I want to install a `tuxedo-drivers` using `akmod`. Because the official is using `dkms`. I add the repo, make sure you follow their instruction, for example here, I also need to add the official `tuxedo` repository first, and exclude a package named `tuxedo-drivers` as told in the documentation.
-
- ```bash
  dnf copr enable darrencocco/tuxedo-drivers-kmod
  dnf install tuxedo-drivers tuxedo-control-center
  
  # reboot
  ```
-
-
-
-
- ## References
-
- https://rpmfusion.org/Configuration
- https://copr.fedorainfracloud.org/coprs/darrencocco/tuxedo-drivers-kmod
-
- #fedora #linux #driver
-
-