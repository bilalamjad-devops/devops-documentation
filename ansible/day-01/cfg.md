### Configuration Files ⭐⭐⭐⭐☆

You edited

```
/etc/ansible/ansible.cfg
```

Concept:

Applications have configuration files.

Examples

* nginx → nginx.conf
* ssh → sshd_config
* Docker → daemon.json
* Ansible → ansible.cfg

Learning to edit configuration files is a general Linux/DevOps skill.


---


ansible.cfg

You don't.

For a beginner project, you can run Ansible without it.

For example:


```ansible
ansible-playbook -i hosts.ini site.yml
```

works perfectly.

Then why does ansible.cfg exist?

It saves you from typing the same options every time.

Without it:

```ansible
ansible-playbook \
-i hosts.ini \
-u ubuntu \
--private-key ~/.ssh/id_rsa \
site.yml
```

With ansible.cfg:

```ansible
ansible-playbook site.yml
```


