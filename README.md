#Raspberry Router
This is a tool-set used to do something with our campus network in Nanjing University.
##Features
###VPN Server Located in Campus Network
Acessing electronical databases bought by the Library of Nanjing University is quite a bonus for us to do some research on anything we are interested in. Theoretically, we can have free access to those databases anywhere on campus. However, when using computers assigned to us by the institute, we can't visit any database.

As is known to all, the network in our labs is supervised by Software Institute itself. It is obvious that the library does not offer enough permission for our institute's export IP address. However, we can play some tricks on the network as if we were searching the database in our dormitory when seated in the labs located in Fei Yiming Building.

In my plan, this function will work with the help of **a DDNS service**. What we need to do is **set up a VPN server** on Rasperberry Pi. Out of convenience, the VPN server had better support both PPTP and L2TP protocol.
###Wireless Router in Dormitory
One of my roommates left the dormitory once the final exam of Software Process and Management finished. Unfortunately, he went away with everything he could bring, **including the wireless router**...

So, we need a new wireless router to enjoy ourselves.

I reject the proposal that we should buy a new router. Instead, I want to build a wireless router based on Raspberry Pi. After all, to build a VPN server, we have owned a Raspberry Pi. Usually, the hardware of a normal wireless router on sale is much worse that that of a Raspberry Pi! We can obtain better network performance on it, maybe.

OpenWRT is a simple solution to turning Raspberry Pi to a wireless router, but that is not my purpose. If we install OpenWRT, VPN server can't be built on the Raspberry Pi at the same time. So, the wireless router still needs to be set up on a more usual Linux distribution, for example, Raspbian.
##Memo
###2015-11-25
* Orders have been made tonight. When everything is ready, we can set about trying.
* I have had a wireless NIC, and luckily, it is chipped with Ralink 3070. Therefore, I don't need to pay attention to its driver any more.  
*If you don't know what NIC to buy, this website may help you.*  
Link: [支持树莓派的USB WiFi网卡](http://shumeipai.nxez.com/2013/08/25/usb-wifi-nic-for-pi.html)
