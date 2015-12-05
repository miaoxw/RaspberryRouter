#Raspberry Router
This is a tool-set used to do something with our campus network in Nanjing University.
##Features
###~~VPN Server Located in Campus Network~~(Abandoned)
Acessing electronical databases bought by the Library of Nanjing University is quite a bonus for us to do some research on anything we are interested in. Theoretically, we can have free access to those databases anywhere on campus. However, when using computers assigned to us by the institute, we can't visit any database.

As is known to all, the network in our labs is supervised by Software Institute itself. It is obvious that the library does not offer enough permission for our institute's export IP address. However, we can play some tricks on the network as if we were searching the database in our dormitory when seated in the labs located in Fei Yiming Building.

In my plan, this function will work with the help of **a DDNS service**. What we need to do is **set up a VPN server** on Rasperberry Pi. Out of convenience, the VPN server had better support both PPTP and L2TP protocol.
###Proxy Server Located in Campus Network
I faced a HUGE problem when setting up VPN server with DDNS. So, I turned to a simpler way to solve it.

With a HTTP proxy, all our HTTP request are forwarded by Raspberry Pi. Additionally, since Pi is located in dormitory, it is absolutely problem-free to have access to those databases.

Proxies can be set up as a transparent one, but with the limit of free DDNS traffic, **a normal positive-direction proxy** is more suitable.
###Wireless Router in Dormitory
One of my roommates left the dormitory once the final exam of Software Process and Management finished. Unfortunately, he went away with everything he could bring, **including the wireless router**...

So, we need a new wireless router to enjoy ourselves.

I reject the proposal that we should buy a new router. Instead, I want to build a wireless router based on Raspberry Pi. After all, to build a VPN server, we have owned a Raspberry Pi. Usually, the hardware of a normal wireless router on sale is much worse that that of a Raspberry Pi! We can obtain better network performance on it, maybe.

OpenWRT is a simple solution to turning Raspberry Pi to a wireless router, but that is not my purpose. If we install OpenWRT, VPN server can't be built on the Raspberry Pi at the same time. So, the wireless router still needs to be set up on a more usual Linux distribution, for example, Raspbian.
##Memo
###2015-12-06
* The DIY router doesn't seem to have a wonderful stabilty...
* If Raspberry Pi runs for over 48 hours, its throughput decreses dramatically. Once it is restarted, the performance goes back to the normal level.  
*The result remains to be investigated.*

###2015-12-01
* VPN doesn't work... Port mapping is a HUGE problem.
* I wonder wether a transparent HTTP proxy works?
* Yes, a proxy works.  
*And the proxy solved the problem that CSS style sheets of GitHub can't be loaded in the laboratory.*

###2015-11-30
* My high-power NIC is a bit too large for my crowded desktop, so I substituted it with a mini-sized one. Luckily, it also works without any additional process with its driver.
* 54Mbps is a little sad to me. Making my router support IEEE 802.11n is in the To-do list now.

###2015-11-25
* Orders have been made tonight. When everything is ready, we can set about trying.
* I have had a wireless NIC, and luckily, it is chipped with Ralink 3070. Therefore, I don't need to pay attention to its driver any more.  
*If you don't know what NIC to buy, this website may help you.*  
Link: [支持树莓派的USB WiFi网卡](http://shumeipai.nxez.com/2013/08/25/usb-wifi-nic-for-pi.html)
