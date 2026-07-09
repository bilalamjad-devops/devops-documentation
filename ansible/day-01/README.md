
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
```all
sudo su 
visudo

root  ALL=(ALL)     ALL
ansible ALL={ALL} NOPASSWD: ALL
```
esc:wq

we are going sudouser privilages to all ansible-server and nodes. so we can work with adding sudo with our command.

To verify:
su - ansible

yum install httpd -y 
sudo yum install httpd -y


### All ansible-server and both nodes

```all
vi /etc/ssh/sshd_config
PermitRootLogin yes 
PasswordAuthentication yes 
#PasswordAuthentication no 
```
esc:wq

```all
server sshd restart
```

Note: big tasks are performed by root user


su - ansible

ssh PrivateIPofNode1

password: 

Now you are in Node1. Create some files and you can see in going Node1. 

Trust Relationship
Root -> Root ka sath 
user -> user ka sath 

Ansible-server
```
ssh-keygen 
ls
.ssh
cd .ssh
ls 
id_rsa id_rsa.pub

ssh-copy-id ansible@PrivateIPofNode1

ssh-copy-id ansible@PrivateIPofNode2

cd . because we were in .ssh menu

---

Host Patterns

all: refers to all the machines in an invertory.

-> ansible all --list-hosts
-> ansible groupname --list-hosts
-> ansible groupname[0] --list-hosts

here [0] shows first node




9-July-2026
