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

