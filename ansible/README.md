#ANSIBLE PLAYBOOKS#

Ansible is an automation library written in Python. Its only requirement on the client-side is Python 2.5
This configuration should be able to populate our auth environment by modifying just the inventory file, then running:

ansible-playbook ./rpi.yml -i inventory

# Getting Started
Two core files must exist:
1. inventory
2. rpi.yml

## Server prerequisites (the machine you physically use)
```
sudo apt-get install ansible python git
```

## Client prerequisites (the machine you are trying to manage remotely)

### Install raspbian onto an SD card
The latest image can always be found here <http://downloads.raspberrypi.org/raspbian_latest.torrent>
Download that file, then insert your SD card.
Identify where your SD card is in the filesystem (`ls /dev/mmc*` generally gives me a good idea)
Copy the downloaded image file onto the SD card.

Example:
```
sudo dd bs=4M if=./2014-09-09-wheezy-raspbian.img of=/dev/mmcblk0
sync
```

Remove the card, and boot it in a pi.
After booting, you'll have some basic options to configure in the 'basic startup'
For this tutorial, we'll assume you have only expanded the primary card and added a password to the `pi` user.

Ensure that you configure networking (automatic if ethernet, or use the built-in wifi client after booting).

### Install apt prerequisites
```
sudo apt-get install python python-apt
```

### Ensure that the user Ansible will use has sudo rights

(as root)
```
adduser pi sudo
```

### Configure SSH keys to [ansible_user]@[server]

For example:
```
ssh-keygen
ssh-copy-id pi@10.100.0.46
```

Documentation on Ansible playbooks/inventory files can be found here <http://docs.ansible.com/>

# TODO
1. Build in fstab entries for automatic filesystem mounts (nfs/webdav/etc)
1. Build automatic login to the auth server
1. Determine the dhcp server address (store as a variable?)
1. Determine the dns server address (store as a variable?)