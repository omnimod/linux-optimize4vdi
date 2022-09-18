# ubuntu-optimize4vdi
Ubuntu-optimize4vdi is a simple Ansible playbook which performs basic configuration steps like updating OS, uninstalling/installing packages, setting GNOME desktop parameters, etc.

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
6. Modify inventory file and specify virtual desktop IP address or hostname.
7. Run Ansible playbook with:
```
ansible-playbook --ask-become-pass optimize.yml
```
