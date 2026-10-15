- Linux kernel builds upon modules, it has many of them. If the module is within the original linux kernel, we call it `in-tree` kernel module, if it isn't available directly, we call it `out-of-tree` kernel module.
- There are many modules that aren't included in the linux kernel out of the box, most of them because of proprietary reason such as proprietary Nvidia driver, and we know linux is open source. To install an out-of-tree modules, we have 2 ways: using Akmod (Autokernel Module), and DKMS (Dynamic Kernel Module Support). Akmod is primarily designed for rpm-based distro such as Fedora, RHEL, etc. While DKMS supports multiple distro including Debian-based, RHEL-based, and Arch.
  id:: 6acefe7b-4984-47e8-98aa-31aa9ca77764
- Both Akmod and DKMS are used to automatically rebuild out-of-tree kernel modules whenever your system kernel updated. They're not magic, they're basically doing build from scratch package and you need to install multiple development packages into your system like `gcc`, `make`, `kernel-devel`, `kernel-header`, which can make your system bloated with unecessary one-time use only packages/libraries. But we don't have another way.
-
- You need to aware with secure boot too, it you have secure boot enabled, your installed modules probably won't be loaded by the kernel. [[Fixing Linux Drivers with Secure Boot Enabled]]
-
-
- ```mermaid
  flowchart LR
    A[New Kernel Update] --> |DKMS/Akmod| B[Rebuild/Recompile]
  ```
-
-
-
- #linux #fedora #kernel #module #driver #unfinished
-
-