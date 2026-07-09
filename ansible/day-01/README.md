
```ansible-server
wget https://fedoraproject.org/pub/epel-release-latest-7.noarch.rpm
```

```ansile-server
apt install epel-release-latest-7.noarch.rpm
```

```ansible-server
ansible --verion
```
/etc/ansible/ansible.cfg

> etc abbreviation: "Editable Text Configuration"

```ansible-server
vi /etc/ansible/hosts

[demo]
PastePrivateIPofNode2
PastePrivateIPofNode2
```
ESC:wq

Now we have made a group and added private IPs of both nodes.

```ansible-server
vi /etc/ansible/ansible.cfg
uncomment:
inventory = /etc/ansible/hosts
sudo_user = root
```
ESC:wq

```ansible-server
adduser ansible
passwd ansible
enter password:
```

### Run on both Node1 and Node2

```bothNodes
ec2-user
sudo su
adduser ansible
passwd ansible
enter password:
```

### ansible server and all nodes

sudo su 
visudo

root  ALL=(ALL)     ALL
ansible ALL={ALL} NOPASSWD: ALL

esc:wq

we are going sudouser privilages to all ansible-server and nodes. so we can work with adding sudo with our command.

9-July-2026
