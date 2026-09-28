- After doing reinstall, first is I want to install Firefox so that I could troubleshoot problems more easily, but before that I need to make my wifi and mouse working. I use bluetooth to connect my mouse. Wireless connection doesn't available at the moment.
-
- ## Fixing the wifi issue
- To fix the wifi, we need to know what causes the problem, so I use dmesg, and know I know that it looks for a file named `iwlwifi-so-a0-hr-b0-89`.
-
- ```bash
  sudo dmesg | grep -i 'wifi'
  [   17.780202] iwlwifi 0000:00:14.3: Detected crf-id 0x1300504, cnv-id 0x80400 wfpm id 0x80000030
  [   17.780244] iwlwifi 0000:00:14.3: PCI dev 51f0/0074, rev=0x370, rfid=0x10a100
  [   17.780247] iwlwifi 0000:00:14.3: Detected Intel(R) Wi-Fi 6 AX201 160MHz
  [   17.780422] iwlwifi 0000:00:14.3: Direct firmware load for iwlwifi-so-a0-hr-b0-89.ucode failed with error -2
  [   17.780426] iwlwifi 0000:00:14.3: no suitable firmware found!
  [   17.780427] iwlwifi 0000:00:14.3: iwlwifi-so-a0-hr-b0-89 is required
  [   17.780428] iwlwifi 0000:00:14.3: check git://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git
  ```
-
- Then I ran the command `dnf provides` to find for a package that has this file.
-
- ```bash
  dnf provides '*/iwlwifi-so-a0-hr-b0-89.ucode*'
  Waiting for a lock on the system repository; another process is currently accessing it. Use the "--skip-file-locks" option to bypass the lock.
  Updating and loading repositories:
   Fedora 44 openh264 (From Cisco) - x86_64                                                                                             100% |   2.5 KiB/s |   7.3 KiB |  00m03s
   Fedora 44 - x86_64 - Updates                                                                                                         100% | 522.9 KiB/s |  26.5 MiB |  00m52s
   Fedora 44 - x86_64                                                                                                                   100% | 482.2 KiB/s |  56.9 MiB |  02m01s
  Repositories loaded.
  iwlwifi-mvm-firmware-20260916-1.fc44.noarch : MVM Firmware for Intel(R) Wireless WiFi adapters
  Repo         : updates
  Matched From : 
  Filename     : /usr/lib/firmware/intel/iwlwifi/iwlwifi-so-a0-hr-b0-89.ucode.xz
  Filename     : /usr/lib/firmware/iwlwifi-so-a0-hr-b0-89.ucode.xz
  
  iwlwifi-mvm-firmware-20260309-1.fc44.noarch : MVM Firmware for Intel(R) Wireless WiFi adapters
  Repo         : fedora
  Matched From : 
  Filename     : /usr/lib/firmware/intel/iwlwifi/iwlwifi-so-a0-hr-b0-89.ucode.xz
  Filename     : /usr/lib/firmware/iwlwifi-so-a0-hr-b0-89.ucode.xz
  ```
-
- Then install it
- ```bash
  sudo dnf install -y iwlwifi-mvm-firmware
  ```
- Then reboot, now everything should be okay.
-
- ## Using nmcli to manage wifi connection.
-
- Because I don't have a GUI to manage the wifi connection, I'll have to use what I have which are `NetworkManager` and `nmcli`, `nmcli` itself is the frontend cli that relies on `NetworkManager`.
-
- ```bash
  # turn on wifi radio signal.
  nmcli radio wifi on
  
  # scan wifi signal and you'll see list of wifi and use the ssid.
  nmcli dev wifi 
  
  # connect the wifi, enter and you'll need to type the wifi password.
  nmcli dev wifi connect "WIFI_SSID" --ask
  ```
-
- Now, this command will add a wifi setting GUI to the KDE setting.
- ```bash
  sudo dnf install -y plasma-nm
  ```
-
- ## Fixing the bluetooth issue
-
- I need to install the `bluez`. And optionally the `bluedevil` which is the frontend GUI for `bluez` for KDE.
- ```bash
  sudo dnf install bluez bluedevil
  ```
- Then a bluetooth section will appear in your KDE settings. As far as I'm concerned, you need to fix the wifi first.
-
- ## Fixing Audio?
-
- I want to fix Audio issue by manually installing `pipewire` and `alsa` but it's already there when I installed `plasma-desktop`. So I don't need to fix anything which is not what I want, I'll let it slide because I've been troubleshooting wireless connection quite a while.
-
- Next thing is to install File Manager, because I use KDE, `dolphin` is the preferred option.
-
- ```bash
  sudo dnf install -y dolphin
  ```
-
-
-
- #linux #fedora #setup