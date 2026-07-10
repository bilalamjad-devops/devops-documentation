
## 🔁 4. Mass Management with Loops (`with_items`)

Multiple objects manually generate karne ke bajaye hum single task ko sequence item supply karte hain.

```yaml
--- # Loops Playbook
- hosts: demo
  user: ansible
  become: yes
  connection: ssh
  tasks:
    - name: add a list of users
      user: name={{item}} state=present   # {{item}} is a built-in keyword for loop values
      with_items:
        - Bhupindar
        - Zeeshan
        - Kishri
        - Rajpal

```

* **Verification Command:**
```bash
cat /etc/passwd | grep -E "Bhupindar|Zeeshan"

```

