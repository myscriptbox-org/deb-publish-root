# man page for deb-publish-root
## NAME 
**deb-publish-root** server installation, publication user accounts and domains on a remote debian repository publication server. You need to be root on the remote server to use this program.

## SYNOPSIS
**deb-publish-root** [objectPath] [ objectId1 ... objectIdN ] -action [ actionArg1 .. actionArgM]

## DESCRIPTION 
### server
Use this object path to manage server-wide installation of packages on the remote server.

### server.apache
Use this object path to manage the apache-related installation on the remote server.

### server.apache.servername
Use this object path to fix the apache server name on the remote server, if needed.

### server.reprepro
Use this object path to manage the reprepro-related installation on the remote server.

### server.user
Use this object path to manage a publication user account on the remote server.

### server.users
Use this object path to inquire on the collection of publication user accounts on the remote server.

### server.vhost
Use this object path to manage publication domains on the remote server.

### server.vhosts
Use this object path to inquire on the collection of publication domains on the remote server.

## OPTIONS

### --help
shows the general help paragraph.

### [objectpath] --help
shows general help for the object path.

### --version
shows the program's version.

### --license
shows the program's license.

### server [obj] -apt-update
This command will update the _apt_ database on the remote system. The _apt_ database contains a list of all packages with their most recent version available from the remote installation repositories. After updating the database, and new versions of packages in use have become available, it will be possible to upgrade these packages to their latest versions. Example:  
**deb-publish-root** server root@myserver.com -apt-update  

### server [obj] -apt-upgrade
This command is typically run after **deb-publish-root** server -apt-update. This command will upgrade all packages on the remote system to the latest versions inscribed in the _apt_ database. The _apt_ database contains a list of all packages with their most recent version available from the remote installation repositories. Example:  
**deb-publish-root** server root@myserver.com -apt-upgrade  

### server [obj] -uninstall
This command uninstalls the packages installed during **deb-publish-root** server -install. Example:
**deb-publish-root** server root@myserver.com -uninstall

### server [obj] -show-users
This command will list the debian repository publishers on the remote server. Example:  
**deb-publish-root** server root@myserver.com -show-users  
This command outputs one line per publisher-user on the remote server.

### server [obj] -check-if-installed
This command checks if the apache and reprepro packages have been installed on the remote server. Example:  
**deb-publish-root** server root@myserver.com -check-if-installed  
This command outputs 'yes' if the packages have been installed and 'no' if not.

### server [obj] -install
This command will install the apache packages, fix the servername, if needed, and install reprepro. Example:  
**deb-publish-root** server root@myserver.com -install  
This command calls all installation tasks required the root level to prepare the server for serving debian repositories.


### server [obj] -verify-system
This command verifies if the minimum required programs are present on the remote server for the publication system to be able to be installed. It checks if _apt-get_ and _gpg_ are installed. Example:  
**deb-publish-root** server root@myserver.com -verify-system  
This command outputs 'ok' if the dependent programs are present, and 'nok' if they are not.

### server.apache [obj] -control [arg]
This command issues control instructions to apache on the remote server. Example:  
**deb-publish-root** apache root@myserver.com -control start  
This example will start apache on the remote server. Permissible control instructions are: start, stop, restart, reload.

### server.apache [obj] -install
This command installs the apache2 and apache2-utils packages on the remote server. Example:  
**deb-publish-root** apache root@myserver.com -install


### server.apache [obj] -check-if-installed
This command checks if the packages apache2 and apache2-utils have been installed on the remote server. Example:  
**deb-publish-root** apache root@myserver.com -check-if-installed  
If the packages have been installed, the command outputs 'yes'. Otherwise, it outputs 'no'.

### server.apache [obj] -is-running
The command checks if apache is running on the remote server. Example:  
**deb-publish-root** apache root@myserver.com -is-running  
The command outputs 'yes' if apache is running, and 'no' if apache is not running.

