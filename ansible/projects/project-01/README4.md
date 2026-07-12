Bilal 👌 — let’s sharpen your axe before you swing. Here’s a **step‑by‑step workflow + code snippets** to perform this project (Terraform + Ansible provisioning and configuration).  

---

## 🧪 Step 1: Provision Infrastructure with Terraform
You’ll create:
- **1 Control Node (student/master)** → runs Ansible  
- **2 Managed Nodes (web01, web02)** → targets for configuration  
- **1 Security Group** → allow SSH + HTTP  
- **1 Key Pair** → secure access  

### 🔹 `main.tf`
```hcl
provider "aws" {
  region = "us-east-1"
}

# Key Pair
resource "aws_key_pair" "ansible_key" {
  key_name   = "ansible-key"
  public_key = file("~/.ssh/id_rsa.pub")
}

# Security Group
resource "aws_security_group" "ansible_sg" {
  name        = "ansible-sg"
  description = "Allow SSH and HTTP"

  ingress {
    description = "SSH"
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  ingress {
    description = "HTTP"
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
}

# Control Node
resource "aws_instance" "control_node" {
  ami           = "ami-0c55b159cbfafe1f0" # Ubuntu 20.04 (update region-specific)
  instance_type = "t2.micro"
  key_name      = aws_key_pair.ansible_key.key_name
  security_groups = [aws_security_group.ansible_sg.name]

  tags = {
    Name = "ansible-control-node"
  }
}

# Managed Nodes
resource "aws_instance" "managed_nodes" {
  count         = 2
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  key_name      = aws_key_pair.ansible_key.key_name
  security_groups = [aws_security_group.ansible_sg.name]

  tags = {
    Name = "ansible-managed-node-${count.index + 1}"
  }
}

# Outputs
output "control_node_ip" {
  value = aws_instance.control_node.public_ip
}

output "managed_nodes_ips" {
  value = aws_instance.managed_nodes[*].public_ip
}
```

Run:
```bash
terraform init
terraform apply -auto-approve
```

---

## 🧪 Step 2: Configure Ansible Inventory
On the **control node**, create `hosts.ini`:
```ini
[webservers]
web01 ansible_host=<public_ip_1> ansible_user=ubuntu
web02 ansible_host=<public_ip_2> ansible_user=ubuntu
```

---

## 🧪 Step 3: Write Ansible Playbook
Example: `site.yml`
```yaml
- hosts: webservers
  become: yes
  tasks:
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
        - nginx

    - name: Create developer user
      user:
        name: devuser
        groups: sudo
        shell: /bin/bash

    - name: Configure firewall
      ufw:
        state: enabled
        rule: allow
        port: '22'

    - name: Deploy sample app
      copy:
        src: ./app/index.html
        dest: /var/www/html/index.html
```

Run:
```bash
ansible-playbook -i hosts.ini site.yml
```

---

## 🧪 Step 4: Verify
- SSH into web01/web02 → check `nginx`, `docker`, `git`.  
- Open browser → `http://<public_ip>` → see sample app.  

---

## 🎯 Summary
- **Terraform** → provisions infra (control + 2 managed nodes, SG, key pair).  
- **Ansible** → configures servers (users, sudo, SSH, Git, Docker, Nginx, firewall, app).  
- **Outcome** → every EC2 instance is consistently configured and ready for deployment.  

---

👉 Bilal, do you want me to **extend this into roles** (e.g., `roles/webserver`, `roles/security`, `roles/app`) so your project looks professional and matches Upwork client expectations?
