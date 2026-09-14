- Let's say you have a small team of 2, you and your friend, you create the Backend and your friend creates the Frontend, your friend want to consume the API you create, and you the backend already run the server with `npm run dev` or `php artisan serve` or a similar command. How can you share that to frontend without paying and installing any tools? It's pretty simple, here's how.
-
- First step is to make sure you and your friend are on the same connected network, this can mean you and your friend using the same wifi, or you or your friend provide a hotspot and the other person connect it from their computer.
  logseq.order-list-type:: number
- Once connected, you will get an IP address, the Frontend person need to use the Backend person IP address, to do operation like `fetch()`. But how do you know the Backend's IP address?
  logseq.order-list-type:: number
- You can do it in many ways, if you're on linux you can utilize command like `ip address` or `nmcli device show`. But the easiest way that works on both `linux` and `windows`, both frontend and backend is to see it through the wifi settings.
  logseq.order-list-type:: number
- On the wifi settings whether you're using linux or windows, you will see an IPv4 Address and an IPv6 address, you can use IPv6 as well for the `fetch()` function, but most of the time, you just need to use the IPv4 address. e.g `fetch("http://192.168.1.4/yourapi")`.
  logseq.order-list-type:: number
- We have three different possibilities:
  logseq.order-list-type:: number
	- You and Your friend connect to the same wifi.
	  logseq.order-list-type:: number
	- You (Backend) make a hotspot wifi, so your friend (Frontend) can connect.
	  logseq.order-list-type:: number
	- You (Frontend) make a hotspot wifi, so your friend (Backend) can connect.
	  logseq.order-list-type:: number
- First possibility is the easiest, after connected to the wifi, tell the backend person to go to the wifi settings, that IP is the IP address the frontend person is going to use. Done.
  logseq.order-list-type:: number
- Second possibility, the frontend is connected to the backend's wifi, just tell the frontend to go to the wifi settings, and use the `default gateway` / `default route` IP address. Done.
  logseq.order-list-type:: number
- Third possibility, the backend is connected to the frontend's wifi, same step as the first possibility, backend person go to the wifi settings, see the IPv4 address, tell the frontend to use it. Done.
  logseq.order-list-type:: number
- Here's the thing, IP address only exists when you connected to a network. You probably will have a different IP address when connected to other wifi. You need to see the IP manually everytime, so don't switch wifi frequently.
  logseq.order-list-type:: number
- If the backend doesn't change wifi frequently, here's a tip for you, go to the wifi settings, you're going to set a static IP address instead of DHCP (automatic), so your IP stays the same as long as you use this wifi. Set the wifi to whatever you like as long as you follow the `default gateway` IP, for example if the `default gateway` IP is 192.168.1.1 you probably can change the last digit after (dot) to whatever you like in range of 1 to 255, like `192.168.1.53` just make sure or hope that no other people already use this IP you've just assigned. After that the frontend should use this IP address for the `fetch()` function without having to worry it change as long as you both are on the same wifi or still connected to the same network.
  logseq.order-list-type:: number
-
- #network #web