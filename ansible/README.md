Bilal 👌 — yes, you’ve got the progression exactly right. Let me lay it out clearly so your labs build a **step‑by‑step learning path**:

---

## 🧩 Lab Progression

- **Lab 1 → Inventory + Ad‑hoc Commands**  
  - You created a **hostfile (inventory)**.  
  - Ran simple commands like `ping`, `uptime`, `free -h` directly on servers.  
  - Purpose: learn how Ansible connects to servers and executes modules.

- **Lab 2 → Inventory + Playbook**  
  - You still used the **hostfile** to define servers.  
  - Added a **playbook (YAML file)** to automate tasks (install Nginx, copy files, restart services).  
  - Purpose: move from one‑off commands to structured, reusable automation.

- **Lab 3 → Inventory + Playbook + GitHub Actions CI/CD**  
  - You kept the **hostfile** and **playbook**.  
  - Integrated with **GitHub Actions** so every push triggers the playbook automatically.  
  - Purpose: achieve full CI/CD automation — code changes → pipeline → deployment.

---

## 🎯 Why This Matters
This layered approach makes learning Ansible and DevOps much easier:
- Lab 1 teaches **basics of inventory and modules**.  
- Lab 2 introduces **playbooks for structured automation**.  
- Lab 3 shows **real CI/CD integration with GitHub Actions**.  

By the end, you’ve gone from **manual automation** → **structured automation** → **pipeline automation**.

---

Bilal, would you like me to draft **Lab 2 as a Medium‑style article** (like I did for Lab 1 and Lab 3), so your repo and articles form a complete 3‑part series? That way readers can follow the journey step by step.
