#Setup Instruction
This is an alternative way to have access to databases offered by the Library of Nanjing University. And by the way, with this proxy, there will not be any circumstances that CSS files won't be loaded when I tried to visit GitHub in my laboratory.

##Install `squid`
**Note:** When installing squid, you may find in apt repos, there are two versions of `squid`, namely, `squid` and `squid3`. The former one is with the version of 2.7. In this instruction, I used `squid`, but `squid3` is also usable.

To install `squid`, run the following command:

	sudo apt-get install squid

##Make some configuraton
The configuration file of `squid` is quite complex. In the original configuration file `/etc/squid/squid.conf`, almost all contents are comments, about 3900 lines of comments! Here, I will only introduce some core configuration items to you. The rest are for you to discover.

###Port settings
The default service port of `squid` is 3128. If you want to change it to increase security, just change it in the configuration file.

	http_port 3128

###Something about cache and memory usage
Our Raspberry Pi has a memory of 1GB. It seems abundant, but with some other services running on it, our proxy can't consume too much memory resource.  
The following configuration works on this issue.

	cache_mem 16 MB
	maximum_object_size 4 MB
	cache_dir ufs /var/spool/squid 16 16 256

Remember, **all numbers and thier units must be seperated by a blank character.**

The total memory usage of `squid` is determined by the following formula:

		M=10x+15+cache_mem (All parameters use MB as the unit)
		
		* x: the size of cache_dir

* `cache_mem` determines the extra memory `squid` can use at most.
* If an object is larger than the value set in `maximum_object_size`, it will **NOT** be cached, neither in memory nor in disk.
* `cache_dir` determines how and where contents are cached in the hard drive. (For us, it means the microSD card.)
	* The first number `16` is the greatest size of the directory we set before itself.
	* The second `16` is the number of directories of L1 cache.
	* The last number `256` is the number of directories of L2 cache.

###ACL
We can let `squid` offer service for a specific range of IP address. In this instruction, I simply opened this service all around the world.  
The way to write ACL is similar to that on a physical router.

	http_access allow all

###Something else
	visible_hostname miaoxw.software.nju.edu.cn
	cache_mgr mg1632004@software.nju.edu.cn

These messages will appear on the error page if this proxy can't have access to the required HTTP request.

##Let It Run
* Stop the service with the following commamd:

		sudo service squid stop
* Re-initialize swap directories with the following command:

		sudo squid –z
* Now, use the command to start the service again:

		sudo service squid start

##Setting up DDNS
Now, our proxy can be accessed in the campus network. However, it is useless since in Building Fei Yiming, it is still unreachable. Let's apply the DDNS service to our Raspberry Pi. [花生壳](http://hsk.oray.com/) is a widely-used DDNS service.

###Download and install 花生壳
* On PC, download Oray DDNS from its website, and transfer it to Raspberry Pi with peroper tools such as FileZilla and WinSCP.  
The following steps assume that the tgz file is located at `/` on Raspberry Pi.
* Switch to root authorization with the following command:

		sudo -s
* Extract the tgz file:

		tar xzvf /phddns_raspberry.tgz
* Enter directory `phddns2` and execute `./oraynewph start`.  
If we see `Oraynewph start success !`, installation is finished.

###Configure Oray DDNS
* Run `oraynewph status` in any path, we can get the running state and the SN number.
* Visit **http://b.oray.com** and log in with the given SN number.
* Bind your Raspberry Pi with your Oray account.
* In **`内网映射`**, add a new port mapping rule.
	* In `应用名称`, type in a string at your wish.
	* In `内网主机`, input the Intranet IP address used by your Raspberry Pi.  
	Any Intranet address will do. Even `127.0.0.1` is also OK.
	* In `内网端口`, input the port where `squid` offers service.
* Click `确定`, you can see a new item in `外网访问地址`. That is the proxy domain name and port, with which we can browse the Internet through campus network.