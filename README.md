Ansible Role: Gogs
==================

This role install Git - Gogs - MariaDB - Nginx on Centos7 and Ubuntu.

Access from:
- http://localhost:3000 - Gogs server
- http://ansible_hostname - Nginx server Vhost

The first register user will have admin privileges.

Requirements
------------

This Ansible playbook is meant to be run on a FRESH never used server, virtual machine or container.

Role Variables
--------------

**defaults/main.yml:***
```
# Yum packages
gogs_packages:
  - openssh-server
  - git

# Mysql root
gogs_mysql_root_password: 'password'
gogs_mysql_user: 'root'

# Gogs
gogs_gogs_version: '0.11.86'
gogs_gogs_install: '/opt'
gogs_gogs_repository: '/opt/git/gogs-repositories'
gogs_mysql_host: '127.0.0.1:3306'
gogs_mysql_gogs_user: 'gogs_user'
gogs_mysql_gogs_password: 'gogs_pass'
gogs_mysql_gogs_db: 'gogs_db'
```

Role Templates
==============

```
gogs_app.ini.j2
gogs_nginx.j2
gogs_service.j2
```

Dependencies
------------

```
squintans.mariadb
squintans.nginx
```

Example Playbook
----------------

**Example with prompt:**
```
- hosts: "{{ vm }}"
  gather_facts: True

  vars_prompt:
    - name: "vm"
      prompt: "VM"
      private: no

  roles:
    - { role: squintans.mariadb }
    - { role: squintans.nginx }
    - { role: squintans.gogs }
```

Playbook Call
=============
```
ansible-playbook -i inventory.yml play.yml
```

License
-------

BSD

Author Information
------------------
This role was created in 2019 by Serafín Quintáns - [@squintans](http://www.linkedin.com/in/serafin-quintans/)

