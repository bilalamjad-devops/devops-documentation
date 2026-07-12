Bilal 👌 — great, let’s **refactor your project into roles** so it looks professional and matches client expectations. Roles make your Ansible code modular, reusable, and easier to maintain.  

---

## 🧩 Project Folder Structure

```
infra-project/
├── terraform/
│   └── main.tf
├── ansible/
│   ├── hosts.ini
│   ├── site.yml
│   └── roles/
│       ├── common/
│       │   └── tasks/main.yml
│       ├── users/
│       │   └── tasks/main.yml
│       ├── security/
│       │   └── tasks/main.yml
│       ├── webserver/
│       │   └── tasks/main.yml
│       └── app/
│           └── tasks/main.yml
```

---

## 🔹 `site.yml` (Playbook that calls roles)
```yaml
- hosts: webservers
  become: yes
  roles:
    - common
    - users
    - security
    - webserver
    - app
```

---

## 🔹 Role: `common/tasks/main.yml`
```yaml
- name: Update apt cache
  apt:
    update_cache: yes

- name: Install common packages
  apt:
    name: "{{ item }}"
    state: present
  loop:
    - git
    - docker.io
```

---

## 🔹 Role: `users/tasks/main.yml`
```yaml
- name: Create developer user
  user:
    name: devuser
    groups: sudo
    shell: /bin/bash
```

---

## 🔹 Role: `security/tasks/main.yml`
```yaml
- name: Configure firewall
  ufw:
    state: enabled
    rule: allow
    port: '22'

- name: Disable root login
  lineinfile:
    path: /etc/ssh/sshd_config
    regexp: '^PermitRootLogin'
    line: 'PermitRootLogin no'
  notify: Restart ssh
```

---

## 🔹 Role: `webserver/tasks/main.yml`
```yaml
- name: Install Nginx
  apt:
    name: nginx
    state: present

- name: Start Nginx service
  service:
    name: nginx
    state: started
```

---

## 🔹 Role: `app/tasks/main.yml`
```yaml
- name: Deploy sample app
  copy:
    src: ./app/index.html
    dest: /var/www/html/index.html
```

---

## 🚀 Workflow
1. **Terraform** provisions infra (control + 2 managed nodes, SG, key pair).  
2. **Ansible inventory** (`hosts.ini`) defines managed nodes.  
3. **Playbook (`site.yml`)** calls roles in order.  
4. **Roles** handle modular tasks (common, users, security, webserver, app).  
5. Run:
   ```bash
   ansible-playbook -i hosts.ini site.yml
   ```
6. Verify services on `web01` and `web02`.

---

## 🎯 Why This Impresses Clients
- **Reusable roles** → modular, professional structure.  
- **Terraform + Ansible integration** → full infra + config automation.  
- **Security hardening + app deployment** → production‑ready.  
- **Documentation** → you can explain each role clearly in your repo/Medium article.  

---

👉 Bilal, do you want me to also draft the **GitHub Actions workflow** that ties Terraform + Ansible together (CI/CD style), so your repo looks like a complete end‑to‑end automation pipeline?

12-July-2026
