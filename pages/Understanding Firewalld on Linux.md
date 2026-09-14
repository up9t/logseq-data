- `Firewalld` is a firewall that runs on linux, usually on Red Hat based linux distro such as Fedora. It provides a higher level way to manage firewall inside linux, it is built on top of nftable which provides the lower level management. Firewalld alternative is UFW, it's the default choice on Debian based distribution like Ubuntu and Linux Mint.
-
- Before we dive into `firewalld`, we first need to have a basic understanding of what is a firewall.
-
- ## What is a firewall?
-
- Firewall is a  piece of software that runs inside your operating system to provide a security mechanism that is  by blocking a traffic coming in from other devices whether those devices are from your local network or from the internet. You can customized it to allow what traffic can go in to you device.
-
- ## How to configure firewall?
-
- You can use software that provides high level firewall management like firewalld, ufw. Or you could use the lower level ones like iptables or nftables.
-
- ## Using Firewalld
-
- Using firewalld is pretty straightforward, you first need to make sure that you have firewalld installed on your machine, and then check if the service is running by using systemctl command.
-
- **Check if firewalld is running.**
-
- ```bash
  systemctl status firewalld
  ```
-
- An example here, I want to run an HTTP server on my machine running on port 8080, and I will use `podman` to do it. And then I want to access the HTTP server from my other device inside my Local Area Network (LAN) by using IPv4 address.
-
- **This will open up port 8080 to run HTTP server**
-
- ```bash
  podman run --rm -p 8080:80 nginx:1.31-alpine
  ```
-
- **I need to get my computer IP address**
-
- ```bash
  ip addr
  ```
-
- **On my other device, I will put that IP address with the server port on my browser search bar**
-
- ```text
  http://192.168.1.9:8080
  ```
-
- **If I have firewalld running, I won't be able to access the server**
-
- The next thing I need to do is configuring my firewall configuration so that other devices can access my server. I will do it by simply telling/configuring the firewall to allow traffics from other device entering my computer on port 8080.
-
- ```bash
  # list current firewall configuration
  sudo firewall-cmd --list-all
  
  # Open port 8080, permanent means keep this port open upon restart
  sudo firewall-cmd --add-port=8080/tcp --permanent
  
  # Don't forget to reload
  sudo firewall-cmd --reload
  ```
-
- Now you can access your server from your other devices.
-
- ## Flag --add-port vs --add-service
-
- You can use `--add-service` as a replacement for `--add-port` the difference are :
-
- You need to know the service name to open that service port. For example `--add-service=http` means open up port 80 which is the same as `--add-port=80/tcp.`
  logseq.order-list-type:: number
- You can't use `--add-service` if you have an HTTP port running on custom port other than 80, just like the example I gave you above.
  logseq.order-list-type:: number
-
- #firewall #linux #fedora
-
-