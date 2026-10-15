- When you install out-of-tree linux modules whether using DKMS or Akmod [[Akmod vs DKMS. Installing Linux Kernel Modules that are out-of-tree.]] and you have secure boot enabled, the modules you have installed won't be loaded. That's because you have unsigned modules that was built using DKMS/Akmod, and that's literally the purpose of secure boot, it's to ensure your PC only boots using trusted, digitally signed software.
- To work around this, you need to signed those compiled modules. It's being documented on https://rpmfusion.org/Howto/Secure%20Boot
-
- Install the tools.
-
- ```bash
  sudo dnf install kmodtool akmods mokutil openssl 
  ```
-
- (Optional) then you generate a key with a default value. You do not need to do this step if you already have the `/etc/pki/akmods/private/private_key.priv` and `/etc/pki/akmods/certs/public_key.der` which is usually the case.
- The `private_key.private` is used to signed kernel modules.
- The `public_key.der` is used to verity the module signatures.
-
- ```bash
  # Optional
  sudo kmodgenca -a
  ```
-
- Now, the MOK enrollment, this is the process to make your system trusts the signing certificate. You can test it if it's enrolled. For my case, it's not enrolled, so I have to enroll it.
-
- ```bash
  sudo mokutil --test-key /etc/pki/akmods/certs/public_key.der
  # /etc/pki/akmods/certs/public_key.der is not enrolled
  ```
-
- Enroll with this command, you'll asked to create a password, which then you need to pass it in on boot after reboot, this is a one time password.
-
- ```bash
  sudo mokutil --import /etc/pki/akmods/certs/public_key.der 
  ```
-
- If you test it again, it'll say it's in the request.
-
- ```bash
  sudo mokutil --test-key /etc/pki/akmods/certs/public_key.der
  # /etc/pki/akmods/certs/public_key.der is already in the enrollment request
  ```
-
- Don't reboot yet, after importing the key, you need to tell `akmod` or `dkms` to rebuild the modules so it produces signed modules. Here's using `akmod`.
-
- ```bash
  sudo akmods --force --rebuild --kernels "$(uname -r)"
  # this may take quite some times
  ```
-
- On the next boot, select "Enroll MOK", and Choose "Continue" to enroll key. Then select "Yes" , then "Reboot.
-
-
-
-
- ## References
-
- https://rpmfusion.org/Howto/Secure%20Boot
- https://github.com/EvernightFedora/akmods-evernight/blob/main/README.secureboot
-
- #linux #driver #boot #computer #uefi
-