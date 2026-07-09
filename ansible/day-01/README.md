These notes contain the right information, but they're hard to scan because they mix **commands**, **configuration**, and **concepts**.

For technical notes (especially DevOps), think in this order:

> **Purpose → Steps → Verification → Concepts**

This makes it much easier to review later.

---

# Ansible Setup (Password Authentication)

## Goal

Configure one **Ansible Control Node (Server)** to manage two **Managed Nodes**.

```
Ansible Server
      │
      ├── Node1
      └── Node2
```

---

# 1. Install Ansible (Control Node)

```bash
wget https://fedoraproject.org/pub/epel-release-latest-7.noarch.rpm
```

```bash
apt install epel-release-latest-7.noarch.rpm
```

Verify installation:

```bash
ansible --version
```

---

# 2. Inventory File

Inventory file location:

```text
/etc/ansible/hosts
```

Edit:

```bash
vi /etc/ansible/hosts
```

Example:

```ini
[demo]
PrivateIPofNode1
PrivateIPofNode2
```

**Concept**

* Inventory = List of managed machines
* `[demo]` = Group name

---

# 3. Configure Ansible

Configuration file:

```text
/etc/ansible/ansible.cfg
```

Edit:

```bash
vi /etc/ansible/ansible.cfg
```

Uncomment:

```ini
inventory = /etc/ansible/hosts
sudo_user = root
```

---

# 4. Create Ansible User

## On Control Node

```bash
adduser ansible
passwd ansible
```

---

## On Node1

```bash
sudo su
adduser ansible
passwd ansible
```

---

## On Node2

```bash
sudo su
adduser ansible
passwd ansible
```

---

# 5. Configure Passwordless sudo

Run on:

* Control Node
* Node1
* Node2

```bash
visudo
```

Add:

```text
root     ALL=(ALL) ALL
ansible  ALL=(ALL) NOPASSWD: ALL
```

### Why?

Allows the **ansible** user to execute sudo commands **without entering a password**.

Example:

Without sudo:

```bash
yum install httpd -y
```

With sudo:

```bash
sudo yum install httpd -y
```

---

# 6. Enable SSH Password Login

Run on all machines.

Edit:

```bash
vi /etc/ssh/sshd_config
```

Update:

```text
PermitRootLogin yes
PasswordAuthentication yes

#PasswordAuthentication no
```

Restart SSH:

```bash
service sshd restart
```

---

# 7. Test SSH Login

Switch to ansible user.

```bash
su - ansible
```

Connect to Node1.

```bash
ssh ansible@PrivateIPofNode1
```

Enter password.

Create a file to verify you're actually on Node1.

---

# 8. Configure SSH Key Authentication (Recommended)

Generate SSH key on the Control Node.

```bash
ssh-keygen
```

Keys are stored in:

```text
~/.ssh/
```

Example:

```text
id_rsa
id_rsa.pub
```

Copy the public key.

```bash
ssh-copy-id ansible@PrivateIPofNode1
```

```bash
ssh-copy-id ansible@PrivateIPofNode2
```

Now Ansible can connect without asking for a password.

---

# 9. Host Patterns

### All hosts

```bash
ansible all --list-hosts
```

---

### Specific group

```bash
ansible demo --list-hosts
```

---

### First host in a group

```bash
ansible demo[0] --list-hosts
```

`[0]` refers to the **first host** in the inventory group.

---

# Quick Revision (30 Seconds)

| Concept                    | Remember                           |
| -------------------------- | ---------------------------------- |
| Control Node               | Machine where Ansible is installed |
| Managed Nodes              | Servers controlled by Ansible      |
| Inventory                  | `/etc/ansible/hosts`               |
| Config File                | `/etc/ansible/ansible.cfg`         |
| Group                      | `[demo]`                           |
| SSH                        | Used to connect to managed nodes   |
| `ssh-copy-id`              | Enables passwordless SSH           |
| `visudo`                   | Configure sudo permissions         |
| `ansible --version`        | Verify installation                |
| `ansible all --list-hosts` | Show all inventory hosts           |

---

## A few corrections to your original notes

* `ansible --verion` → `ansible --version`
* `ansile-server` → `ansible-server`
* `sudo_user = root` is a legacy setting and is generally unnecessary in modern Ansible. Today, it's more common to use `become: true` in playbooks or the `-b` (`--become`) option when running commands.
* "`etc` abbreviation: Editable Text Configuration" is **not correct**. `/etc` is simply the standard Unix directory for **system-wide configuration files**. Its historical origin isn't "Editable Text Configuration."

One suggestion that will improve all of your DevOps notes: separate **commands** from **concepts**. For example, use headings like **Goal**, **Configuration**, **Commands**, **Verification**, and **Key Concepts**. When you open the notes months later, you'll understand the entire workflow in less than a minute instead of rereading every command.
