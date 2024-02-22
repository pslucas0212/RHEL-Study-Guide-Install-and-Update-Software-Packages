# RHEL Study Guide - Install and Update Software Packages


[RHEL Study Guide - Table of Contents](https://github.com/pslucas0212/RHEL-Study-Guide)  



Lets create a software repository for udpates.  Use the following parameters:

Parameter | Value
----------|------
File Name | errata.repo
Repository Name | [errata]
name= | Red Hat Updates
baseurl= | http://content.example.com/rhel9.0/x86_64/rhcsa-practice/errata
enabled= | 1
gpgcheck= | 0

The file is named errata.repo and located in the /etc/yum.repos.d/ directory.  The file contents look like this:
```
[errata]
name=Red Hat Updates
baseurl=http://content.example.com/rhel9.0/x86_64/rhcsa-practice/errata
enabled=1
gpgcheck=0
```

Let's install a new package.  First lets see if we have access to the package and if it is already installed
```
# dnf list rht-system
Red Hat Updates                                                                                         466 kB/s | 3.0 kB     00:00    
Available Packages
rht-system.noarch
```

Let's install the package.
```
# dnf install -y rht-system
Last metadata expiration check: 0:00:54 ago on Tue 09 Jan 2024 02:05:34 PM EST.
Dependencies resolved.
========================================================================================================================================
 Package                            Architecture                   Version                         Repository                      Size
========================================================================================================================================
Installing:
 rht-system                         noarch                         1.0.0-2                         errata                         7.5 k
...
Complete!
```

After installation:
```
# dnf list rht-system
Last metadata expiration check: 0:01:45 ago on Tue 09 Jan 2024 02:05:34 PM EST.
Installed Packages
rht-system.noarch
```

Let's remove an installed package.  Check that the package is installed:
```
# dnf list cups
Last metadata expiration check: 0:02:20 ago on Tue 09 Jan 2024 02:05:34 PM EST.
Installed Packages
cups.x86_64                                    1:2.3.3op2-13.el9                                     @rhel-9.0-for-x86_64-appstream-rpms
```

Remove the package:
```
# dnf remove -y cups
Dependencies resolved.
========================================================================================================================================
 Package                                     Architecture  Version                     Repository                                  Size
========================================================================================================================================
Removing:
 cups                                        x86_64        1:2.3.3op2-13.el9           @rhel-9.0-for-x86_64-appstream-rpms        7.6 M
...

Complete!
```

What if we want to install particular version of a package we have copied locally. In this example we want to install rhcsa-script-1.0.0-1.noarch.rpm - note the version.  Let's see if its available via a repo.
```
# dnf list rhcsa-script
Last metadata expiration check: 0:06:40 ago on Tue 09 Jan 2024 02:05:34 PM EST.
Available Packages
rhcsa-script.noarch                                                    1.0.0-2                                                    errata

```
That's not the correct version (1.0.0-2).  Let's be a bit more precies in our package name:
```
# dnf list rhcsa-script-1.0.0-1.noarch.rpm
Last metadata expiration check: 0:07:07 ago on Tue 09 Jan 2024 02:05:34 PM EST.
Error: No matching Packages to list
```

We have the exact version of the package located in the /home/student directory.  Let's go there and check the package out.  We use -qi for query information add -p to query the package.  The -i can also come after the package name. Note that rpm -i <package name> is used for installation via rpm and rpm -e <package name> is used for removing or erasing the package.  You can update an existing package with rpm -U <package name>.
```
# cd /home/student
# pwd
/home/student
# ls
rhcsa-script-1.0.0-1.noarch.rpm
# rpm -q -p rhcsa-script-1.0.0-1.noarch.rpm -i
Name        : rhcsa-script
Version     : 1.0.0
Release     : 1
Architecture: noarch
Install Date: (not installed)
Group       : System
Size        : 593
License     : GPL
Signature   : (none)
Source RPM  : rhcsa-script-1.0.0-1.src.rpm
Build Date  : Wed 23 Mar 2022 08:24:21 AM EDT
Build Host  : localhost
Packager    : Bernardo Gargallo
URL         : http://example.com
Summary     : RHCSA Practice Script
Description :
A RHCSA practice script.
The package changes the motd.
```


We can also use the rpm command to see if a package is installed.  Let's do that before we install this version.  We will use the packages "short name".
```
# rpm -q rhcsa-script
package rhcsa-script is not installed
```

Let's install the package from the /home/student directory using dnf install.
```
# dnf install -y rhcsa-script-1.0.0-1.noarch.rpm
Last metadata expiration check: 0:12:44 ago on Tue 09 Jan 2024 02:05:34 PM EST.
Dependencies resolved.
=====================================================================================================================================
 Package                           Architecture                Version                       Repository                         Size
=====================================================================================================================================
Installing:
 rhcsa-script                      noarch                      1.0.0-1                       @commandline                      7.5 k
...
Installed:
  rhcsa-script-1.0.0-1.noarch                                                                                                        

Complete!
```

Let's use the rpm -q command to check the installation with the package short name
```
# rpm -q rhcsa-script
rhcsa-script-1.0.0-1.noarch
```
Or with -qi for query information for an installed package. Note the Install Date information
```
# rpm -qi rhcsa-script
Name        : rhcsa-script
Version     : 1.0.0
Release     : 1
Architecture: noarch
Install Date: Thu 22 Feb 2024 09:42:18 AM EST
Group       : System
Size        : 593
License     : GPL
Signature   : (none)
Source RPM  : rhcsa-script-1.0.0-1.src.rpm
Build Date  : Wed 23 Mar 2022 08:24:21 AM EDT
Build Host  : localhost
Packager    : Bernardo Gargallo
URL         : http://example.com
Summary     : RHCSA Practice Script
Description :
A RHCSA practice script.
The package changes the motd.
```

And for fun let's use the dnf list command to check the installation
```
# dnf list rhcsa-script
Last metadata expiration check: 0:14:20 ago on Tue 09 Jan 2024 02:05:34 PM EST.
Installed Packages
rhcsa-script.noarch                                               1.0.0-1                                               @@commandline
Available Packages
rhcsa-script.noarch                                               1.0.0-2                                               errata
```

We see that we installed the correct version and the other version is available via the errata repo




