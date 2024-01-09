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
