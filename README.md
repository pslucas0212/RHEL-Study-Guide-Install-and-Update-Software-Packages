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
