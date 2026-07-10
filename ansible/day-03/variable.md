## 🔑 2. Reusability with Variables (`vars`)

Hardcoding se bachne ke liye hum variables define karte hain taake code dynamic aur clean rahe.

```yaml
--- # My 3rd Testing YAML Playbook
- hosts: demo 
  user: ansible
  become: yes
  connection: ssh
  vars: 
    pkgname: httpd     # Defining the variable
  tasks:
    - name: install httpd server 
      action: yum name='{{pkgname}}' state=installed  # Referencing the variable

```

