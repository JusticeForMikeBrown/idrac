
Configuring and Updating Dell PowerEdge Using Ansible
===============

This **WIP** role will update Dell PowerEdge iDRAC and BIOS as well as configure various iDRAC settings.  Among other things you can set boot order, reboot server, reset iDRAC, configure iDRAC authentication, and configure iDRAC alerts.


Things To Consider
------------

iDRAC and BIOS updates are ran within operating system therefore it must already be installed.  The role will not initiate reboot.

To configure iDRAC this role wraps **racadm** so you must be able to run it on the given server whether through the operating system or iDRAC.

Given the use of **vars_prompt** you will be prompted every time to choose a new iDRAC password.  By pressing enter the default of null will be selected while tasks to reset password will be skipped.

Requirements
------------

You must have Ansible 2.0 installed.

You need [Slack](https://slack.com/)

You need a web server to host iDRAC and Firmware files.  This role does not download them from Dell, either.


TODO
--------------

Add Slack alerts for tasks in **configure.yml**

Add error handling to detect whether updates in **bios.yml** were successful or failed

Add steps to detect whether updates in **bios.yml** were already completed thus skip the given task

Get rid of **vars_prompt** as it's annoying

Examples
--------

Many potential command-line variables can be defined, along with tags, to do specific things.

By default, when using **-e conf=[]**, only these tasks will be performed:

* iDRAC DNS configured (required for email alerts)
* iDRAC gateway configured (required for email alerts)
* Persistent boot order set to HD
* Hardware Alerts configured via email

To run this do:

```
ansible-playbook idrac.yml -e hosts=dracip -e conf=[] -k

```

To change iDRAC password:

```
ansible-playbook idrac.yml -e hosts=dracip -e password=[] -u root -k -t new_password
```

To do one-time PXE:
```
ansible-playbook idrac.yml -e hosts=dracip -e pxe=[] -u root -k -t pxe
```

Reboot server:
```
ansible-playbook idrac.yml -e hosts=dracip -e reboot=[] -u root -k -t reboot
```

Stop server:
```
ansible-playbook drac.yml -e hosts=dracip -e stop=[] -u root -k -t stop
```

Start server:
```
ansible-playbook drac.yml -e hosts=dracip -e start=[] -u root -k -t start
```



License
-------

GPL

Author Information
------------------

Douglas Duckworth
quackmaster@protonmail.com
