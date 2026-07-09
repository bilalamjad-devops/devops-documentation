### SSH ⭐⭐⭐⭐⭐

This is probably the biggest concept in your notes.

Question:

> How does the Control Node communicate with remote servers?

Answer:

SSH.

```
Ansible Server
       │
       │ SSH
       ▼
Node1
```

Ansible does **not** install an agent on remote servers.

It connects over SSH.


### Password Authentication ⭐⭐⭐☆

Initially you connected like this:

```
ssh ansible@10.0.0.5
```

Password:

```
*******
```

Concept:

Authentication can be done using passwords.

---

### SSH Key Authentication ⭐⭐⭐⭐⭐

Then you used

```
ssh-keygen

ssh-copy-id
```

Concept:

Instead of typing a password every time,

Use

* Private Key
* Public Key

```
Private Key
      │
      ▼
Control Node
      │
      ▼
Managed Node
Public Key
```

This enables secure, passwordless authentication and is the recommended method for Ansible.

---

### Trust Relationship ⭐⭐⭐⭐☆

After copying the public key,

Node1 trusts the Control Node.

Concept:

SSH trust is based on matching key pairs.

No password is needed because the remote server recognizes the Control Node's public key.

---

### SSH Configuration ⭐⭐⭐☆

You edited

```
/etc/ssh/sshd_config
```

Concept:

The SSH server's behavior is controlled by its configuration.

Examples:

* Allow root login
* Enable/disable password authentication
* Specify the SSH port
* Restrict users
