
### Inventory ⭐⭐⭐⭐⭐

**Question:**

> How does Ansible know which servers to manage?

Answer:

Inventory.

```
/etc/ansible/hosts
```

Example

```ini
[web]
10.0.1.10
10.0.1.11

[db]
10.0.2.20
```

Concept:

Inventory is simply a list of servers.






Bilal 👌 — good catch. Let’s clear up the difference between **`hosts`** and **`hosts.ini`** in Ansible:

---

## 🔹 `hosts` vs `hosts.ini`

- **hosts**  
  - This is the **default inventory file** that comes with Ansible (usually located at `/etc/ansible/hosts`).  
  - It’s a global file where you can define groups of servers and their connection details.  
  - If you don’t specify an inventory file when running Ansible, it will use this default `hosts`.  

- **hosts.ini**  
  - This is a **custom inventory file** you create in your project directory.  
  - It allows you to keep project‑specific server definitions separate from the global Ansible config.  
  - You explicitly tell Ansible to use it with `-i hosts.ini`.  
  - It’s more portable and is the recommended approach for projects you want to share (like your GitHub repo).  

---

## 🧪 Example

### Default `hosts` file (system-wide)
```ini
[webservers]
192.168.1.10
192.168.1.11
```

### Project-specific `hosts.ini`
```ini
[webservers]
web01 ansible_host=54.210.123.45 ansible_user=ubuntu
web02 ansible_host=3.91.45.67 ansible_user=ubuntu
```

---

## 🎯 Summary
- Use **`hosts`** → for quick tests or global Ansible setup.  
- Use **`hosts.ini`** → for project‑based inventories (best practice, especially with GitHub repos).  

---

👉 Bilal, do you want me to also show you how to **generate `hosts.ini` dynamically from Terraform outputs** so you don’t have to copy IPs manually each time? That would make your lab workflow even smoother.
