# linux-optimize4vdi
Linux-optimize4vdi is a simple Ansible playbook which performs basic configuration steps like updating OS, uninstalling/installing packages, setting GNOME desktop parameters, etc. Current version supports Ubuntu 22.04.

Automated features
==================
This playbook performs multiple optimizations:
1. Remove unnecessary Ubuntu apps (games, usb creator utility and transmission app).
2. Update and upgrade packages with apt update && apt upgrade.
3. Update installed apps with snap refresh.
4. Install the latest version of Open-VM-Tools.
5. Install new apps via apt (chromium, 7zip, vlc, telegram desktop client, and zoom client).
6. Disable apt automatic updates and upgrades.
7. Enable GRUB quiet boot.
8. Disable system hibernation and sleep.
9. Disable unnecessary services (bluetooth, thunderbolt, firmware update service).
10. Join to the domain.
11. Compile VHCI driver for Horizon USB redirection.
12. Compile V4L2Loopback driver for Horizon RTAV.
13. Install Horizon Agent with Audio redirection, USB redirection, and RTAV.
14. Enable SSO for Horizon.
15. Optimize GNOME desktop (disable animation, set default background to single color).
16. Clean bash history.
17. Reboot the virtual desktop.

How to use
==========
1. Install Ubuntu 22.04 Guest OS on the virtual desktop VM with default parameters. Set the default user account with 'user' as username and sudoer permissions. If you user another username, please modify configuration steps and ansible.cfg accordingly.
2. Install OpenSSH server on the virtual desktop:
```
sudo apt get install openssh-server
```
3. Install Ansible on your workstation / client computer.
4. Generate ssh keys on your workstation with default settings:
```
ssh-keygen
```
5. Copy public key from your workstation to the virtual desktop:
```
ssh-copy-id -i ~/id_rsa.pub user@virtual_desktop_ip_address
```
6. Modify inventory file and specify virtual desktop IP address and modify required variables.
7. Download and place required installation packages and archives to the files folder.
8. Run Ansible playbook with:
```
ansible-playbook --ask-become-pass optimize.yml
```

Tags
====
If you want to run only certain optimization you can run ansible-playbook with `--tags "tag1, tag2, tag3"` parameter. Currently this playbook supports tags:
- horizon - install and configure VMware Horizon Agent on the virtual desktop.
- domain - join to the domain with the parameters specified in inventory files.
- gnome - perform GNOME desktop tweaks and optimizations.
- reboot - reboot the virtual desktop after completing optimizations.
For example to run playbook with horizon and domain join optimization only enter:
```
ansible-playbook --ask-become-pass --tags "horizon, domain" optimize.yml
```
Variables
=========
Inventory file contains variables, which are necessary to run the playbook:
- horizon_agent - archive name with the horizon_agent installation package
- vhci_driver - vhci driver archive name
- v4l2loopback_driver - archive name with the v4l2loopback driver
- domain_name - domain name to join
- domain_user - domain account name to join to the domain
- domain_password - password for domain-entry account
- debug - set to True to display extended information from the commands that have been executed
