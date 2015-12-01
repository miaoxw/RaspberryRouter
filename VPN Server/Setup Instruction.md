#Setup Instruction
In Linux, we have many open-sourced VPN servers. Choose any of them can fulfill our needs. In this instruction, we will use `pptpd` as the service provider.

##Install necessary packages
###Install `pptpd`
Just install `pptpd` with the following command:

	sudo apt-get install pptpd

###Configure the server
* Open `/etc/pptpd.conf` to make some modification.  
In this configuration file, changing only the bottom part of it is enough. We can assign an IP for the server(our Raspberry Pi) and an IP range for VPN clients.  
**Note:** It is strongly recommended that IP ranges assigned for VPN nad actual network are DIFFERENT.  
For example, the configuraiton file can be written as:

		localip 10.0.0.1
		remoteip 10.0.0.2-254
* Configure the DNS for VPN clients in `/etc/ppp/pptpd-optioins`:

		msdns 61.177.7.1
		msdns 223.5.5.5

* Comment the context `nodefaultroute` in the same file above to disable that feature.
* Add some users for VPN connection.  
In `etc/ppp/chap-secrets`, we can add some users according to the insturction in the file. If a user needa a dedicated IP address, input it in the last field. Otherwise, fill that field with `*`.

##Configure iptable again
* To run VPN smoothly, we need one more iptables rule. Just run the following command:

		sudo iptables -A FORWARD -p tcp –syn -s 10.0.0.0/24 -j TCPMSS –set-mss 1356
* Since NAT has been configured when setting up the wireless router, we don't need to work on it again.
* Then, disconnect the wireless network with Raspberry Pi, borrow another network cable and try to connect to Raspberry Pi with its IP address and the username/password. If all operations are correctly done, there will not be any problems.

##Setting up DDNS
Now, our VPN can be accessed in the campus network. However, it is useless since in Building Fei Yiming, it is still unreachable. Let's apply the DDNS service to our Raspberry Pi. [花生壳](http://hsk.oray.com/) is a widely-used DDNS service.
###Download and install 花生壳
* On PC, download Oray DDNS from its website, and transfer it to Raspberry Pi with peroper tools such as FileZilla.  
The following steps assume that the tgz file is located at `/` on Raspberry Pi.
* Switch to root authorization with the following command:

		sudo -s
* Extract the tgz file:

		tar xzvf /home/pi/phddns_raspberry.tgz
* Enter directory `phddns2` and execute `./oraynewph start`.  
If we see `Oraynewph start success !`, installation is finished.

###~~Configure Oray DDNS~~
When I tried to map PPTP port 1723, Oray DDNS mapped it to a randon port. However, most VPN clients don't support customize the port of VPN connection. So, sadly, VPN doesn't work.

* ~~Run `oraynewph status` in any path, we can get the running state and the SN number.~~
* ~~Visit **http://b.oray.com** and log in with the given SN number.~~
* ~~Bind your Raspberry Pi with your Oray account, then the free DN is bound to your Raspberry Pi now.~~