Bilal, aapke notes ka content bohot zabardast hai! Isme aap **Advanced Ansible Standards** cover kar rahe hain: **Conditionals (`when`), Secret Protection (`ansible-vault`), aur Architecture Componentisation (`roles`)**.

Aapne built-in structural design ko bilkul sahi tarike se execute kiya hai. Aapke revision aur GitHub repository ke liye isko ekdum professional, clean aur highly scannable formatting mein convert kar diya hai.

---

# 🛠️ Ansible Advanced: Conditionals, Secrets, & Modular Roles

> **Date:** 11-July-2026 | **Core Focus:** Multi-OS target validation, playbook encryption, and structural enterprise play organization via Roles.

---

## 🎛️ 1. Environmental Conditionals (`when`)

Jab aapka infrastructure heterogeneous ho (kuch nodes Ubuntu/Debian par hon aur kuch CentOS/RedHat par), toh hum facts monitoring ke mutabik condition lagate hain.

```yaml
--- # Condition Playbook
- hosts: demo
  user: ansible
  become: yes
  connection: ssh
  tasks:
    - name: install apache on debian
      command: apt-get -y install apache
      when: ansible_os_family == "Debian"   # Runs ONLY if the target node is Debian/Ubuntu

    - name: install apache for redhat
      command: yum -y install httpd
      when: ansible_os_family == "RedHat"   # Runs ONLY if the target node is RHEL/CentOS

```

> 💡 **Best Practice Note:** Real-world operations mein `command` module ke bajaye declarative `apt` aur `yum` modules use karna zyaada safe hota hai.

---

## 🔐 2. Vault Security Management (`ansible-vault`)

> 🔑 **Concept:** Playbooks ya variable files ke andar mojood sensitive data (jaise API keys, database passwords) ko encrypt karke secure ("tajori" mein) rakhna.

| Command Execution | Practical Action Purpose |
| --- | --- |
| `ansible-vault create vault.yml` | Nayi encrypted file zero se create karna. |
| `ansible-vault edit vault.yml` | Kisi encrypted file ka safe data edit/view karna. |
| `ansible-vault rekey vault.yml` | Encryption key ka authentication password badalna. |
| `ansible-vault encrypt target.yml` | Pehle se bani hui standard file ko lock/encrypt karna. |
| `ansible-vault decrypt target.yml` | Encrypted file ko wapas human-readable text mein badalna. |

* **Running an Encrypted Playbook:**
```bash
ansible-playbook vault.yml --ask-vault-pass

```



---

## 📦 3. Industrial Infrastructure Organization: Roles

Bade production projects mein tasks, variables, aur handlers ko ek hi file mein likhne ke bajaye hum unhein modular component structure (`roles`) mein divide karte hain.

### A. Directory Structure Tree View

Aap `playbook` root directory ke andar structural layout generate karte hain:

```text
playbook/
├── master.yml
└── roles/
    └── webserver/
        ├── handlers/
        └── tasks/
            └── main.yml

```

*Quick Command to build this structure:* `mkdir -p roles/webserver/{tasks,handlers}`

### B. Low-Level Execution Blueprint: `roles/webserver/tasks/main.yml`

*Is specialized child-file mein hum hosts ya user definitions nahi likhte, sirf direct isolated tasks define karte hain:*

```yaml
---
- name: install apache on RedHat
  yum: pkg=httpd state=latest

```

### C. The Orchestrator Root File: `master.yml`

*Is root-file mein hum sirf targeting scope specify karte hain aur dynamic links connect karte hain:*

```yaml
--- # master playbook for webservers
- hosts: demo
  user: ansible
  become: yes
  connection: ssh
  roles:
    - webserver    # Injects all tasks defined inside the webserver directory layout

```

### D. Verification Workflow

```bash
ansible-playbook master.yml
which httpd

```

---

### 🧠 At a Glance Mental Map:

1. **`when: ansible_os_family`**: Dynamic automation environment filters jo machine specifications ko context verification ke mutabik cross-check karte hain.
2. **`ansible-vault`**: Strict secure compliance layer taake pipeline automation logs ya raw repositories mein parameters leaks na hon.
3. **`roles/` Pattern**: Monolithic (single thick file) configuration code style ko micro-component building blocks mein translate karne ka enterprise structural standard.
