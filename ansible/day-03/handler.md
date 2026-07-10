

## 🚨 3. Event-Driven Automation: Handlers & Dry Runs

> 💡 **The Reality Check:** Handler tabhi chalega jab task ka status `changed` hoga. Agar service pehle se installed hai aur koi change nahi hua, toh handler execution bypass ho jayegi.

```yaml
--- # Handlers Playbook
- hosts: demo
  user: ansible
  become: yes
  connection: ssh
  tasks:
    - name: install httpd server
      action: yum name=httpd state=installed
      notify: restart HTTPD   # Triggers the handler IF package installation causes a change
  handlers:
    - name: restart HTTPD     # Name MUST perfectly match the notify string
      action: service name=httpd state=restarted

```
