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
