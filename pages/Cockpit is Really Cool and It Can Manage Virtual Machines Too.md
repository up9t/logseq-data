- `Cockpit` is a general-purpose web-based system administration dashboard for Linux. It can also manage Virtual Machine, Container, and many others. For VM, you can replace `virt-manager` with `cockpit` if you want. Same to container with `podman-desktop`. But it's not really a replacement for them as they don't expose much settings. But, this limitation is actually a great thing, because you can now use CLI when needed instead of relying everything on the UI or everything on the CLI.
-
- Because it's a web-based admin dashboard, you can also use terminal in the browser even from a remote machine if necessary.
-
- Here's how you can install it.
-
- ```bash
  sudo dnf install -y cockpit
  sudo systemctl start cockpit
  ```
-
- After started, you can go to your browser and visit http://localhost:9090
-
- Now if you want it manage virtual machine you need to download another package.
- ```bash
  sudo dnf install -y cockpit-machines
  ```
-
- After installed, you can refresh your browser, and it'll automatically show Virtual Machine menu on the side bar.
-
- This one allows you to manage podman container.
- ```bash
  sudo dnf install -y cockpit-podman
  ```
-
-
- #fedora #linux #sysadmin #dashboard #vm #web
-
-
-
- ## Sources
-
- https://www.redhat.com/en/blog/manage-virtual-machines-cockpit
- https://cockpit-project.org/applications.html
- https://cockpit-project.org/running.html
-