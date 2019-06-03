# Shell tricks

## Move/rename multiple files

Use `mmv` to move/rename multiple files using patterns, etc. (taken from [this SO answer](https://stackoverflow.com/questions/1086502/rename-multiple-files-based-on-pattern-in-unix/20119482#20119482))

http://manpages.ubuntu.com/manpages/precise/man1/mln.1.html

## Default variable

`VALUE=${1:-defaultvalue}`

## Check for env var in Bash

Taken from [this SO question](https://stackoverflow.com/questions/307503/whats-a-concise-way-to-check-that-environment-variables-are-set-in-a-unix-shell)

```bash
: "${STATE?Need to set STATE}"
: "${DEST:?Need to set DEST non-empty}"
```
The first requires STATE to be set, but STATE="" (an empty string) is OK. The 2nds requires DEST to be set and non-empty.

## In-place replacement

    find . -name '*.py' -exec sed -i '' -e  "s/OLD_PATTERN/NEW_PATTERN/g" {} \;
    
If there are quotes which are the target replacement, use the following variables: `LC_CTYPE=C LANG=C`. [From this answer](https://stackoverflow.com/questions/19242275/re-error-illegal-byte-sequence-on-mac-os-x)

## Prepend a line to an existing file

    echo 'task goes here' | cat - todo.txt > temp && mv temp todo.txt

[Taken from SO](https://superuser.com/questions/246837/how-do-i-add-text-to-the-beginning-of-a-file-in-bash)

## Create a temp file descriptor

This is great for getting data out of some existing system or process and into a command which
expect to read from a file.  A file is never actually created using this, but the end result is
what you'd expect.

https://unix.stackexchange.com/questions/63923/pseudo-files-for-temporary-data

    docker run --env-file <(env | grep AWS)


## Read an SSL certificate

	openssl x509 -in public.pem -text -noout


## Execute a command for a user who has no login shell

	su -s /bin/bash -c '/path/to/your/script' testuser


## Sum column using awk

	cat count.txt | awk '{sum+=$1} END {print sum}'


## Default a command line arg in bash

    FOO=${VARIABLE:-default}


## To see all the files the package installed onto Ubuntu:

	dpkg-query -L <package_name>


## To see the files a .deb file will install

	dpkg-deb -c <package_name.deb>


## To see the files contained in a package NOT installed, do this once (if you haven't installed apt-file already):

	sudo apt-get install apt-file
	sudo apt-file update

	then

	apt-file list <package_name>


## List open ports

	linux: netstat -lnptu
	mac: netstat -a -p tcp


## Reset postgres pkey sequences

	SELECT pg_catalog.setval(pg_get_serial_sequence('TABLE_NAME', 'id'), (SELECT MAX(id) FROM TABLE_NAME)+1); 


## List connected hosts

	netstat -n -A inet
	netstat -n -A inet | awk '{print $5}' | tr ':' ' ' | awk '{print $1}' | sort | uniq -c


# DNS Stuff

	dscacheutil -q host -a name admin.ccdev.vg
	scutil --dns

# Misc

## Remove VirtualBox virtual interfaces

	VBoxManage hostonlyif remove vboxnet1


## Reset guest additions version

    VBoxManage guestproperty set ae63d283-bd8d-44ea-be05-e61c9b2a8f73  /VirtualBox/GuestAdd/Version


## Purge all queues from rabbitmq

	for q in ` sudo rabbitmqctl list_queues | awk '{print $1'} | egrep "d16|celery"`;
		 do celery amqp queue.purge $q;
	done

## Display status of loaded kernel extensions

	man kextstat
	kextstat | grep -i usb  | awk '{print $6}' | sort


## display the system message buffer

dmesg


# Setup vim plugins

	https://github.com/tpope/vim-pathogen


## Push up to a specific commit

    git push origin SHA:branch_name


## Run a simple HTTP server using nc

    nc -kl 5432 -c 'echo -e "HTTP/1.1 200 OK\r\n$(date)\r\n\r\n";echo "<p>How are you today?</p>"'
    while true ; do nc -l 80  < index.html ; done


## Find time a process has been running

    for pid in `ps auwwwx | grep uwsgi | grep clearcare.yaml | awk '{print $2}'`; do
      ps -p $pid -o etime=
    done


## Add/remove 200ms delay to a network interface

    root@ccdev# tc qdisc add dev lo root netem delay 200ms
    root@ccdev# tc qdisc del dev lo root


## Get IP address for a given network device

    ifconfig eth1 | grep "inet addr" | awk '{ print substr($2,6) }


## ssh-agent on the mac

    sudo launchctl load -w /System/Library/LaunchAgents/org.openbsd.ssh-agent.plist
    sudo launchctl unload /Path


## To start a differently named key at login:

    ssh-add -K ~/.ssh/some_key 


## strip multiple characters

    sed 's/[<>,]//g'


## Uninstall and purge a debian pakages

    removes conf files: dpkg -P elasticsearch  


## Install a package from a file: 

    dpkg -i elasticsearch-0.90.7.deb
