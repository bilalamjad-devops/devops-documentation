become or -b: sudo priviages dena

--- # My First Testing YAML Playbook

vi target.yml
- host: demo 
  user: ansible
  become: yes
  connection: ssh
  gather_facts: yes

esc:wq
ansible-playbook target.yml


---===




vi target.yml
--- # My second Testing YAML Playbook
- host: demo 
  user: ansible
  become: yes
  connection: ssh
  tasks:
   - name: install httpd 
     action: yum name=httpd state=installed

esc:wq
ansible-playbook target.yml

which httpd 

-====




vi vars.yml
--- # My 3rd Testing YAML Playbook
- host: demo 
  user: ansible
  become: yes
  connection: ssh
  vars: 
    pkgname: httpd
  tasks:
   - name: install httpd server 
     action: yum name='{{pkgname}}' state=installed

esc:wq
ansible-playbook target.yml

which httpd 


10-July-2026
