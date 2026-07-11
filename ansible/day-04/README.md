When we have different different scenaios, we put conditions according to the scenario. 

--- # Condition Playbook
- hosts: demo
  user: ansible
  become: yes
  connection: ssh
tasks:
  - name: install apache on debian
    command: apt-get -y install apache
    when: ansible_os_family=="Debian"
  - name: install apache for redhat
    command: yum -y install httpd
    when: ansible_os_family=="RedHat"

===

Vault means tajori

when we want to make encrypted playbook.

ansible-vault create vault.yml 
edit the encrypted playbook:
ansible-vault edit value.yml
to change the password:
ansible-vault rekey vault.yml
to encrypt an existing playbook
ansible-vault encrypte target.yml
to decrypt an encrypted playbook:
ansible-vault decripte target.yml


Roles

mkdir -p playbook/roles/webserver/tasks

tree

mkdir playbook/roles/webserver/handler

created master.yml and roles/webserver/tasks/main.yml

touch roles/webserver/tasks/main.yml

touch master.yml

vi roles/webserver/tasks/main.yml

Inside main.yml

-name: install apache
 yum: pkg=httpd state=latest
esc:wq

vi master.yml
note: in maste.yml we target kon sa group, kon sa role us pr apply krna ha 

-host: all
 user: ansible
 become: yes
 connection: ssh
 roles:
  - webserver 
esc:wq

ansible-playbook master.yml

mkdir -p playbook/roles/webserver/tasks

cd playbook

tree

touch roles/webserver/tasks/main.yml

touch master.yml

vi roles/webserver/tasks/main.yml

- name: install apache on RedHat
  yum: pkg=httpd state=latest
esc:wq

vi master.yml

--- # master playbook for webservers
- hosts: demo
  user: ansible
  become: yes
  connection: ssh
  roles:
   - webserver
esc:wq

ansible-playbook master.yml

which httpd






