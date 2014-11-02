#ANSIBLE PLAYBOOKS#

Ansible is an automation library written in Python. Its only requirement on the client-side is Python 2.5
This configuration should be able to populate our auth environment by modifying just the inventory file, then running:

ansible-playbook ./openldap.yml -i inventory

# Getting Started
Two core files must exist:
1. inventory
2. playbook.yml

## Server prerequisites (the machine you physically use)

```
sudo apt-get install ansible python
```

## Client prerequisites (the machine you are trying to manage remotely)
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

Documentation on their setup can be found here <http://docs.ansible.com/>
