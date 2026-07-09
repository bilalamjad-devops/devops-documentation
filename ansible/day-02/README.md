These notes are now moving from **Ansible setup** to **using Ansible modules**. I would organize them around the concept of **"What can Ansible do?"** rather than just listing commands.

---

## Ansible Ad-hoc Commands

### Goal

Learn how to use Ansible modules to perform tasks on managed nodes without writing a playbook.

---

## Command Structure

Most ad-hoc commands follow this format:

```bash
ansible <host-pattern> -b -m <module> -a "<module arguments>"
```

### Meaning of each option

| Option           | Meaning                           |
| ---------------- | --------------------------------- |
| `ansible`        | Run an Ansible ad-hoc command     |
| `<host-pattern>` | Target hosts or host group        |
| `-b`             | Become (run with sudo privileges) |
| `-m`             | Module to execute                 |
| `-a`             | Arguments passed to the module    |

Example:

```bash
ansible demo -b -m yum -a "name=httpd state=present"
```

---

## 1. yum Module

### Install Apache (httpd)

```bash
ansible demo -b -m yum -a "name=httpd state=present"
```

### Verify on a Managed Node

```bash
which httpd
```

or

```bash
sudo service httpd status
```

### Concept

The `yum` module manages software packages on RHEL/CentOS systems.

Common states:

* `present` → Install package
* `latest` → Upgrade to latest version
* `absent` → Remove package

---

# 2. service Module

### Start Apache

```bash
ansible demo -b -m service -a "name=httpd state=started"
```

Verify:

```bash
sudo service httpd status
```

### Concept

The `service` module manages Linux services.

Common states:

* `started`
* `stopped`
* `restarted`
* `reloaded`

---

## 3. user Module

Create a new user.

```bash
ansible demo -b -m user -a "name=bhupendarrajput state=present"
```

Verify:

```bash
cat /etc/passwd
```

### Concept

The `user` module manages Linux user accounts.

Examples:

* Create user
* Delete user
* Modify user
* Lock user

---

## 4. copy Module

### Step 1

Create a file on the Ansible Control Node.

```bash
touch copiedfromserver
```

---

### Step 2

Copy it to managed nodes.

```bash
ansible demo -b -m copy -a "src=copiedfromserver dest=/tmp/"
```

---

### Step 3

Verify.

```bash
ls /tmp/
```

### Concept

The `copy` module copies files from:

**Control Node → Managed Nodes**

It is commonly used to distribute:

* Configuration files
* Scripts
* Certificates
* Static files

---

## 5. setup Module (Facts Gathering)

Collect system information.

```bash
ansible demo -m setup
```

Retrieve only IPv4-related facts.

```bash
ansible demo -m setup -a "filter=*ipv4*"
```

### Concept

The `setup` module gathers facts about managed nodes, such as:

* Operating System
* IP addresses
* Hostname
* CPU
* Memory
* Disk
* Network interfaces

These facts are automatically available in playbooks.

---

## 6. Idempotency ⭐⭐⭐⭐⭐

One of the most important concepts in Ansible.

### What is idempotency?

Running the same task multiple times produces the **same final state**.

Example:

```bash
ansible demo -b -m yum -a "name=httpd state=present"
```

Run it once:

* Apache is installed.

Run it again:

* Nothing changes because Apache is already installed.

This prevents unnecessary work and makes automation safe.

### Why is it important?

Without idempotency:

* Duplicate users could be created.
* Packages could be reinstalled unnecessarily.
* Files might be overwritten every time.
* Services might restart even when no changes are needed.

With idempotency:

* Only required changes are made.
* Existing correct configurations are left unchanged.

### Where does idempotency exist?

* ✅ Ansible Modules
* ✅ Ansible Playbooks

---

## Quick Revision

| Module    | Purpose                                       |
| --------- | --------------------------------------------- |
| `yum`     | Install, update, or remove packages           |
| `service` | Start, stop, restart, or reload services      |
| `user`    | Manage Linux users                            |
| `copy`    | Copy files from Control Node to Managed Nodes |
| `setup`   | Gather system facts                           |

---

## Concepts Learned

From these notes, you're learning these core DevOps concepts:

1. **Ad-hoc Commands** – Run one-time tasks without a playbook.
2. **Modules** – Reusable units that perform specific tasks (package management, service management, user management, file copying, etc.).
3. **Package Management** – Installing and removing software using the `yum` module.
4. **Service Management** – Controlling Linux services like Apache.
5. **User Management** – Creating and managing Linux user accounts.
6. **File Distribution** – Copying files from the Control Node to Managed Nodes.
7. **Facts Gathering** – Collecting system information for automation.
8. **Idempotency** – Ensuring repeated executions produce the same desired state without unnecessary changes.

9-July-2026
