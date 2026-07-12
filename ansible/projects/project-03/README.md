Bilal 👌 — let’s complete your project by adding the **GitHub Actions workflow** so Terraform + Ansible run as a CI/CD pipeline. This will make your repo look like a full end‑to‑end automation solution.

---

## 🧩 Folder Structure Update
```
infra-project/
├── terraform/
│   └── main.tf
├── ansible/
│   ├── hosts.ini
│   ├── site.yml
│   └── roles/...
└── .github/
    └── workflows/
        └── infra-deploy.yml
```

---

## 🔹 GitHub Actions Workflow (`infra-deploy.yml`)
```yaml
name: Infra Provision + Config

on:
  push:
    branches: [ "main" ]

jobs:
  provision:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repo
        uses: actions/checkout@v3

      - name: Set up Terraform
        uses: hashicorp/setup-terraform@v2

      - name: Terraform Init
        run: terraform -chdir=terraform init

      - name: Terraform Apply
        run: terraform -chdir=terraform apply -auto-approve

  configure:
    runs-on: ubuntu-latest
    needs: provision
    steps:
      - name: Checkout repo
        uses: actions/checkout@v3

      - name: Install Ansible
        run: sudo apt-get update && sudo apt-get install -y ansible

      - name: Configure SSH
        run: |
          mkdir -p ~/.ssh
          echo "${{ secrets.ANSIBLE_PRIVATE_KEY }}" > ~/.ssh/id_rsa
          chmod 600 ~/.ssh/id_rsa

      - name: Run Playbook
        run: ansible-playbook -i ansible/hosts.ini ansible/site.yml
```

---

## 🔹 Secrets Management
- Store your **AWS credentials** (`AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`) in GitHub Secrets.  
- Store your **Ansible SSH private key** (`ANSIBLE_PRIVATE_KEY`) in GitHub Secrets.  
- Reference them in the workflow as shown above.  

---

## 🚀 Workflow Explanation
1. **Provision job** → runs Terraform to create EC2 infra.  
2. **Configure job** → runs Ansible playbooks to configure servers.  
3. **Secrets** → ensure secure access to AWS + EC2 nodes.  
4. **Trigger** → every push to `main` branch runs the pipeline.  

---

## 🎯 Why This Impresses Clients
- **End‑to‑end automation** → infra + config in one pipeline.  
- **Reusable roles** → modular Ansible design.  
- **CI/CD integration** → GitHub Actions ensures consistency.  
- **Secrets management** → secure and professional.  

---

👉 Bilal, do you want me to also prepare a **diagram caption** showing the CI/CD flow: *Developer → GitHub Push → Actions Workflow → Terraform → Ansible → EC2 Nodes*? That would make your repo visually complete and client‑ready.

12-July-2026
