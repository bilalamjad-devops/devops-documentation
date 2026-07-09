Bilal, aapke GitHub production notes ke liye is data ko aik behtareen, clean aur highly scannable **Markdown Table** format mein convert kar diya hai. Ise aap direct apni repository ki `README.md` mein copy-paste kar sakte hain.

---

# 📊 Ansible Commands & Modules Reference Sheet

### 🛠️ 1. Ansible Built-in Modules (`-m`)

Yahan hum declarative modules use karte hain jahan Ansible system ki state (`present`, `absent`, `started`) ko khud manage karta hai.

| Task / Purpose | Target | Flags | Module (`-m`) | Arguments (`-a`) | Complete Production Command |
| --- | --- | --- | --- | --- | --- |
| **Install Package (`httpd`)** | `demo` | `-b` (Sudo) | `yum` | `"pkg=httpd state=present"` | `ansible demo -b -m yum -a "pkg=httpd state=present"` |
| **Update Package** | `demo` | `-b` (Sudo) | `yum` | `"pkg=httpd state=latest"` | `ansible demo -b -m yum -a "pkg=httpd state=latest"` |
| **Uninstall/Remove Package** | `demo` | `-b` (Sudo) | `yum` | `"pkg=httpd state=absent"` | `ansible demo -b -m yum -a "pkg=httpd state=absent"` |
| **Start Service** | `demo` | `-b` (Sudo) | `service` | `"name=httpd state=started"` | `ansible demo -b -m service -a "name=httpd state=started"` |
| **Create Local User** | `demo` | `-b` (Sudo) | `user` | `"name=raj"` | `ansible demo -b -m user -a "name=raj"` |
| **Copy File to Remote Node** | `demo` | `-b` (Sudo) | `copy` | `"src=file4 dest=/tmp"` | `ansible demo -b -m copy -a "src=file4 dest=/tmp"` |

---

### ⚡ 2. Raw Ad-hoc Commands (`-a`)

Yahan hum bina kisi module ke managed nodes par direct standard Linux Linux commands shell format mein execute karte hain.

| Task / Purpose | Target | Flags | Command / Argument (`-a`) | Complete Production Command |
| --- | --- | --- | --- | --- |
| **List Directory Files (`ls`)** | `demo` | *None* | `"ls"` | `ansible demo -a "ls"` |
| **Create File on Node 1 Only** | `demo[0]` | *None* | `"touch file2"` | `ansible demo[0] -a "touch file2"` |
| **Create File on ALL Nodes** | `all` | *None* | `"touch file4"` | `ansible all -a "touch file4"` |
| **List Hidden Files (`ls -al`)** | `demo` | *None* | `"ls -al"` | `ansible demo -a "ls -al"` |
| **Install Package via Sudo Command** | `demo` | *None* | `"sudo yum install httpd -y"` | `ansible demo -a "sudo yum install httpd -y"` |
| **Install Package (Combined Flags)** | `demo` | `-ba` (Sudo + Arg) | `"yum install httpd -y"` | `ansible demo -ba "yum install httpd -y"` |
| **Remove Package (Combined Flags)** | `demo` | `-ba` (Sudo + Arg) | `"yum remove httpd -y"` | `ansible demo -ba "yum remove httpd -y"` |

---

### 💡 GitHub Formatting Key Notes for Your Repo:

* **`-b` (Become):** Sudo access target machine par activate karne ke liye use hota hai.
* **`-ba` Shortcut:** Jab aapko direct shell script chalani ho root privilege ke sath, toh alag se `-b -a` likhne ke bajaye aap `-ba` short-hand code use kar sakte hain.
