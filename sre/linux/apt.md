###apt-get install service with specified version
```
apt-get install -y <package name>=<package version>
```

###apt list available a service's version list
```
apt list -a <package name>
```

###common apt commands and the counterpart of apt-get or apt-cache
```
apt command	         the command it replaces	 function of the command

apt install	         apt-get install	         Installs a package
apt remove	         apt-get remove	             Removes a package
apt purge	         apt-get purge	             Removes package with configuration
apt update	         apt-get update	             Refreshes repository index
apt upgrade	         apt-get upgrade	         Upgrades all upgradable packages
apt autoremove	     apt-get autoremove	         Removes unwanted packages
apt full-upgrade	 apt-get dist-upgrade	     Upgrades packages with auto-handling of dependencies
apt search	         apt-cache search	         Searches for the program
apt show	         apt-cache show	             Shows package details
```
