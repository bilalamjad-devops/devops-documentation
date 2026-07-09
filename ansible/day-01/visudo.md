
### sudo Privileges ⭐⭐⭐⭐⭐

You edited

```
visudo
```

Concept:

Normal users cannot perform administrative tasks.

```
yum install
```

requires root privileges.

Using

```
sudo
```

temporarily gives those privileges.

Ansible often uses `sudo` to install packages, manage services, or edit system files.
