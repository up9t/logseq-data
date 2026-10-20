- If you use Fedora Linux and Nvidia GPU, there is a chance that your Nvidia GPU isn't even used, or at least isn't using it's maximum potential. That's because in order for your system to communicate property with the hardware, you need a piece of program or software called `driver`. In Fedora, I think it has a very basic Nvidia driver installed called nousea, I mean nouveau. It supports very limited feature from your GPU. If you want to use 100% the capability of your GPU, you need to download the official proprietary Nvidia driver for linux.
- One important note, if you use a gaming linux like Bazzite, you might not need to install it manually, because they have it installed for you already.
-
- First thing you need to do is to add RPM Fusion repository [[Difference between Fedora Copr vs RPM Fusion.]] to the `dnf` command. This is the command to do this:
-
- ```bash
  sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
  ```
-
- That command, will add a new file into your `/etc/yum.repos.d` directory. That way `dnf` can look for a package in that repository too. Now install the Nvidia driver.
-
- ```bash
  sudo dnf install akmod-nvidia
  ```
-
- Now, you should have a fully working Nvidia driver. You need to reboot though. And if you have Secure Boot enabled, you have to take an extra step, otherwise it won't work. [[Fixing Linux Drivers with Secure Boot Enabled]].
-
-
-
-
- ## References
-
- https://rpmfusion.org/Howto/NVIDIA
- https://rpmfusion.org/Configuration
-
-
-
- #linux #fedora #setup #module #driver #nvidia #gpu
-
-
-
-