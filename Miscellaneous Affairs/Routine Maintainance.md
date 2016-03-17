#Routine Maintainance
##Rebooting every day
Usually, the every-day network traffic is quite heavy. In order to keep our Raspberry Pi working in good conditions, it is a good idea to reboot it at a reasonable frequency. The easiest way is of course using `cron`.

###Check whether `crond` is installed
By default, `crond` is a service together with the Raspberry Pi image. If it is not installed, run the following simple command:

	sudo apt-get install cron

###Locate the command to be used
It is suggested that full path of every command in the crontab be written. It is because in different permission of different users, a single command may lead to different executable files.  
To find out the path of a command, just use the command `whereis`. In this instruction, we try to use `init 6` to reboot the Raspberry Pi. Therefore, we need to type in:

	whereis init

We get the following output:

	init: /sbin/init /etc/init /etc/init.status /etc/init.d /lib/init /usr/share/man/man1/init.1.gz

According to our experience, `/sbin/init` is the proper one.

###Edit `crontab`
Since rebooting is an operating which requires `root` authentication, rebooting commands must be run with user `root`. So, we need to edit root's crontab:

	sudo crontab -e

Then, you may be asked about which editor you want to use. Choose one you like.

We want our rebooting to cause as little influence on our daily Internet access as possible. So we'd better set the rebooting time at midnight. 0:00 is still too early, I think 3:30 is a good idea. Append the following new line to the file just opened.

	30 3 * * * /sbin/init 6

Then everything is done.