### server.apache [obj] -uninstall
The command uninstalls the apache2 and apache2-utils packages on the remote server. Example:  
**deb-publish-root** apache root@myserver.com -uninstall

### server.apache.servername [obj] -fix
This command supplies a server name, if one is missing in apache's configuration file. Example:  
**deb-publish-root** apache.servername root@myserver.com -fix  
The command will set the server name to _localhost_. This will stop apache from producing warnings.

### server.apache.servername [obj] -remove-fix
The command **deb-publish-root** apache.servername -fix will supply a default server name. This command will remove the fix. Example:
**deb-publish-root** apache.servername root@myserver.com -remove-fix  
This command is being supplied in a policy of maintaining the ability to undo/reverse each command, when possible. A command that cannot be undone, becomes strategic. This policy tries to limit the number of strategic commands to the bare minimum possible.

### server.apache.servername [obj] -check
Apache issues warnings if the server name is not filled out. This command checks if a server name was supplied in apache's configuration file: _/etc/apache2/apache2.conf_. Example:  
**deb-publish-root** apache.servername root@myserver.com -check  
The command outputs 'ok' if the servername was filled out and 'nok' if not.

### server.reprepro [obj] -check-if-installed
This command verifies if _reprepro_ has been installed on the remote system. Example:  
**deb-publish-root** server.reprepro root@myserver.com -check-if-installed  
This command outputs 'yes' if _reprepro_ has been installed and 'no', if it hasn't.

### server.reprepro [obj] -uninstall
This command uninstalls _reprepro_ on the remote system. Example:  
**deb-publish-root** server.reprepro root@myserver.com -uninstall  

### server.reprepro [obj] -install
This command installs _reprepro_ on the remote system. Example:  
**deb-publish-root** server.reprepro root@myserver.com -install  

### server.show [obj] -show-vhosts
This command shows the list of domains being published from a remote server. Synopsis:  
**deb-publish-root** server [root@server] -show-vhosts  
Example:  
**deb-publish-root** server root@myserver.com -show-vhosts  
Example output:  
domain                   user     enabled  
garagesoft.myserver.com  carlos   yes  
john.myserver.com        john     no  
internal.myserver.com    thanh    yes  

### server.user.arg [obj] -set-pwd [arg]
This command will create a new user on a remote server or change its password. If the user exists already, this command will just change his password. Synopsis:  
**deb-publish-root** server.user [root@server] [user] -set-pwd [password]  
Example:  
**deb-publish-root** server.user root@myserver john -set-pwd '!?j.o.h.n*99'
This command will also add the user to the group _deb-publish_ on the remote server.

### server.user.arg [obj] -create-skeleton [arg]
This command creates the required _reprepro_ skeleton folders on the remote system for a user who will be publishing debian packages.  .Synopsis:{br}
**deb-publish-root** [root@server] [user] -create-skeleton [domain]  
 Example:  
**deb-publish-root** root@myserver.com john -create-skeleton somerepository.com  

### server.user.arg [obj] -exists
This command checks if a particular user exists on a remote server. Synopsis:  
**deb-publish-root** server.user [root@server] [user] -exists  
Example:
**deb-publish-root** server.user root@myserver.com john -exists  
This command will output 'yes' if the user exists and 'no' if he doesn't.

### server.user.arg [obj] -delete
This command deletes a user account from the remote server. Example:  
**deb-publish-root** server.user root@myserver.com john -delete  
This example will delete the user 'john' from the server myserver.com.

### server.user.arg [obj] -delete-skeleton [arg]
This command will delete the skeleton folders for a particular user on the remote server. Synopsis:  
**deb-publish-root** [root@server] [user] -delete-skeleton  
Example:  
**deb-publish-root** root@myserver john -delete-skeleton

### server.user.arg [obj] -show-domains
This command will list the domains managed by a particular user on the remote server. Synopsis:  
**deb-publish-root** server.user [root@server.com] [user] -show-domains  
Example:  
**deb-publish-root** server.user root@myserver.com carl -show-domains  
This command outputs one line per domain managed by the user on the remote server.

