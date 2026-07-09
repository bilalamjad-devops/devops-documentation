
### Inventory ⭐⭐⭐⭐⭐

**Question:**

> How does Ansible know which servers to manage?

Answer:

Inventory.

```
/etc/ansible/hosts
```

Example

```ini
[web]
10.0.1.10
10.0.1.11

[db]
10.0.2.20
```

Concept:

Inventory is simply a list of servers.
