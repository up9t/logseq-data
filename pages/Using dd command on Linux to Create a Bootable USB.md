- To easily create a bootable USB, use `Fedora Media Writer` or `Balena Etcher`. But because we're a linux user, we have the opportunity to do it the advance way that is using the `dd` command.
-
- **1.** First of all you need to make sure you have the ISO file downloaded and the USB has already plugged in.
- Then, use this command to list all available block: `lsblk`. Note that the name can be different, for me it's `/dev/sda`.
-
- ```bash
  lsblk
  
  NAME                                          MAJ:MIN RM   SIZE RO TYPE  MOUNTPOINTS
  sda                                             8:0    0 119.2G  0 disk  
  ├─sda1                                          8:1    0     3G  0 part  /run/media/yasa/Fedora-KDE-Live-43
  └─sda2                                          8:2    0    30M  0 part  
  ```
-
- You see I already have the bootable USB, but I'm going to to it again because I have a newer or different ISO file.
-
- **2.** Second is to unmount the USB Drive, this doesn't mean plugged out the USB. You need to execute this command. Note that you need to use `umount` command without the `n` on `un`. And use `sudo`.
-
- ```bash
  sudo umount /dev/sda*
  ```
-
- **3.** Use the `dd` command precautiously, worst case scenario is one wrong mistake and your entire disk will go bye-bye. Note that you need to target the whole disk (`/dev/sda`) not a single partition on it like `/dev/sda1`.
-
- ```bash
  sudo dd if=file.iso of=/dev/sda bs=4M status=progress conv=fsync
  ```
-
- Here's what the command does according to Google:
- `if=/path/to/your.iso`:  The input file.
- `of=/dev/sdX`: The output file. `/dev/sda` is a file on linux representing a disk.
- The remaining arguments are optional:
- `bs=4M` increases the write performance.
- `conv=fsync` ensures that all data is written when the command finishes. and
- `status=progress` shows progress information.
-
- `conv=fsync` is probably important, here's a quick explanation from Google.
- By default, Linux uses an aggressive caching system. When you write data using a command like `dd`, the operating system often stores that data temporarily in system RAM (write cache) and reports the operation as finished, even if the data hasn't actually landed on the physical drive yet.
-
- Here's the command looks like in action:
- ```bash
  sudo dd if=./Fedora-Everything-netinst-x86_64-44-1.7.iso of=/dev/sda bs=4M status=progress conv=fsync
  1170210816 bytes (1.2 GB, 1.1 GiB) copied, 5 s, 232 MB/s1217329152 bytes (1.2 GB, 1.1 GiB) copied, 5.9965 s, 203 MB/s
  
  290+1 records in
  290+1 records out
  1217329152 bytes (1.2 GB, 1.1 GiB) copied, 27.7326 s, 43.9 MB/s
  
  ```
-
- Once finished, safely eject the USB.
-
-
- ## Sources
- https://ubuntu.com/desktop/docs/en/latest/how-to/create-a-bootable-usb-stick/#using-the-linux-command-line
-
- #linux #fedora #command
-