### server.vhost.arg [obj] -disable
This command pauses the publication from a particular domain. Synopsis:  
**deb-publish-root** server.vhost [root@server] [domain] -disable
Example:  
**deb-publish-root** server.vhost root@myserver.com packages-by-john.server.com -disable

### server.vhost.arg [obj] -delete-with-user
This command will delete a virtual apache host on the remote server. It will also delete the user account and its data, though. Synopsis:  
**deb-publish-root** server.vhost [root@server] [domain] -delete-with-user  
Example:  
**deb-publish-root** server.vhost root@myserver.com packages-by-john.myserver.com -delete-with-user

### server.vhost.arg [obj] -show-user
This command queries what user is associated with a particular domain on the remote server. Synopsis:  
**deb-publish-root** server.vhost [root@server] [domain] -show-user  
Example:
**deb-publish-root** server.vhost root@myserver.com garagesoft.myserver.com -show-user  
This command will output the username from whose account the domain is being published.


### server.vhost.arg [obj] -enable
This command resumes the publication from a particular domain. Synopsis:  
**deb-publish-root** server.vhost [root@server] [domain] -enable
Example:  
**deb-publish-root** server.vhost root@myserver.com packages-by-john.server.com -enable

### server.vhost.arg [obj] -delete
This command will delete a virtual apache host on the remote server. It will not delete the user account nor its data, though. Synopsis:  
**deb-publish-root** server.vhost [root@server] [domain] -delete  
Example:  
**deb-publish-root** server.vhost root@myserver.com packages-by-john.myserver.com -delete
If the user will be publishing the same packages but on another domain, you can use this command to just delete the domain.

### server.vhost.arg [obj] -set-user [arg]
This command attaches an existing user to a particular domain on the remote server. Synopsis:  
**deb-publish-root** server.vhost [root@server] [domain] -set-user [user]  
Example:
**deb-publish-root** server.vhost root@myserver.com other-software.myserver.com -set-user carlos

### server.vhost.arg [obj] -create-with-user [args]
This command will create an apache virtual host along with a user account. Synopsis:  
**deb-publish-root** server.vhost [root@server] [domain] -create-with-user [user] [password]  
Example:  
**deb-publish-root** server.vhost root@myserver.com packages-by-peter.myserver.com -create-with-user peter '*p!e!t!e!r*'


### server.vhost.arg [obj] -exists
This command checks if a domain is being served on a remote server. Synopsis:  
**deb-publish-root** server.vhost [root@server] [domain] -exists  
Example:  
**deb-publish-root** server.vhost root@myserver.com john.myserver.com -exists  
The command outputs 'yes' if the domain exists and 'no' if it doesn't.

## ENVIRONMENT 
## EXIT-STATUS 
### 0
A zero exit code means that everything went ok.
### 1
A one exit code is usually an error generated by **deb-publish-root** itself.
### other
Another exit code is always an error generated by one of the underlying programs invoked by **deb-publish-root**.

## FILES 
### /etc/deb-publish-root.d/templates/reprepro.vhost
This file contains the default apache virtual host template. If you have reasons to customize this file, you can change it. The file uses the template variables _{documentRoot}_ and _{serverName}_.

### /etc/deb-publish-root.d/sshConnection.conf
This file is a bash shell script. In order to speed up processing over SSH, **deb-publish-root** opens a master control connection that remains active for 15 minutes. All subsequent connections to the same SSH account will be multiplexed over this master controller. Change the parameters for master and slave connections in this file. You can also switch off the master control facility, but in that case processing may go much slower.

## AUTHOR
Erik Poupaert <erik@sankuru.biz>

## REPORTING-BUGS
Report bugs to: erik@sankuru.biz

# COPYRIGHT
Licensed under: GPL
