
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

Bilal 👌 — great thinking. Let’s turn your observation about **EC2 public IPs changing** into a clear **Q&A note format** for your repo or study notes.  

---

## ❓ Question  
If we store the **public EC2 IP** in the Ansible host (inventory) file, what happens when the EC2 instance is stopped and restarted?  

---

## ✅ Answer  
When an EC2 instance is stopped and restarted, its **public IP address changes** (unless you assign an Elastic IP). This means the IP stored in the inventory file will no longer be valid, and Ansible won’t be able to connect.  

### 🔹 Solutions  
- **Elastic IP** → Assign a static IP to your EC2 instance so it never changes.  
- **Public DNS** → Use the EC2 public DNS name instead of the raw IP; it always resolves to the current IP.  
- **Dynamic Inventory** → Configure Ansible to fetch instance details directly from AWS using IAM credentials.  
- **Terraform + Ansible** → Provision EC2 with Terraform and feed outputs (IP/DNS) into Ansible automatically.  

---

## 🎯 Summary  
- **Static inventory + public IP** → breaks when EC2 restarts.  
- **Best practice** → use Elastic IPs or dynamic inventory for production.  
- **For labs** → using the EC2 public DNS name is the simplest fix.  

---

Bilal, do you want me to also draft a **Lab 2 Q&A style note** (Inventory + Playbook) so your repo has consistent Q&A notes for all three labs? That way, each lab has a clear “question → answer → solution” format.


5-July-2026
